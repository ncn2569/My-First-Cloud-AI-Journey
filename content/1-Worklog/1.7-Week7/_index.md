---
title: "Week 7 Worklog"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Build the SageMaker Pipeline for Telco Churn: Processing → HPO → Evaluation → Condition → Register.
* Implement Data Drift detection with Lambda + S3 Event trigger, and automatic pipeline re-execution.
* Configure Auto-Deploy: EventBridge captures Approved events → Lambda Deployer updates the Serverless Endpoint.
* Set up the Inference API: Lambda Predict Handler + API Gateway POST endpoint.
* Publish group Blog #2 on AWS Security Best Practices.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Write preprocessing.py: data cleaning, One-Hot Encoding, train/val/test split <br> - Write evaluate.py: decompress best model from HPO, evaluate AUC <br> - Build Pipeline: ProcessingStep → TuningStep → EvalStep → ConditionStep (AUC ≥ 0.80) → ModelStep (Register) | 07/13/2026 | 07/14/2026 | [SageMaker Processing](https://docs.aws.amazon.com/sagemaker/latest/dg/processing-job.html) |
| 3   | - Write Lambda DriftChecker: compare baseline vs new data statistical distribution <br> - Configure S3 Event Notification: PUT event → Lambda DriftChecker <br> - **Practice:** upload new data, verify DriftChecker triggers the Pipeline | 07/15/2026 | 07/15/2026 | [S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) |
| 4   | - Write Lambda Auto-Deployer (TelcoChurnAutoDeployer): create EndpointConfig → update Serverless Endpoint <br> - Configure EventBridge Rule: Model Registry Approved event → Lambda Deployer <br> - Configure IAM PassRole + Inline Policy for Deployer | 07/16/2026 | 07/16/2026 | [EventBridge Events from SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/automating-sagemaker-with-eventbridge.html) |
| 5   | - Write Lambda Predict Handler: parse API Gateway request → invoke SageMaker Endpoint → return prediction <br> - Create HTTP API in API Gateway with Lambda integration <br> - **Practice:** POST sample payload, verify `{"Churn": "Yes", "Probability": 0.87}` returns correctly | 07/17/2026 | 07/17/2026 | [SageMaker Runtime](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_runtime_InvokeEndpoint.html) |
| 6   | - Write group Blog #2 on AWS Security Best Practices <br> - Publish to AWS Study Group | 07/18/2026 | 07/18/2026 | [AWS Security Best Practices](https://docs.aws.amazon.com/whitepapers/latest/aws-security-best-practices/) |
| 7   | - Review the full architecture <br> - Write worklog notes | 07/19/2026 | 07/19/2026 | |

### Week 7 Achievements:

* Built a complete 4-step SageMaker Pipeline: Processing (data prep) → HPO (XGBoost tuning) → Evaluation (AUC check) → Condition/Register. The pipeline automatically approves models with AUC ≥ 0.80.

* Implemented Data Drift detection: Lambda DriftChecker compares statistical distributions of new vs baseline data. S3 Event Notification triggers the DriftChecker, which triggers the SageMaker Pipeline when drift is detected.

* Deployed Auto-Deploy: EventBridge captures the "Approved" event from the Model Registry → Lambda Deployer automatically updates the Serverless Endpoint. Achieved zero-touch deployment from model training to production.

* Built the Inference API: API Gateway + Lambda Predict Handler → SageMaker Endpoint, returning JSON predictions.

* Published Blog #2 covering security best practices: no hardcoded credentials, Least Privilege, public/private subnet separation, WAF, and continuous monitoring with GuardDuty, Inspector, Security Hub.
