---
title: "Week 4 Worklog"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Learn EventBridge, API Gateway, CloudWatch, SNS/SQS.
* **Start exploring MLOps and analyzing the Telco Churn dataset as a team.**
* Attend Swinburne Cloud Mastery Career Talk.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - EventBridge: Event Bus, Rules, Event Patterns, Input Transformer <br> - SQS vs SNS vs EventBridge - when to use which? <br> - **Practice:** create EventBridge Rule capturing S3 events => Lambda | 06/29/2026 | 06/29/2026 | [EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/) |
| 3   | - API Gateway: REST API, HTTP API, WebSocket API <br> - Stages, API Keys, Usage Plans, Throttling, CORS <br> - **Practice:** create an HTTP API with Lambda integration | 06/30/2026 | 06/30/2026 | [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/) |
| 4   | - **Team: MLOps overview** - End-to-End workflow, SageMaker components (Studio, Processing Jobs, Training Jobs, Pipelines) <br> - **Team: Analyze Telco Churn dataset** - feature structure, distribution stats, define binary classification problem | 07/01/2026 | 07/01/2026 | [SageMaker Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/) |
| 5   | - CloudWatch: Log Groups, Log Insights, Metrics, Alarms <br> - CloudWatch Agent & Custom Metrics <br> - **Practice:** create a CloudWatch Alarm monitoring EC2 CPU, send alerts via SNS | 07/02/2026 | 07/02/2026 | [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/) |
| 6   | - SNS: Topics, Subscriptions (Email, SMS, Lambda, SQS) <br> - SQS: Standard vs FIFO Queues, DLQ <br> - S3 Event Notification & Lambda trigger patterns <br> - **Practice:** create SNS Topic + Email Subscription | 07/03/2026 | 07/03/2026 | [SNS Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/) |
| 7   | - **Attend Swinburne Cloud Mastery Career Talk (04/07/2026):** <br>&emsp; + Navigating Job Market in the AI Era <br>&emsp; + Communication & Referrals as Career Skills <br>&emsp; + School vs Work & AI as a Learning Tool | 07/04/2026 | 07/04/2026 | AWS Study Group Community |

### Week 4 Achievements:

*  **As a team, clearly understood the End-to-End MLOps workflow:** from data ingestion => preprocessing => training => evaluation => model registry => deployment => monitoring. Completed Telco Churn dataset analysis.

* Mastered CloudWatch: Logs, Log Insights, Metrics, Alarms. Set up monitoring for AWS resources.

* Understood SNS (push notification) and SQS (pull message queue) - can differentiate Standard vs FIFO, and understand the DLQ mechanism.

* Solid on EventBridge: event buses, rules, event pattern matching, input transformation.

* Proficient with API Gateway: creating HTTP APIs, integrating Lambda, configuring throttling and CORS.

* Attended Career Talk - gained a realistic perspective on the AI-era job market, the power of referrals, and a growth mindset.
