---
title: "Week 4 Worklog"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Study Docker: Image, Container, Dockerfile, Docker Compose, and push images to Amazon ECR.
* Learn AWS database services: RDS (PostgreSQL), RDS Proxy, DynamoDB, ElastiCache.
* Understand the Connection Exhaustion problem and how RDS Proxy solves it.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Docker: VM vs Container, Docker Architecture, core commands <br> - Dockerfile: FROM, RUN, COPY, CMD, EXPOSE, layer caching <br> - **Practice:** write a Dockerfile for Node.js, build & run container | 06/22/2026 | 06/22/2026 | [Docker Get Started](https://docs.docker.com/get-started/) |
| 3   | - Docker Compose: multi-container app (frontend + backend + DB) <br> - Amazon ECR: push/pull images <br> - Overview: ECS, EKS, Fargate <br> - **Practice:** run a multi-container app, push Docker image to ECR | 06/23/2026 | 06/23/2026 | [Amazon ECR Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| 4   | - AWS Database overview: RDS (MySQL, PostgreSQL, Aurora), DynamoDB, ElastiCache <br> - RDS: Multi-AZ, Read Replicas, Backup, encryption at rest <br> - **Practice:** launch RDS PostgreSQL with Multi-AZ | 06/24/2026 | 06/24/2026 | [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/) |
| 5   | - RDS Proxy: Connection Pooling, Multiplexing, Failover, IAM Auth <br> - DynamoDB: Primary Key, Sort Key, GSI, LSI, DynamoDB Streams <br> - **Practice:** Lambda => RDS Proxy => RDS, create DynamoDB table + GSIs | 06/25/2026 | 06/25/2026 | [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) |
| 6   | - Review Docker, Database services <br> - Write worklog notes | 06/27/2026 | 06/27/2026 | |

### Week 4 Achievements:

* Mastered Docker: wrote efficient Dockerfiles, ran multi-container apps with Compose, pushed images to ECR. Understood ECS, EKS, and Fargate orchestration options.

* Launched RDS PostgreSQL with Multi-AZ, configured Read Replicas and automated backup.

* Understood and resolved the Connection Exhaustion problem: Lambda (thousands of parallel functions) vs RDS (500 max connections) => solved by RDS Proxy Connection Pooling.

* Compared RDS (SQL) vs DynamoDB (NoSQL) vs ElastiCache (in-memory) - able to select the right DB per workload.
