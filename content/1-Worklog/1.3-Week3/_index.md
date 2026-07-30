---
title: "Week 3 Worklog"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Master network architecture on AWS - Amazon VPC, Subnet, Route Table, NAT Gateway, VPC Endpoints.
* Understand Auto Scaling, ELB, and the Serverless model with AWS Lambda.
* Apply Security Groups and NACLs to build multi-layer security.
* Attend Amazon Quick & Kiro Fiesta (Event 3) and FCAJ Meetup #3 (Event 4).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - VPC: CIDR, Public/Private Subnet, IGW, NAT Gateway <br> - Distinguish Security Group (stateful) vs NACL (stateless) <br> - **Practice:** create VPC 10.0.0.0/16, 2 Public + 2 Private Subnets | 06/15/2026 | 06/15/2026 | [VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| 3   | - VPC Endpoints (Gateway, Interface), VPC Flow Logs <br> - EC2 Instance families + Launch Template + ALB <br> - **Practice:** deploy ALB + EC2 in Public Subnet, route tables configured | 06/16/2026 | 06/16/2026 | [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/) |
| 4   | - Auto Scaling Group: Scaling Policies (Target Tracking, Step Scaling) <br> - AWS Lambda: event-driven, runtime, Cold Start, Provisioned Concurrency <br> - **Practice:** create Lambda function triggered by S3, test ASG scale-out when CPU > 70% | 06/17/2026 | 06/17/2026 | [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) |
| 5   | - **Attend Amazon Quick & Kiro Fiesta (19/06/2026):** <br>&emsp; + Agentic AI for Finance <br>&emsp; + Hands-on: Build Agent, Quick Flows, Quick App | 06/19/2026 | 06/19/2026 | |
| 6   | - **Attend FCAJ Meetup #3 – AWS Knowledge Battle (20/06/2026)** | 06/20/2026 | 06/20/2026 | AWS Study Group Community |
| 7   | - Write Event 3 & 4 recap <br> - Write worklog notes | 06/21/2026 | 06/21/2026 | |

### Week 3 Achievements:

* Mastered VPC: designed and deployed a multi-tier network with 2 Public + 2 Private Subnets, IGW, NAT Gateway, Route Tables across 2 AZs.

* Understood VPC Endpoints and Flow Logs for secure service access without Internet exposure.

* Deployed ALB + Auto Scaling Group reacting to CloudWatch CPU metrics.

* Wrote and tested the first AWS Lambda function - understood Cold Start, event-driven model, and when to use Provisioned Concurrency.

* Attended 2 events: hands-on with AWS's latest Agentic AI tools, and competitive AWS knowledge quiz.
