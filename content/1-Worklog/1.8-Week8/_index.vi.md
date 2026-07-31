---
title: "Worklog Tuần 8"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Dọn dẹp tài nguyên AWS, xác nhận billing về 0.
* Cùng nhóm viết Blog 1 (RDS Proxy), Blog 2 (Bảo mật AWS) và Blog 3 (Terraform Infrastructure as Code).
* Viết self-evaluation, feedback, hoàn thiện báo cáo thực tập.
* Tổng kết hành trình 8 tuần.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Dọn dẹp tài nguyên AWS: <br>&emsp; + Xóa Serverless Endpoint & Configurations <br>&emsp; + Xóa Model Registry (TelcoChurnModelGroup) <br>&emsp; + Xóa SageMaker Pipeline <br>&emsp; + Xóa Lambda Functions (DriftChecker, Deployer, Predict) <br>&emsp; + Xóa S3 bucket, EventBridge Rules, SNS Topics, CloudWatch Alarms <br> - Xác nhận billing về 0 trong Billing Dashboard | 27/07/2026 | 27/07/2026 | |
| 3   | - **Cùng nhóm tìm hiểu RDS Proxy:** Connection Pooling, Multiplexing, Graceful Failover, IAM Authentication <br> - **Cùng nhóm viết Blog 1:** "Bài toán cạn kiệt kết nối với RDS Proxy" | 28/07/2026 | 28/07/2026 | [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) |
| 4   | - **Cùng nhóm tìm hiểu bảo mật AWS:** IAM Least Privilege, WAF, GuardDuty, Security Hub, Public/Private Subnet <br> - **Cùng nhóm viết Blog 2:** "Bảo mật trong phát triển phần mềm trên AWS" | 29/07/2026 | 29/07/2026 | [AWS Well-Architected Security](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/) |
| 5   | - **Cùng nhóm tìm hiểu Terraform:** IaC mindset, Plan & Apply workflow, State management, Modules, Drift detection <br> - **Cùng nhóm viết Blog 3:** "Quản lý hạ tầng với Terraform — không chỉ là click trên Console" <br> - Viết self-evaluation <br> - Viết feedback <br> - Hoàn thiện proposal, events, workshop docs | 30/07/2026 | 30/07/2026 | [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) |
| 6   | - Review toàn bộ báo cáo, sửa lỗi chính tả, format <br> - Tổng kết hành trình 8 tuần | 31/07/2026 | 31/07/2026 | |

### Kết quả đạt được tuần 8:

* **Cùng nhóm viết và đăng Blog 1** - phân tích chi tiết bài toán Connection Exhaustion khi kết hợp Lambda + RDS, và cách RDS Proxy giải quyết qua Multiplexing, Graceful Failover, và IAM Authentication.

* **Cùng nhóm viết và đăng Blog 2** - tổng hợp 5 bài học bảo mật thực tế khi phát triển trên AWS: không hardcode Access Key, Least Privilege, phân tách Public/Private Subnet, bảo vệ với WAF, giám sát với GuardDuty/Inspector/Security Hub.

* **Cùng nhóm viết và đăng Blog 3** - chia sẻ hành trình chuyển từ thao tác Console sang quản lý hạ tầng bằng code với Terraform, bao gồm: IaC, Plan/Apply, Remote State với S3 + DynamoDB, Modules, và kiểm soát Drift.

* Dọn dẹp triệt để toàn bộ 11+ tài nguyên AWS - billing verified at $0.

* Hoàn thiện báo cáo thực tập đầy đủ - worklog 8 tuần, Proposal MLOps, 6 sự kiện tham dự, 3 blog đã đăng, toàn bộ tài liệu workshop.

* Viết self-evaluation và feedback cho chương trình.

* **Tổng kết:** 8 tuần tại FCAJ không chỉ là học các service AWS - đó là hành trình trưởng thành toàn diện bao gồm: kỹ năng kỹ thuật (20+ dịch vụ AWS), xây dựng hệ thống thực tế, viết blog chia sẻ kiến thức, gắn kết cộng đồng, và kỹ năng thuyết trình trước đám đông.
