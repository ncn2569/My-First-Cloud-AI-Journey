---
title: "Worklog Tuần 3"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Nắm vững kiến trúc mạng AWS - VPC, Subnet, Route Table, NAT Gateway, VPC Endpoints.
* Hiểu Auto Scaling, ELB và mô hình Serverless với AWS Lambda.
* Áp dụng Security Groups và NACLs xây dựng bảo mật nhiều lớp.
* Tham dự Amazon Quick & Kiro Fiesta (Event 3) và FCAJ Meetup #3 (Event 4).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - VPC: CIDR, Public/Private Subnet, IGW, NAT Gateway <br> - Phân biệt Security Group (stateful) vs NACL (stateless) <br> - **Thực hành:** tạo VPC 10.0.0.0/16, 2 Public + 2 Private Subnets | 15/06/2026 | 15/06/2026 | [VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| 3   | - VPC Endpoints (Gateway, Interface), VPC Flow Logs <br> - EC2 Instance families + Launch Template + ALB <br> - **Thực hành:** deploy ALB + EC2 trong Public Subnet, cấu hình route tables | 16/06/2026 | 16/06/2026 | [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/) |
| 4   | - Auto Scaling Group: Scaling Policies (Target Tracking, Step Scaling) <br> - AWS Lambda: event-driven, runtime, Cold Start, Provisioned Concurrency <br> - **Thực hành:** tạo Lambda trigger từ S3, test ASG scale-out khi CPU > 70% | 17/06/2026 | 17/06/2026 | [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/) |
| 5   | - **Tham dự Amazon Quick & Kiro Fiesta (19/06/2026):** <br>&emsp; + Agentic AI cho Finance <br>&emsp; + Hands-on: Build Agent, Quick Flows, Quick App | 19/06/2026 | 19/06/2026 | |
| 6   | - **Tham dự FCAJ Meetup #3 – AWS Knowledge Battle (20/06/2026)** | 20/06/2026 | 20/06/2026 | AWS Study Group Community |
| 7   | - Viết recap Event 3 & 4 <br> - Ghi chép nhật ký công việc | 21/06/2026 | 21/06/2026 | |

### Kết quả đạt được tuần 3:

* Nắm vững VPC: thiết kế và triển khai mạng multi-tier với 2 Public + 2 Private Subnets, IGW, NAT Gateway, Route Tables trên 2 AZs.

* Hiểu VPC Endpoints và Flow Logs để kết nối dịch vụ an toàn không lộ ra Internet.

* Deploy ALB + Auto Scaling Group phản ứng theo CloudWatch CPU metric.

* Viết và test Lambda function đầu tiên - hiểu Cold Start, event-driven model, khi nào dùng Provisioned Concurrency.

* Tham dự 2 sự kiện: hands-on công cụ Agentic AI mới nhất của AWS, và thi đấu quiz kiến thức AWS.
