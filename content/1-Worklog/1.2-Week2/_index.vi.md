---
title: "Worklog Tuần 2"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Nắm vững IAM: Users, Groups, Roles, Policies và cơ chế Policy Evaluation Logic.
* Áp dụng nguyên tắc Least Privilege khi phân quyền.
* Bảo mật tài khoản với MFA, Password Policy và Credential Report.
* Học S3: bucket, versioning, lifecycle policy, encryption, static website hosting.
* Tham dự FCAJ Meetup #2.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - IAM Overview: Users, Groups, Roles, Policy Evaluation Logic <br> - Root User vs IAM User <br> - AWS Managed vs Customer Managed Policies | 08/06/2026 | 08/06/2026 | [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 3   | - IAM Roles: Service Role (EC2 → S3), Cross-Account Role <br> - **Thực hành:** tạo IAM Role cho EC2 thay vì hardcode Access Key <br> - Bật MFA, Password Policy, Credential Report | 09/06/2026 | 09/06/2026 | [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) |
| 4   | - S3: bucket, object, storage classes (Standard, IA, Glacier, Deep Archive) <br> - S3 Versioning, Lifecycle Policy, Encryption (SSE-S3, SSE-KMS) <br> - **Thực hành:** tạo bucket, upload object, cấu hình versioning + lifecycle | 10/06/2026 | 10/06/2026 | [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| 5   | - S3 Static Website Hosting + CloudFront CDN + Route 53 <br> - S3 Bucket Policy & Pre-signed URL <br> - **Thực hành:** host static website trên S3 + CloudFront | 11/06/2026 | 11/06/2026 | [S3 Static Website](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| 6   | - **Tham dự FCAJ Meetup #2 (13/06/2026):** <br>&emsp; + DevOps Engineer làm gì thực sự? <br>&emsp; + Career Path trong AWS Ecosystem <br>&emsp; + Data Analytics & Văn hóa MNC | 13/06/2026 | 13/06/2026 | AWS Study Group Community |
| 7   | - Viết recap Event 2 <br> - Ghi chép nhật ký công việc | 14/06/2026 | 14/06/2026 | |

### Kết quả đạt được tuần 2:

* Nắm vững IAM: Users, Groups, Roles; hiểu Policy Evaluation Logic (Explicit Deny > Allow > Implicit Deny).

* Triển khai IAM Role cho EC2 thay thế Access Key — giảm rủi ro lộ credential. Bảo mật tài khoản với MFA, Password Policy.

* Nắm vững S3: bucket, storage classes, versioning, lifecycle tự động, encryption, static website hosting. Chọn đúng storage class theo tần suất truy cập.

* Cấu hình CloudFront CDN + S3 để hosting website nhanh hơn, chi phí thấp hơn.

* Tham dự FCAJ Meetup #2 — hiểu sâu DevOps, MNC Culture, Data Analytics.
