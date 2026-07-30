---
title: "Proposal"
date: 2026-07-27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MLOps Platform for Telco Customer Churn Prediction
## An Automated MLOps System for Training, Evaluation, and Deployment of a Telco Customer Churn Prediction Model on AWS

### 1. Executive Summary
The Telco Customer Churn MLOps Platform is designed to build a fully closed-loop End-to-End MLOps Pipeline that automates the entire lifecycle of a Machine Learning model. The platform covers everything from data processing, model training and Hyperparameter Optimization (HPO), model quality evaluation, registration into the Model Registry, and automatic Deployment to a Serverless Endpoint as soon as the model is Approved. The system enables telecom businesses to proactively identify customers at risk of churning, allowing timely retention policies to be applied at the lowest possible operational cost.

### 2. Problem Statement
*Current Problem*  
Traditional Churn prediction models are typically developed manually in local environments (Local Notebooks), causing Model Drift as real-world data changes over time. The manual deployment process from Notebook to Production is time-consuming, prone to operational errors, and lacks an automatic Retrain mechanism when model performance degrades.
 
*Solution*  
Build an MLOps system on the AWS SageMaker Workflow (Pipeline) platform combined with an Event-Driven Automation architecture. When an Admin uploads new data to Amazon S3, AWS Lambda checks for Data Drift and sends notifications via SNS. If retraining is needed, the SageMaker Pipeline runs a 4-step process (Processing, HPO, Evaluation, Condition Check with AUC >= 0.80). Once the model meets the standard and transitions to Approved status in the SageMaker Model Registry, Amazon EventBridge triggers the Lambda Deployer to automatically update the Serverless Endpoint without service interruption (Zero-downtime Deployment).

*Benefits and Return on Investment (ROI)*  
- **Technical:** Reduces time from Training to Deploy from several days down to a few hours. The Serverless Endpoint mechanism optimizes infrastructure costs by only charging when inference requests occur.  
- **Business:** Early detection of churning customers, protecting revenue for the business.
- **Estimated Cost:** ~$2.5 – $4.0 USD/month for pipeline retraining runs and serverless inference.
 
### 3. Solution Architecture

![Architecture](/images/2-Proposal/architecture.png)

*AWS Services Used*  
- *Amazon S3*: Stores raw data, processed data, and Model Artifacts.
- *Amazon API Gateway & AWS Lambda (Inference)*: Receives prediction requests from clients via REST API and performs real-time data preprocessing.
- *AWS SageMaker Serverless Endpoint*: Provides a real-time inference API with the XGBoost model, auto-scaling based on traffic.
- *AWS Lambda (Drift Checker & Trigger)*: Checks for Data Drift when new data is uploaded to S3 and triggers the SageMaker Pipeline.
- *AWS SageMaker Pipelines*: Orchestrates the 4-step MLOps workflow (Processing, Tuning, Evaluation, Condition & Register).  
- *AWS SageMaker Model Registry*: Manages model versions and approval status.
- *Amazon EventBridge & AWS Lambda (Deployer)*: Listens for Model Approved events to automatically update the Serverless Endpoint.  
- *Amazon CloudWatch & Amazon SNS*: Stores Logs, sets Alarms for API/Endpoint errors, and sends automated email notifications to Gmail.

### 4. Technical Implementation
*Implementation Phases*  
  
1. *Data Exploration & Experimental Training*: Analyze the Telco Customer Churn dataset. Preprocess data using SKLearnProcessor. Conduct experimental training of a standalone XGBoost model and evaluate the AUC metric.   
2. *Pipeline Automation & MLOps Workflow*: Configure a Hyperparameter Tuning Job for XGBoost. Write an evaluation script that outputs an evaluation.json file containing AUC metrics. Build a complete SageMaker Pipeline with a ConditionStep (only registers the model if AUC $\ge$ 0.80).    
3. *Event-Driven Automated Deployment*: Program the AWS Lambda Deployer to handle flexible Endpoint updates. Configure the EventBridge Rule to capture events from the Model Registry. Integrate CloudWatch Alarms and SNS Email Alerts. 


### 5. Timeline & Milestones  
- Week 1 – Week 2: Research the problem context, process the Telco Churn dataset, and build the Baseline XGBoost Model.
- Week 3 – Week 4: Package the data processing and training workflow into SageMaker Pipelines.  
- Week 5 – Week 6: Automate the model evaluation phase and integrate with the SageMaker Model Registry.  
- Week 7: Set up EventBridge and Lambda Functions to implement the Auto-Deploy feature to the Serverless Endpoint.  
- Week 8: System-wide testing, cost optimization, Endpoint latency evaluation, and final report completion.   

### 6. Budget Estimation
- AWS Lambda & Amazon EventBridge: $0.00 USD/month (Free Tier).  
- Amazon S3: ~$0.12/month (~5 GB including Artifacts & Data).  
- AWS SageMaker Processing & Training: ~$0.35/month (`ml.m5.large` instance).  
- AWS SageMaker Hyperparameter Tuning: ~$0.80/month (6 parallel Tuning Jobs on `ml.m5.large`).  
- AWS SageMaker Serverless Endpoint: ~$1.20/month (2048 MB Memory, ~10,000 requests/month).  
- Amazon CloudWatch & SNS: ~$0.10/month.  
 

*Total*: ~$2.57 – $4.00 USD/month
 

### 7. Risk Assessment
*Risk Matrix*  
- Model Performance Drift: High impact, medium probability.  
- Uncontrolled resource cost overruns: Medium impact, low probability.   

*Mitigation Strategies*  
- Model Performance: Set a ConditionStep in the Pipeline. If the new model has AUC $< 0.80$, the Pipeline will trigger a FailStep and immediately halt registration into the Registry.  
- Cost Control: Use Serverless Endpoint (only charged per invocation, no idle waiting cost). Set an AWS Budgets Alarm to alert when costs exceed $10 USD/month.  


### 8. Expected Outcomes
- Technical: Successfully deploy a fully automated, 100% closed-loop MLOps pipeline: Data Upload -> Drift Check -> Pipeline -> Model Registry -> Auto-Deploy -> Serverless Endpoint.
- Operational: Reduce 95% of the manual effort required by Data/MLOps Engineers when deploying a new model version.