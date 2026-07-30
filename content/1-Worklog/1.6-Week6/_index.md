---
title: "Week 6 Worklog"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Write preprocessing and evaluation scripts for the MLOps Pipeline.
* Code Lambda DriftChecker with S3 Event trigger.
*  **Build the complete SageMaker Pipeline together as a team.**

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Review AABW hackathon results <br> - Write hackathon recap | 07/13/2026 | 07/13/2026 | |
| 3   | - Write preprocessing.py: data cleaning, One-Hot Encoding, train/val/test split <br> - Test preprocessing script on SageMaker Processing Job | 07/14/2026 | 07/14/2026 | [SageMaker Processing](https://docs.aws.amazon.com/sagemaker/latest/dg/processing-job.html) |
| 4   | - Write evaluate.py: decompress best model from HPO, evaluate AUC <br> - Configure evaluation.json output for ConditionStep | 07/15/2026 | 07/15/2026 | |
| 5   | - Write Lambda DriftChecker: compare baseline vs new data statistical distribution <br> - Configure S3 Event Notification: PUT event => Lambda DriftChecker | 07/16/2026 | 07/16/2026 | [S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) |
| 6   | - **Team: Build SageMaker Pipeline** - ProcessingStep => TuningStep => EvalStep => ConditionStep (AUC >= 0.80) => ModelStep (Register) <br> - Test Pipeline execution | 07/17/2026 | 07/17/2026 | [SageMaker Pipelines](https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html) |
| 7   | - Test full Pipeline flow, review code <br> - Write worklog notes | 07/18/2026 | 07/18/2026 | |

### Week 6 Achievements:

*  **As a team, built the complete 4-step SageMaker Pipeline:** Processing (data prep) => HPO (XGBoost tuning) => Evaluation (AUC check) => Condition/Register. The pipeline automatically approves models with AUC >= 0.80.

* Wrote and tested preprocessing.py and evaluate.py scripts that integrate with SageMaker Processing Jobs and Pipeline steps.

* Implemented Data Drift detection foundation: Lambda DriftChecker compares statistical distributions of new vs baseline data. S3 Event Notification triggers the DriftChecker on new file uploads.

* Reviewed AABW Hackathon results - documented lessons learned about Agentic AI, team collaboration under pressure.
