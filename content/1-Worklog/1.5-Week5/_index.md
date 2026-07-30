---
title: "Week 5 Worklog"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Set up SageMaker Studio and get familiar with the environment.
*  **Design MLOps Pipeline architecture and write the Proposal as a team.**
* Participate in the AABW Hackathon (team Six Pillars - separate from AWS team).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Set up SageMaker Studio Domain + User Profile <br> - Explore Studio UI: notebooks, pipelines, models, endpoints | 07/06/2026 | 07/06/2026 | [SageMaker Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/) |
| 3   | - Create S3 bucket, create folder structure (raw/, processed/, models/) <br> - Upload Telco Churn dataset to S3 | 07/07/2026 | 07/07/2026 | |
| 4   | - **Team: Design full MLOPS Pipeline architecture** - S3 => Pipeline 4 bước => Model Registry => EventBridge => Lambda Deployer => Serverless Endpoint <br> - **Team: Write Proposal** - Problem Statement, Solution Architecture, Timeline | 07/08/2026 | 07/08/2026 | |
| 5   | - SageMaker Pipelines deep dive: ProcessingStep, TuningStep, ConditionStep, ModelStep <br> - SageMaker Model Registry: model groups, versions, approval status | 07/09/2026 | 07/09/2026 | [SageMaker Pipelines](https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html) |
| 6   | - Model Registry + Endpoint configurations <br> - Serverless Endpoint vs Real-time Endpoint <br> - IAM Role review for SageMaker execution | 07/10/2026 | 07/10/2026 | |
| 7   | - **AABW Hackathon Day 1 (team Six Pillars):** <br>&emsp; + Build Adaptive AML/KYC Workflow Engine <br>&emsp; + Use: Amazon Bedrock, Lambda, DynamoDB, GuardDuty, CloudWatch, Security Hub | 07/11/2026 | 07/11/2026 | [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/) |
| CN   | - **AABW Hackathon Day 2:** <br>&emsp; + Finalize + pitch demo <br> - Write worklog notes | 07/12/2026 | 07/12/2026 | |

### Week 5 Achievements:

*  **As a team, designed the full MLOps Pipeline architecture and wrote the complete Proposal with Problem Statement, Solution Architecture Diagram, Timeline, Budget, and Risk Assessment.**

* Set up SageMaker Studio and got familiar with all components: notebooks, pipelines, models, endpoints.

* Created S3 bucket infrastructure with proper folder structure for the MLOps pipeline.

* Mastered SageMaker Pipeline components: ProcessingStep, TuningStep, ConditionStep, ModelStep, and Model Registry version management.

* Competed in AABW Hackathon - built an Adaptive AML/KYC engine with Bedrock; first hands-on experience with Agentic AI, understanding the shift from "LLM chatbot" to "autonomous agent using tools."
