---
title: "Worklog Tuần 2"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Nắm vững AWS Identity & Access Management: Users, Groups, Roles, Policies.
* Hiểu S3: bucket, storage classes, versioning, lifecycle policies.
* Tìm hiểu S3 Static Website Hosting và tích hợp CloudFront CDN.
* Tham dự Amazon Quick & Kiro Fiesta (19/06) và FCAJ Meetup #3 - AWS Quiz Battle (20/06).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - IAM Overview: Users, Groups, Roles, Policy Evaluation Logic <br> - Root User vs IAM User <br> - AWS Managed vs Customer Managed Policies | 15/06/2026 | 15/06/2026 | [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 3   | - IAM Roles: Service Role (EC2 => S3), Cross-Account Role <br> - **Thực hành:** tạo IAM Role cho EC2 thay vì hardcode Access Key <br> - Bật MFA, Password Policy, Credential Report | 16/06/2026 | 16/06/2026 | [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) |
| 4   | - S3: bucket, object, storage classes (Standard, IA, Glacier, Deep Archive) <br> - S3 Versioning, Lifecycle Policy, Encryption (SSE-S3, SSE-KMS) <br> - **Thực hành:** tạo bucket, upload object, cấu hình versioning + lifecycle | 17/06/2026 | 17/06/2026 | [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| 5   | - S3 Static Website Hosting + CloudFront CDN + Route 53 <br> - S3 Bucket Policy & Pre-signed URL <br> - **Thực hành:** host static website trên S3 + CloudFront | 18/06/2026 | 18/06/2026 | [S3 Static Website](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| 6   | - **Tham dự Amazon Quick & Kiro Fiesta Vietnam 2026 #2 (19/06/2026):** <br>&emsp; + Workshop thực hành Agentic AI for Finance dùng Amazon Quick <br>&emsp; + Build AI Agents, Quick Flows, Quick Apps trên dataset Travel & Expense <br>&emsp; + Trải nghiệm cách AI bình dân hóa phân tích dữ liệu cho CxO | 19/06/2026 | 19/06/2026 | AWS Study Group Community |
| 7   | - **Tham dự FCAJ Meetup #3 - AWS Quiz Battle (20/06/2026):** <br>&emsp; + Thi đấu kiến thức AWS theo thể thức vòng loại trực tiếp (8 đội) <br>&emsp; + Câu hỏi từ khái niệm cơ bản đến case-study Solution Architecture thực tế | 20/06/2026 | 20/06/2026 | AWS Study Group Community |
| CN  | - Viết recap Event 3 & Event 4 <br> - Ghi chép nhật ký công việc | 21/06/2026 | 21/06/2026 | |

### Kết quả đạt được tuần 2:

* Nắm vững IAM: Users, Groups, Roles, Policies, Policy Evaluation Logic, MFA/Password Policy.

* Triển khai IAM Role cho EC2 thay thế Access Key - giảm rủi ro lộ credential. Bảo mật tài khoản với MFA, Password Policy.

* Sử dụng thành thạo S3: bucket, versioning, lifecycle policy, static website hosting, Bucket Policy.

* Tham dự Amazon Quick & Kiro - lần đầu trải nghiệm Agentic AI trên AWS, thấy được sức mạnh của AI trong việc bình dân hóa phân tích dữ liệu.

* Tham dự FCAJ Meetup #3 - lần đầu tiếp xúc với tư duy Solution Architecture qua các câu hỏi case-study cạnh tranh dưới áp lực thi đấu.
