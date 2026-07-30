---
title: "Worklog Tuần 3"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Nắm vững kiến trúc mạng AWS: VPC, Subnet, Route Table, NAT Gateway, VPC Endpoints.
* Tìm hiểu RDS: Multi-AZ, Read Replicas, Backup, RDS Proxy.
* Làm quen với DynamoDB: Primary Key, GSI, LSI, DynamoDB Streams.
* Tìm hiểu Docker: Dockerfile, Docker Compose, Amazon ECR.
* Tìm hiểu Lambda: event-driven, Cold Start, layers, concurrency.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - VPC: Subnet, Route Table, Internet Gateway, NAT Gateway <br> - Security Groups vs Network ACLs <br> - **Thực hành:** tạo VPC với Public/Private Subnet, NAT Gateway, launch EC2 | 22/06/2026 | 22/06/2026 | [VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| 3   | - VPC Endpoints (Gateway, Interface) <br> - VPC Peering, Transit Gateway overview <br> - **Thực hành:** tạo VPC Endpoint cho S3, test kết nối Private Subnet => S3 | 23/06/2026 | 23/06/2026 | [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/) |
| 4   | - RDS: Multi-AZ, Read Replicas, Backup, encryption at rest <br> - RDS Proxy: Connection Pooling, Multiplexing, Failover, IAM Auth <br> - **Thực hành:** launch RDS PostgreSQL với Multi-AZ | 24/06/2026 | 24/06/2026 | [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/) |
| 5   | - DynamoDB: Primary Key, Sort Key, GSI, LSI <br> - DynamoDB Streams, TTL, On-Demand vs Provisioned capacity <br> - **Thực hành:** tạo DynamoDB table + GSIs, test CRUD operations | 25/06/2026 | 25/06/2026 | [DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) |
| 6   | - Docker: VM vs Container, Docker Architecture, core commands <br> - Dockerfile: FROM, RUN, COPY, CMD, EXPOSE <br> - Docker Compose, Amazon ECR: push/pull images <br> - **Thực hành:** viết Dockerfile cho Node.js, build & push lên ECR | 26/06/2026 | 26/06/2026 | [Docker Get Started](https://docs.docker.com/get-started/) |
| 7   | - Lambda: event-driven model, Cold Start, layers <br> - Concurrency: Reserved vs Provisioned <br> - **Thực hành:** viết Lambda function xử lý S3 event, test Cold Start | 27/06/2026 | 27/06/2026 | [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) |

### Kết quả đạt được tuần 3:

* Nắm vững kiến trúc VPC: Subnet, Route Table, NAT Gateway, VPC Endpoints, Peering.

* Hiểu và giải quyết bài toán Connection Exhaustion: Lambda (hàng nghìn function song song) vs RDS (tối đa 500 connections) => giải quyết bằng RDS Proxy Connection Pooling.

* So sánh RDS (SQL) vs DynamoDB (NoSQL) - biết chọn DB phù hợp theo workload.

* Làm chủ Docker: viết Dockerfile, build image, push lên ECR. Hiểu rõ sự khác biệt VM vs Container.

* Viết và test Lambda function đầu tiên - hiểu Cold Start, event-driven model, khi nào dùng Provisioned Concurrency.

* Thực hành khá nhiều: VPC multi-subnet, RDS Multi-AZ, DynamoDB table, Lambda + S3 event.
