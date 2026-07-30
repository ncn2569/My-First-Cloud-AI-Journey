---
title : "Test Automated Retrain & Deployment Flow"
date : 2026-07-29
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

#### 1. Simulate Uploading a New Data File to S3
- Go to S3 Console $\rightarrow$ Buckets $\rightarrow$ `telco-churn-mlops-fcaj` $\rightarrow$
`raw/` -> Upload.
- Upload a new data file.
![new](/images/5-Workshop/5.4-Test-Validation/up-newdata.png)

#### 2. Check the Data Drift Alert & Pipeline Trigger (Lambda Drift Checker)
- Open AWS Lambda $\rightarrow$ select the `TelcoChurnDriftChecker` function $\rightarrow$ select the **Monitor** tab $\rightarrow$ **View CloudWatch logs**.
- Check the latest execution log:
  - Expected log: Lambda detects the new file `raw/new_telecom_data.csv`, performs drift check, sends a mail via SNS, and calls `start_pipeline_execution()`.
  ![log](/images/5-Workshop/5.4-Test-Validation/newdata-log.png)
- Open your Gmail inbox to check the alert email from Amazon SNS.
  ![newdata-gmail](/images/5-Workshop/5.4-Test-Validation/newdata-gmail.png)

#### 3. Monitor SageMaker Pipeline Execution Progress
- Go to Amazon SageMaker $\rightarrow$ select **Pipelines** $\rightarrow$ select `TelcoChurnPipeline`.
- Click on the latest run (Execution ID) to observe the 4-step diagram executing:
  - TelcoChurnProcessStep (Succeeded) $\rightarrow$ TelcoChurnHpoStep (Succeeded) $\rightarrow$ TelcoChurnEvalStep (Succeeded) $\rightarrow$ TelcoChurnCheckAUCThreshold (True) $\rightarrow$ TelcoChurnRegisterModelStep (Approved).
  
![pipeline](/images/5-Workshop/5.4-Test-Validation/pipeline.png)
- Confirm the Pipeline result email: When the Pipeline completes, the EventBridge Rule (`TelcoChurnPipelineStatusRule`) captures the event and sends a confirmation email:
 ![done-gmail](/images/5-Workshop/5.4-Test-Validation/done-gmail.png)

#### 4. Confirm Automatic Deployment to Serverless Endpoint (Lambda Deployer)
- Go to Amazon SageMaker $\rightarrow$ select **Model Registry** $\rightarrow$ `TelcoChurnModelGroup`.
  - You will see the new model just registered with the latest Version and Approved status.
   ![model-registry](/images/5-Workshop/5.4-Test-Validation/model-registry.png)
- The EventBridge Rule (`TelcoChurnModelApprovedRule`) captures the Approved event and automatically triggers `TelcoChurnAutoDeployer`.
- Check the Lambda Deployer (`TelcoChurnAutoDeployer`) logs:
    ![deploy-logs](/images/5-Workshop/5.4-Test-Validation/deploy-logs.png)
- Go to Amazon SageMaker $\rightarrow$ Endpoints $\rightarrow$ `telco-churn-serverless-endpoint`:
  - The Endpoint status will transition from **Updating** to **InService** with the new EndpointConfig pointing to the retrained model version!
  
![inservice](/images/5-Workshop/5.4-Test-Validation/inservice.png)
