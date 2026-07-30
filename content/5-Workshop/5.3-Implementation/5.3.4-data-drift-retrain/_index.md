---
title : "Configure AWS Lambda for Data Drift Check & Retrain Trigger"
date : 2026-07-27 
weight : 4
chapter : false
pre : " <b> 5.3.4 </b> "
---

This Lambda function is attached to an S3 Event Notification (ObjectCreated). Every time an Admin uploads a new CSV data file to the `raw/` folder, Lambda automatically runs to check for Data Drift, sends a notification via Amazon SNS, and calls `pipeline.start()` to begin Retraining.

#### Program the Lambda Function (TelcoChurnDriftChecker)
- Go to AWS Lambda $\rightarrow$ select **Create function**.
- Function name: `TelcoChurnDriftChecker` | Runtime: Python 3.11.
- Assign a Role with permissions: `AmazonS3ReadOnlyAccess`, `AmazonSageMakerFullAccess`, `AmazonSNSFullAccess`.
- In the **Configuration** tab $\rightarrow$ **General configuration**, set Timeout to **2 min 0 sec**.
- Configure Environment variables and Layers as shown below.
![ev](/images/5-Workshop/5.3-Implementation/ev.png)
![layers](/images/5-Workshop/5.3-Implementation/layers.png)
- Paste the code below into `lambda_function.py` and click **Deploy**:

