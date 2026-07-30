---
title: "Week 8 Worklog"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Perform End-to-End testing of the full MLOps system: data upload → drift check → pipeline → deployment → inference.
* Set up Monitoring & Alerting with CloudWatch + SNS for pipeline status, Lambda errors, and endpoint latency.
* Clean up all AWS resources and ensure billing returns to $0.
* Finalize the internship report and present at FCAJ Community Day.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - End-to-End Testing: <br>&emsp; + Upload new data → DriftChecker triggers → Pipeline runs → Model Registered → Deployer updates Endpoint → Predict API returns results <br> - Analyze CloudWatch logs to verify each step | 07/20/2026 | 07/21/2026 | [CloudWatch Log Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) |
| 3   | - Set up CloudWatch Alarm: Lambda Predict Handler errors > 0 → SNS email alert <br> - Configure EventBridge Rule: Pipeline completion → SNS notification <br> - Test and verify alarm/notification flow | 07/22/2026 | 07/22/2026 | [CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 4   | - Clean up AWS resources: <br>&emsp; + Delete Serverless Endpoint & Configurations <br>&emsp; + Delete Model Registry (TelcoChurnModelGroup) <br>&emsp; + Delete SageMaker Pipeline <br>&emsp; + Delete Lambda Functions (DriftChecker, Deployer, Predict) <br>&emsp; + Empty S3 bucket, delete EventBridge Rules, SNS Topics, CloudWatch Alarms | 07/23/2026 | 07/23/2026 | |
| 5   | - Verify billing has returned to $0 in Billing Dashboard <br> - Finalize internship report: worklog, proposal, blogs, events, workshop docs <br> - Prepare presentation slides for Showcase | 07/24/2026 | 07/25/2026 | |
| 6   | - **Attend FCAJ Community Day – AABW Hackathon Showcase (25/07/2026):** <br>&emsp; + Deliver an 8-minute presentation as a Speaker <br>&emsp; + Share the Six Pillars hackathon journey <br>&emsp; + Network with community members | 07/25/2026 | 07/25/2026 | |
| 7   | - Complete report and worklog notes <br> - Write Self-evaluation & Feedback <br> - Final reflection on the 8-week journey | 07/26/2026 | 07/31/2026 | |

### Week 8 Achievements:

* Completed full End-to-End testing — all 5 stages (data ingestion → pipeline → register → deploy → inference API) functioned correctly.

* Set up Monitoring & Alerting: CloudWatch Alarms tracking Lambda errors, EventBridge sending Pipeline status notifications via SNS email.

* Thoroughly cleaned up all 11+ AWS resources — billing verified at $0.

* Finalized the complete internship report — 8 weeks of worklog, the MLOps Proposal, 2 published blogs, 6 participated events, and full workshop documentation.

* Delivered a speaker presentation at FCAJ Community Day — a milestone in personal growth and communication confidence.

* **Key reflection:** 8 weeks at FCAJ was not just about learning AWS services — it was a comprehensive growth journey spanning technical skills (20+ AWS services), hands-on system building, community engagement, technical writing, and public speaking ability.
