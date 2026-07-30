---
title: "Week 3 Worklog"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Master network architecture on AWS: VPC, Subnet, Route Table, NAT Gateway, VPC Endpoints.
* Learn RDS: Multi-AZ, Read Replicas, Backup, RDS Proxy.
* Get familiar with DynamoDB: Primary Key, GSI, LSI, DynamoDB Streams.
* Learn Docker: Dockerfile, Docker Compose, Amazon ECR.
* Learn Lambda: event-driven, Cold Start, layers, concurrency.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - VPC: Subnet, Route Table, Internet Gateway, NAT Gateway <br> - Security Groups vs Network ACLs <br> - **Practice:** create VPC with Public/Private Subnets, NAT Gateway, launch EC2 | 06/22/2026 | 06/22/2026 | [VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| 3   | - VPC Endpoints (Gateway, Interface) <br> - VPC Peering, Transit Gateway overview <br> - **Practice:** create VPC Endpoint for S3, test Private Subnet => S3 connectivity | 06/23/2026 | 06/23/2026 | [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/) |
| 4   | - RDS: Multi-AZ, Read Replicas, Backup, encryption at rest <br> - RDS Proxy: Connection Pooling, Multiplexing, Failover, IAM Auth <br> - **Practice:** launch RDS PostgreSQL with Multi-AZ | 06/24/2026 | 06/24/2026 | [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/) |
| 5   | - DynamoDB: Primary Key, Sort Key, GSI, LSI <br> - DynamoDB Streams, TTL, On-Demand vs Provisioned capacity <br> - **Practice:** create DynamoDB table + GSIs, test CRUD operations | 06/25/2026 | 06/25/2026 | [DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) |
| 6   | - Docker: VM vs Container, Docker Architecture, core commands <br> - Dockerfile: FROM, RUN, COPY, CMD, EXPOSE <br> - Docker Compose, Amazon ECR: push/pull images <br> - **Practice:** write Dockerfile for Node.js, build & push to ECR | 06/26/2026 | 06/26/2026 | [Docker Get Started](https://docs.docker.com/get-started/) |
| 7   | - Lambda: event-driven model, Cold Start, layers <br> - Concurrency: Reserved vs Provisioned <br> - **Practice:** write Lambda function handling S3 events, test Cold Start | 06/27/2026 | 06/27/2026 | [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) |

### Week 3 Achievements:

* Mastered VPC architecture: Subnet, Route Table, NAT Gateway, VPC Endpoints, Peering.

* Understood and resolved the Connection Exhaustion problem: Lambda (thousands of parallel functions) vs RDS (500 max connections) => solved by RDS Proxy Connection Pooling.

* Compared RDS (SQL) vs DynamoDB (NoSQL) - able to select the right DB per workload.

* Proficient with Docker: writing Dockerfiles, building images, pushing to ECR. Clear understanding of VM vs Container.

* Wrote and tested the first AWS Lambda function - understood Cold Start, event-driven model, and when to use Provisioned Concurrency.

* Lots of hands-on practice: VPC multi-subnet, RDS Multi-AZ, DynamoDB tables, Lambda + S3 events.