```python
import os
import json
import urllib.parse
import io
import boto3
import numpy as np
import pandas as pd

s3_client = boto3.client('s3')
sagemaker_client = boto3.client('sagemaker')
sns_client = boto3.client('sns')

BUCKET_NAME = os.environ.get('BUCKET_NAME', 'telco-churn-mlops-fcaj')
PIPELINE_NAME = os.environ.get('PIPELINE_NAME', 'TelcoChurnMLOpsPipeline')
SNS_TOPIC_ARN = os.environ.get('SNS_TOPIC_ARN', 'arn:aws:sns:ap-southeast-1:606754308917:Telco-Churn-Alarm-Topic')

def calculate_drift_ks_test(df_ref, df_curr, threshold=0.15):
    """
    Calculates the Kolmogorov-Smirnov (KS-Statistic) distance between 2 distributions using NumPy.
    If the distance d_stat >= 0.15 -> That feature has drifted.
    """
    drifted_features = []
    numeric_cols = df_ref.select_dtypes(include=[np.number]).columns
    
    for col in numeric_cols:
        if col in df_curr.columns:
            ref_data = df_ref[col].dropna().values
            curr_data = df_curr[col].dropna().values
            
            if len(ref_data) > 0 and len(curr_data) > 0:
                # Sort the 2 arrays
                ref_sorted = np.sort(ref_data)
                curr_sorted = np.sort(curr_data)
                
                # Gather all unique values to compute ECDF
                data_all = np.concatenate([ref_sorted, curr_sorted])
                
                # Compute ECDF for each set
                cdf_ref = np.searchsorted(ref_sorted, data_all, side='right') / len(ref_sorted)
                cdf_curr = np.searchsorted(curr_sorted, data_all, side='right') / len(curr_sorted)
                
                # KS distance (Max Absolute Difference)
                d_stat = np.max(np.abs(cdf_ref - cdf_curr))
                
                # If distance exceeds threshold (e.g., > 0.15) -> Drift detected
                if d_stat >= threshold:
                    drifted_features.append((col, round(float(d_stat), 4)))
                    
    drift_share = len(drifted_features) / len(numeric_cols) if len(numeric_cols) > 0 else 0
    return drift_share, drifted_features


def lambda_handler(event, context):
    try:
        record = event['Records'][0]
        new_file_key = urllib.parse.unquote_plus(record['s3']['object']['key'], encoding='utf-8')
        print(f" NEW file just uploaded: s3://{BUCKET_NAME}/{new_file_key}")

        # Only process CSV files in the raw/ folder
        if not new_file_key.startswith("raw/") or not new_file_key.endswith(".csv"):
            print(" File is not in the raw/ folder or is not a CSV. Ignoring.")
            return {'statusCode': 200, 'body': 'Ignored non-raw/non-csv file.'}

        # 2. List files in raw/ to find OLD files
        response = s3_client.list_objects_v2(Bucket=BUCKET_NAME, Prefix="raw/")
        all_objects = response.get('Contents', [])

        old_csv_keys = [
            obj['Key'] for obj in all_objects 
            if obj['Key'].endswith('.csv') and obj['Key'] != new_file_key
        ]

        if not old_csv_keys:
            print(" This is the first CSV file in raw/. No old data to compare Drift against.")
            return {'statusCode': 200, 'body': 'First file uploaded. No baseline to compare.'}

        print(f" Found {len(old_csv_keys)} old CSV files as Baseline: {old_csv_keys}")
        
        # 3. Read and MERGE ALL old CSV files into a single Baseline DataFrame
        baseline_dfs = []
        for old_key in old_csv_keys:
            obj_old = s3_client.get_object(Bucket=BUCKET_NAME, Key=old_key)
            df_temp = pd.read_csv(io.BytesIO(obj_old['Body'].read()))
            baseline_dfs.append(df_temp)
            
        # Merge all historical data
        df_baseline = pd.concat(baseline_dfs, axis=0, ignore_index=True)
        print(f" Merged a total of {len(df_baseline)} rows of historical data as Baseline.")

        # Read the NEWLY uploaded file
        obj_new = s3_client.get_object(Bucket=BUCKET_NAME, Key=new_file_key)
        df_new = pd.read_csv(io.BytesIO(obj_new['Body'].read()))
        print(f" New file has {len(df_new)} rows of data.")

        # Quick preprocessing to normalize numeric columns
        for df in [df_baseline, df_new]:
            if 'customerID' in df.columns:
                df.drop(columns=['customerID'], inplace=True)
            if 'TotalCharges' in df.columns:
                df['TotalCharges'] = pd.to_numeric(df['TotalCharges'], errors='coerce')
                df['TotalCharges'].fillna(df['TotalCharges'].median(), inplace=True)

        # 4. Calculate Data Drift with KS-Test
        drift_share, drifted_cols = calculate_drift_ks_test(df_baseline, df_new)
        print(f" Proportion of drifted features: {drift_share * 100:.2f}%")

        DRIFT_THRESHOLD = 0.25 # Threshold: 25% of features fluctuating
        
        if drift_share >= DRIFT_THRESHOLD:
            message = (
                f" DATA DRIFT ALERT — CHURN DATA!\n\n"
                f"- Newly uploaded file: {new_file_key}\n"
                f"- Number of merged Baseline files: {len(old_csv_keys)} files ({len(df_baseline)} rows)\n"
                f"- Proportion of drifted features: {drift_share * 100:.1f}% (Threshold: {DRIFT_THRESHOLD * 100}%)\n"
                f"- Strongly drifted columns: {[col[0] for col in drifted_cols]}\n\n"
                f" System is AUTOMATICALLY TRIGGERING SageMaker Pipeline '{PIPELINE_NAME}'..."
            )
            print(message)

            if SNS_TOPIC_ARN:
                try:
                    sns_client.publish(
                        TopicArn=SNS_TOPIC_ARN,
                        Subject="[MLOps Alert] Data Drift Detected - Auto Retrain Triggered",
                        Message=message
                    )
                except Exception as sns_err:
                    print(f" Could not send SNS Alert: {str(sns_err)}")

            # Trigger SageMaker Pipeline
            execution = sagemaker_client.start_pipeline_execution(
                PipelineName=PIPELINE_NAME,
                PipelineExecutionDisplayName=f"AutoRetrain-Drift-{pd.Timestamp.now().strftime('%Y%m%d-%H%M')}"
            )

            return {
                'statusCode': 200,
                'body': json.dumps({
                    'status': 'Drifted',
                    'drift_share': drift_share,
                    'pipeline_execution_arn': execution['PipelineExecutionArn']
                })
            }
        else:
            message = (
                f" NEW DATA NOTIFICATION\n\n"
                f"- Newly uploaded file: {new_file_key}\n"
                f"- Fluctuation rate: {drift_share * 100:.1f}% (Below threshold {DRIFT_THRESHOLD * 100}%)\n\n"
                f" Data is stable, NO RETRAIN required."
            )
            print(message)

            if SNS_TOPIC_ARN:
                try:
                    sns_client.publish(
                        TopicArn=SNS_TOPIC_ARN,
                        Subject="[MLOps Info] New data is stable - No Retrain needed",
                        Message=message
                    )
                except Exception as sns_err:
                    print(f" Could not send SNS Info: {str(sns_err)}")

            return {
                'statusCode': 200,
                'body': json.dumps({'status': 'No Drift', 'drift_share': drift_share})
            }

    except Exception as e:
        print(f" Lambda execution error: {str(e)}")
        return {'statusCode': 500, 'body': json.dumps({'error': str(e)})}
```

#### Attach S3 Event Notification to Lambda
So that Lambda automatically runs when S3 receives a new file:
- Open Amazon S3 $\rightarrow$ Click to select the `telco-churn-mlops-fcaj` Bucket.
- Switch to the **Properties** tab $\rightarrow$ Scroll down to **Event notifications** $\rightarrow$ Click **Create event notification**.
![event-s3](/images/5-Workshop/5.3-Implementation/event-s3.png)
- Configure:
  - Event name: `NewRawCsvUploaded`.
  - Prefix: `raw/` (only capture events in the raw folder).
  - Suffix: `.csv`
  ![event-s3](/images/5-Workshop/5.3-Implementation/event-conf.png)
  - Event types: Check **All object create events** (s3:ObjectCreated:*).
    ![event-s3](/images/5-Workshop/5.3-Implementation/event-type.png)
- In the **Destination** section at the bottom:
  - Select **Lambda function**.
  - Lambda function: Select `TelcoChurnDriftChecker`.
- Click **Save changes**.