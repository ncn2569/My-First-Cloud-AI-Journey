---
title : "Prerequisites"
date : 2026-07-27
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

# Workshop Prerequisites

Before deploying the MLOps system on AWS, ensure the AWS account, IAM permissions, S3 storage structure, and execution environment are fully prepared as described below.

---

## AWS Account & IAM Requirements
- **AWS Account:** Must have access to AWS Management.
- **IAM Permissions:** The IAM user account needs AdministratorAccess or at minimum the following policies:
  - `AmazonSageMakerFullAccess`
  - `AWSLambda_FullAccess`
  - `AmazonS3FullAccess`
  - `AmazonEventBridgeFullAccess`
  - `AmazonSNSFullAccess`
  - `AmazonAPIGatewayAdministrator`
  - `IAMFullAccess` (to configure PassRole)

---

## Create IAM Roles for Services
The system uses the following IAM Roles to delegate permissions between services (following the Principle of Least Privilege):

1. **`SageMaker-Telco-Churn-Role`:**
   - **Service Trust:** `sagemaker.amazonaws.com`
   - **Attached Policies:** `AmazonSageMakerFullAccess`, `AmazonS3FullAccess`.
   - **Purpose:** Grants SageMaker Processing Jobs, HPO Jobs, Evaluation, and Serverless Endpoint access to S3 data.
 
![telco-churn-role](/images/3-Prerequiste/telco-churn-role.png)

2. **`Lambda-Execution-Role` (for Lambda Trigger & Lambda Deployer):**
   - **Service Trust:** `lambda.amazonaws.com`
   - **Attached Policies:** `AWSLambdaBasicExecutionRole`, `AmazonSageMakerFullAccess`, `AmazonS3FullAccess`.
   - **Inline Policy (`PassRolePolicy`):** Allows Lambda to execute the `iam:PassRole` command to the `SageMaker-Execution-Role`:
     ```json
     {
         "Version": "2012-10-17",
         "Statement": [
             {
                 "Effect": "Allow",
                 "Action": "iam:PassRole",
                 "Resource": "arn:aws:iam::<YOUR_ACCOUNT_ID>:role/<SageMaker-Execution-Role-Name>"
             }
         ]
     }
     ```

---

## Create S3 Bucket & Data Lake Folder Structure
Create 1 S3 Bucket with a globally unique name (e.g., `telco-churn-mlops-<account-id>`).

Create the following folder structure (Prefixes) inside the Bucket:
```text
telco-churn-mlops-<account-id>/
├── raw/                 # Contains raw data (.csv)
├── processed/           # Contains preprocessed data
│   ├── train/
│   ├── validation/
│   └── test/
└── models/              # Contains model.tar.gz archive files
```
![s3](/images/3-Prerequiste/S3.png)


## Prepare Data & Programming Environment (Local / SageMaker Studio)
- **Dataset:** Download the initial training data file WA_Fn-UseC_-Telco-Customer-Churn.csv.
- **SageMaker Studio / Jupyter Notebook:** Initialize a Python 3.10+ environment on SageMaker Studio.