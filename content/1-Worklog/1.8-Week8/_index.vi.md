---
title: "Worklog Tuần 8"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Kiểm thử End-to-End toàn bộ hệ thống MLOps: upload data → drift check → pipeline → deployment → inference.
* Thiết lập Monitoring & Alerting với CloudWatch + SNS: trạng thái pipeline, lỗi Lambda, độ trễ endpoint.
* Dọn dẹp toàn bộ tài nguyên AWS, xác nhận billing về 0.
* Hoàn thiện báo cáo thực tập và trình bày tại FCAJ Community Day.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - End-to-End Testing: <br>&emsp; + Upload data mới → DriftChecker trigger → Pipeline chạy → Model Registered → Deployer update Endpoint → Predict API trả kết quả <br> - Phân tích CloudWatch logs để xác minh từng bước | 20/07/2026 | 21/07/2026 | [CloudWatch Log Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) |
| 3   | - Thiết lập CloudWatch Alarm: Lambda Predict Handler errors > 0 → SNS gửi email <br> - Cấu hình EventBridge Rule: Pipeline hoàn thành → SNS notification <br> - Test và xác minh luồng alarm/notification | 22/07/2026 | 22/07/2026 | [CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 4   | - Dọn dẹp tài nguyên AWS: <br>&emsp; + Xóa Serverless Endpoint & Configurations <br>&emsp; + Xóa Model Registry (TelcoChurnModelGroup) <br>&emsp; + Xóa SageMaker Pipeline <br>&emsp; + Xóa Lambda Functions (DriftChecker, Deployer, Predict) <br>&emsp; + Xóa S3 bucket, EventBridge Rules, SNS Topics, CloudWatch Alarms | 23/07/2026 | 23/07/2026 | |
| 5   | - Xác nhận billing về 0 trong Billing Dashboard <br> - Hoàn thiện báo cáo: worklog, proposal, blogs, events, workshop docs <br> - Chuẩn bị slide trình bày cho Showcase | 24/07/2026 | 25/07/2026 | |
| 6   | - **Tham dự FCAJ Community Day – AABW Hackathon Showcase (25/07/2026):** <br>&emsp; + Trình bày 8 phút với tư cách Speaker <br>&emsp; + Chia sẻ hành trình hackathon Six Pillars <br>&emsp; + Giao lưu với cộng đồng | 25/07/2026 | 25/07/2026 | |
| 7   | - Hoàn thiện báo cáo và nhật ký <br> - Viết Self-evaluation & Feedback <br> - Tổng kết hành trình 8 tuần | 26/07/2026 | 31/07/2026 | |

### Kết quả đạt được tuần 8:

* Hoàn thành kiểm thử End-to-End toàn bộ 5 khâu — tất cả hoạt động chính xác từ data ingestion đến inference qua API.

* Thiết lập Monitoring & Alerting: CloudWatch Alarms theo dõi Lambda errors, EventBridge gửi Pipeline status notification qua SNS email.

* Dọn dẹp triệt để toàn bộ 11+ tài nguyên AWS — billing verified at $0.

* Hoàn thiện báo cáo thực tập đầy đủ — worklog 8 tuần, Proposal MLOps, 2 blog đã đăng, 6 sự kiện tham dự, toàn bộ tài liệu workshop.

* Trình bày với tư cách Speaker tại FCAJ Community Day — một cột mốc quan trọng về sự trưởng thành cá nhân và tự tin trong giao tiếp.

* **Tổng kết:** 8 tuần tại FCAJ không chỉ là học các service AWS — đó là hành trình trưởng thành toàn diện bao gồm: kỹ năng kỹ thuật (20+ dịch vụ AWS), xây dựng hệ thống thực tế, gắn kết cộng đồng, viết blog kỹ thuật, và kỹ năng thuyết trình trước đám đông.
