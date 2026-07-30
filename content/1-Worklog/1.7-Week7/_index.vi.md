---
title: "Worklog Tuần 7"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Code Lambda AutoDeployer, Lambda Predict Handler và API Gateway.
* Setup CloudWatch Monitoring & SNS Alert.
*  **Cùng nhóm End-to-End Test và review toàn bộ hệ thống.**
* Tham dự FCAJ Community Day.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Viết Lambda Auto-Deployer (TelcoChurnAutoDeployer): tạo EndpointConfig => update Serverless Endpoint <br> - Cấu hình IAM PassRole + Inline Policy cho Deployer | 20/07/2026 | 20/07/2026 | [EventBridge from SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/automating-sagemaker-with-eventbridge.html) |
| 3   | - Viết Lambda Predict Handler: parse request từ API Gateway => invoke SageMaker Endpoint => trả về prediction <br> - Cấu hình EventBridge Rule: Model Registry Approved event => Lambda Deployer | 21/07/2026 | 21/07/2026 | [SageMaker Runtime](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_runtime_InvokeEndpoint.html) |
| 4   | - Tạo HTTP API trong API Gateway với Lambda integration <br> - Setup CloudWatch Alarm: Lambda Predict Handler errors > 0 => SNS gửi email | 22/07/2026 | 22/07/2026 | [CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 5   | - Cấu hình EventBridge Rule: Pipeline hoàn thành => SNS notification <br> - Test và xác minh luồng alarm/notification | 23/07/2026 | 23/07/2026 | |
| 6   | - **Cùng nhóm End-to-End Testing:** upload data mới => DriftChecker trigger => Pipeline chạy => Model Registered => Deployer update Endpoint => Predict API trả kết quả <br> - Phân tích CloudWatch logs để xác minh từng bước | 24/07/2026 | 24/07/2026 | [CloudWatch Log Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) |
| 7   | - **Tham dự FCAJ Community Day - AABW Hackathon Showcase (25/07/2026):** <br>&emsp; + Trình bày trên sân khấu <br>&emsp; + Chia sẻ hành trình hackathon Six Pillars <br>&emsp; + Giao lưu với cộng đồng | 25/07/2026 | 25/07/2026 | |

### Kết quả đạt được tuần 7:

*  **Cùng nhóm hoàn thành End-to-End Testing** toàn bộ 5 khâu - tất cả hoạt động chính xác từ data ingestion đến inference qua API.

* Triển khai Auto-Deploy: EventBridge bắt sự kiện "Approved" từ Model Registry => Lambda Deployer tự động cập nhật Serverless Endpoint. Đạt zero-touch deployment từ model training đến production.

* Xây dựng Inference API: API Gateway + Lambda Predict Handler => SageMaker Endpoint, trả về JSON prediction.

* Thiết lập Monitoring & Alerting: CloudWatch Alarms theo dõi Lambda errors, EventBridge gửi Pipeline status notification qua SNS email.

* Đứng lên làm speaker tại FCAJ Community Day - một cột mốc quan trọng về sự trưởng thành cá nhân và tự tin trong giao tiếp.
