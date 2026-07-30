---
title: "Worklog Tuần 4"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Học Docker: Image, Container, Dockerfile, Docker Compose, push image lên Amazon ECR.
* Tìm hiểu các dịch vụ database AWS: RDS (PostgreSQL), RDS Proxy, DynamoDB, ElastiCache.
* Hiểu bài toán Connection Exhaustion và cách RDS Proxy giải quyết.
* Đăng Blog nhóm #1.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Docker: VM vs Container, Docker Architecture, các lệnh core <br> - Dockerfile: FROM, RUN, COPY, CMD, EXPOSE, layer caching <br> - **Thực hành:** viết Dockerfile cho Node.js, build & run container | 22/06/2026 | 22/06/2026 | [Docker Get Started](https://docs.docker.com/get-started/) |
| 3   | - Docker Compose: multi-container app (frontend + backend + DB) <br> - Amazon ECR: push/pull image <br> - Tổng quan: ECS, EKS, Fargate <br> - **Thực hành:** chạy multi-container app, push Docker image lên ECR | 23/06/2026 | 23/06/2026 | [Amazon ECR Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| 4   | - Tổng quan AWS Database: RDS (MySQL, PostgreSQL, Aurora), DynamoDB, ElastiCache <br> - RDS: Multi-AZ, Read Replicas, Backup, encryption at rest <br> - **Thực hành:** launch RDS PostgreSQL với Multi-AZ | 24/06/2026 | 24/06/2026 | [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/) |
| 5   | - RDS Proxy: Connection Pooling, Multiplexing, Failover, IAM Auth <br> - DynamoDB: Primary Key, Sort Key, GSI, LSI, DynamoDB Streams <br> - **Thực hành:** Lambda → RDS Proxy → RDS, tạo DynamoDB table + GSIs | 25/06/2026 | 25/06/2026 | [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) |
| 6   | - Viết Blog nhóm #1: Connection Exhaustion & RDS Proxy <br> - Đăng lên AWS Study Group | 26/06/2026 | 26/06/2026 | [DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) |
| 7   | - Ôn tập Docker, Database services <br> - Ghi chép nhật ký công việc | 27/06/2026 | 27/06/2026 | |

### Kết quả đạt được tuần 4:

* Thành thạo Docker: viết Dockerfile hiệu quả, chạy multi-container app với Compose, push image lên ECR. Hiểu các lựa chọn orchestration ECS, EKS, Fargate.

* Launch RDS PostgreSQL với Multi-AZ, cấu hình Read Replicas và automated backup.

* Hiểu và giải quyết bài toán Connection Exhaustion: Lambda (hàng nghìn function song song) vs RDS (tối đa 500 connections) → giải quyết bằng RDS Proxy Connection Pooling.

* So sánh RDS (SQL) vs DynamoDB (NoSQL) vs ElastiCache (in-memory) — biết chọn DB phù hợp theo workload.

* Đăng Blog #1 — bài viết kỹ thuật đầu tiên chia sẻ với cộng đồng.
