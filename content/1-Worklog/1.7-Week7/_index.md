---
title: "Week 7 Worklog"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Code Lambda AutoDeployer, Lambda Predict Handler, and API Gateway.
* Set up CloudWatch Monitoring & SNS Alerting.
*  **End-to-End test and review the entire system as a team.**
* Attend FCAJ Community Day.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Write Lambda Auto-Deployer (TelcoChurnAutoDeployer): create EndpointConfig => update Serverless Endpoint <br> - Configure IAM PassRole + Inline Policy for Deployer | 07/20/2026 | 07/20/2026 | [EventBridge from SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/automating-sagemaker-with-eventbridge.html) |
| 3   | - Write Lambda Predict Handler: parse API Gateway request => invoke SageMaker Endpoint => return prediction <br> - Configure EventBridge Rule: Model Registry Approved event => Lambda Deployer | 07/21/2026 | 07/21/2026 | [SageMaker Runtime](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_runtime_InvokeEndpoint.html) |
| 4   | - Create HTTP API in API Gateway with Lambda integration <br> - Set up CloudWatch Alarm: Lambda Predict Handler errors > 0 => SNS email alert | 07/22/2026 | 07/22/2026 | [CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 5   | - Configure EventBridge Rule: Pipeline completion => SNS notification <br> - Test and verify alarm/notification flow | 07/23/2026 | 07/23/2026 | |
| 6   | - **Team: End-to-End Testing** - upload new data => DriftChecker trigger => Pipeline runs => Model Registered => Deployer updates Endpoint => Predict API returns results <br> - Analyze CloudWatch logs to verify each step | 07/24/2026 | 07/24/2026 | [CloudWatch Log Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) |
| 7   | - **Attend FCAJ Community Day - AABW Hackathon Showcase (25/07/2026):** <br>&emsp; + Deliver a presentation on stage <br>&emsp; + Share the Six Pillars hackathon journey <br>&emsp; + Network with community members | 07/25/2026 | 07/25/2026 | |

### Week 7 Achievements:

*  **As a team, completed full End-to-End testing** - all 5 stages (data ingestion => pipeline => register => deploy => inference API) functioned correctly.

* Deployed Auto-Deploy: EventBridge captures the "Approved" event from the Model Registry => Lambda Deployer automatically update the Serverless Endpoint. Achieved zero-touch deployment from model training to production.

* Built the Inference API: API Gateway + Lambda Predict Handler => SageMaker Endpoint, returning JSON predictions.

* Set up Monitoring & Alerting: CloudWatch Alarms tracking Lambda errors, EventBridge sending Pipeline status notifications via SNS email.

* Spoke at FCAJ Community Day - a milestone in personal growth and communication confidence.
