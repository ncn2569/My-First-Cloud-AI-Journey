---
title: "Week 8 Worklog"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Clean up AWS resources and verify billing returns to $0.
* Write Blog 1 (RDS Proxy), Blog 2 (AWS Security), and Blog 3 (Terraform IaC) together as a team.
* Write self-evaluation, feedback, and finalize the internship report.
* Wrap up the 8-week journey.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Clean up AWS resources: <br>&emsp; + Delete Serverless Endpoint & Configurations <br>&emsp; + Delete Model Registry (TelcoChurnModelGroup) <br>&emsp; + Delete SageMaker Pipeline <br>&emsp; + Delete Lambda Functions (DriftChecker, Deployer, Predict) <br>&emsp; + Empty S3 bucket, delete EventBridge Rules, SNS Topics, CloudWatch Alarms <br> - Verify billing has returned to $0 in Billing Dashboard | 07/27/2026 | 07/27/2026 | |
| 3   | - **Team: Research RDS Proxy** - Connection Pooling, Multiplexing, Graceful Failover, IAM Authentication <br> - **Team: Write Blog 1** - "Connection Exhaustion and RDS Proxy" | 07/28/2026 | 07/28/2026 | [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) |
| 4   | - **Team: Research AWS Security** - IAM Least Privilege, WAF, GuardDuty, Security Hub, Public/Private Subnet design <br> - **Team: Write Blog 2** - "Security in Software Development on AWS" | 07/29/2026 | 07/29/2026 | [AWS Well-Architected Security](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/) |
| 5   | - **Team: Research Terraform** - IaC mindset, Plan & Apply workflow, State management, Modules, Drift detection <br> - **Team: Write Blog 3** - "Infrastructure Management with Terraform — Beyond Clicking on the Console" <br> - Write self-evaluation <br> - Write feedback <br> - Finalize proposal, events, workshop docs | 07/30/2026 | 07/30/2026 | [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) |
| 6   | - Review entire report, fix typos and formatting <br> - Wrap up the 8-week journey | 07/31/2026 | 07/31/2026 | |

### Week 8 Achievements:

* **As a team, wrote and published Blog 1** - detailed analysis of the Connection Exhaustion problem when combining Lambda + RDS, and how RDS Proxy addresses it through Multiplexing, Graceful Failover, and IAM Authentication.

* **As a team, wrote and published Blog 2** - compiled 5 practical security lessons when developing on AWS: never hardcode Access Keys, apply Least Privilege, separate Public/Private Subnets, protect with WAF, and monitor with GuardDuty/Inspector/Security Hub.

* **As a team, wrote and published Blog 3** - shared the journey from manual Console operations to Infrastructure as Code with Terraform, covering: IaC concepts, Plan/Apply workflow, Remote State with S3 + DynamoDB, reusable Modules, and Drift control.

* Thoroughly cleaned up all 11+ AWS resources - billing verified at $0.

* Finalized the complete internship report - 8 weeks of worklog, the MLOps Proposal, 6 participated events, 3 published blogs, and full workshop documentation.

* Wrote self-evaluation and feedback for the program.

* **Key reflection:** 8 weeks at FCAJ was not just about learning AWS services - it was a comprehensive growth journey spanning technical skills (20+ AWS services), hands-on system building, knowledge sharing through technical blogs, community engagement, and public speaking ability.
