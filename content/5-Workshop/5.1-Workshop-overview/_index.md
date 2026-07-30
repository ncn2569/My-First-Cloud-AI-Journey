---
title: "Overview"
date: 2026-07-27
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Workshop Overview: MLOps Platform for Telco Customer Churn Prediction

## Problem Introduction
In the telecommunications (Telco) industry, the cost of acquiring a new customer is typically 5–25 times higher than the cost of retaining an existing one. Early prediction of customer churn risk enables customer care teams to proactively offer promotions and timely support.

However, real-world Machine Learning models frequently suffer from **Data Drift / Model Drift** — prediction quality degrades over time as user behavior changes. Furthermore, manually training and deploying models from Jupyter Notebooks to a Production environment is time-consuming and prone to operational errors.

This Workshop will build a fully closed-loop **End-to-End Automated MLOps Platform** on **AWS Cloud** to comprehensively address these challenges.

---

## Workshop Goals
After completing this lab, you will have mastered and be able to deploy:
1. **Real-time Inference:** Integrate Amazon API Gateway, AWS Lambda, and AWS SageMaker Serverless Endpoint to process requests and return churn probability instantly at optimal cost ($0 when there is no traffic).
2. **Event-Driven Trigger:** Automatically detect when an Admin uploads new data to Amazon S3, check for Data Drift, and launch the Retrain flow.
3. **MLOps Workflow (SageMaker Pipeline - 4 Steps):**
   - TelcoChurnProcessStep: Preprocess data and split into Train/Validation/Test sets (SKLearnProcessor).
   - TelcoChurnHpoStep: Train & automatically optimize hyperparameters with the XGBoost model (HyperparameterTuner).
   - TelcoChurnEvalStep: Evaluate model quality on the Test set (ScriptProcessor).
   - ConditionStep: Check quality threshold ($AUC \ge 0.80$). If met, automatically register into the SageMaker Model Registry with Approved status.
4. **Continuous Deployment (CD):** Use Amazon EventBridge to listen for the Approved status from the Model Registry, triggering the AWS Lambda Deployer to automatically update the Serverless Endpoint without service interruption (Zero-Downtime Deployment).
5. **Monitoring & Alerting:** Centralize log storage via CloudWatch Logs, set up CloudWatch Alarms, and send automated email alerts to your inbox via Amazon SNS.

---

##  System Architecture Diagram

![MLOps AWS Architecture Diagram](/images/5-Workshop/5.1-Workshop-overview/architecture.png)

### AWS Services Used:
- **Amazon S3:** Stores raw data, processed data, and Model Artifacts.
- **Amazon API Gateway & AWS Lambda:** Provides REST API endpoints and handles real-time request data preprocessing.
- **AWS SageMaker Serverless Endpoint:** Deploys the XGBoost model in Serverless mode, auto-scaling.
- **AWS SageMaker Pipelines:** Manages and orchestrates the automated 4-step ML workflow.
- **AWS SageMaker Model Registry:** Centrally stores and manages model versions.
- **Amazon EventBridge:** Listens for state transition events from the Pipeline and Model Registry.
- **Amazon SNS:** Sends email notifications for Retrain results and automatic incident alerts.
- **Amazon CloudWatch:** Stores system logs, monitors metrics, and triggers error alerts.

---

## Estimated Time & Cost
- **Completion Time:** ~60–90 minutes.
- **Infrastructure Cost:** ~$0.50–$1.00 USD (If resources are cleaned up correctly following the Clean-up steps at the end of the lab, most services fall within the AWS Free Tier).