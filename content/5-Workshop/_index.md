---
title: "Workshop"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Automating the MLOps Pipeline and Deploying a Telco Customer Churn Prediction Model on AWS

#### Overview

In a real-world enterprise environment, Machine Learning models often suffer from **Data Drift** (degradation of prediction quality over time) and require significant manual effort to operate and update.

This Workshop will guide you step-by-step through building a fully closed-loop **End-to-End Automated MLOps Platform** on the AWS Cloud for the Telco Customer Churn Prediction use case.

The system combines the power of Event-Driven Automation architecture with AWS Serverless Services:
+ **Automated Retrain Trigger:** Checks for Data Drift and launches the SageMaker Pipeline immediately when an Admin uploads new data to Amazon S3.
+ **Standard 4-Step MLOps Pipeline (SageMaker Pipeline):** Automates the entire process from Data Preprocessing (SKLearnProcessor), Training & Hyperparameter Optimization (HyperparameterTuner), Model Quality Evaluation (ScriptProcessor), to Quality Gate verification ($AUC \ge 0.80$).
+ **Continuous Deployment (CD):** Uses Amazon EventBridge to listen for the Approved label event in the Model Registry, triggering AWS Lambda to automatically create the configuration and update the **SageMaker Serverless Endpoint** without causing service interruption (Zero-Downtime Deployment).
+ **Real-time Inference API:** Integrates Amazon API Gateway (HTTP API) and a Lambda Inference Handler to accept HTTPS requests and return Churn probability instantly.
+ **Monitoring & Alerts:** Centralizes log management via CloudWatch Logs, sets up CloudWatch Alarms, and sends automated email notifications via Amazon SNS.

#### Workshop Contents

1. [1. Workshop Overview](5.1-Workshop-overview/)
2. [2. Prerequisites](5.2-Prerequiste/)
3. [3. Step-by-Step Technical Implementation](5.3-Implementation/)
4. [4. Full System Test & Validation](5.4-Test-Validation/)
5. [5. Resource Cleanup](5.5-Cleanup/)