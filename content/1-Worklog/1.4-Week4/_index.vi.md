---
title: "Worklog Tuần 4"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Học EventBridge, API Gateway, CloudWatch, SNS/SQS.
* **Cùng nhóm bắt đầu tìm hiểu MLOps và phân tích dataset Telco Churn.**
* Tham dự Swinburne Cloud Mastery Career Talk.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - EventBridge: Event Bus, Rules, Event Patterns, Input Transformer <br> - SQS vs SNS vs EventBridge - khi nào dùng gì? <br> - **Thực hành:** tạo EventBridge Rule bắt S3 events => Lambda | 29/06/2026 | 29/06/2026 | [EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/) |
| 3   | - API Gateway: REST API, HTTP API, WebSocket API <br> - Stages, API Keys, Usage Plans, Throttling, CORS <br> - **Thực hành:** tạo HTTP API với Lambda integration | 30/06/2026 | 30/06/2026 | [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/) |
| 4   | - **Cùng nhóm tìm hiểu MLOps:** quy trình End-to-End, các thành phần SageMaker (Studio, Processing Jobs, Training Jobs, Pipelines) <br> - **Cùng nhóm phân tích dataset Telco Churn:** cấu trúc features, thống kê phân phối, xác định bài toán phân loại nhị phân | 01/07/2026 | 01/07/2026 | [SageMaker Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/) |
| 5   | - CloudWatch: Log Groups, Log Insights, Metrics, Alarms <br> - CloudWatch Agent & Custom Metrics <br> - **Thực hành:** tạo CloudWatch Alarm theo dõi CPU EC2, gửi cảnh báo qua SNS | 02/07/2026 | 02/07/2026 | [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/) |
| 6   | - SNS: Topics, Subscriptions (Email, SMS, Lambda, SQS) <br> - SQS: Standard vs FIFO Queues, Dead Letter Queues <br> - S3 Event Notification & Lambda trigger patterns <br> - **Thực hành:** tạo SNS Topic + Subscription gửi email | 03/07/2026 | 03/07/2026 | [SNS Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/) |
| 7   | - **Tham dự Swinburne Cloud Mastery Career Talk (04/07/2026):** <br>&emsp; + Navigating Job Market in the AI Era <br>&emsp; + Communication & Referrals as Career Skills <br>&emsp; + School vs Work & AI as a Learning Tool | 04/07/2026 | 04/07/2026 | AWS Study Group Community |

### Kết quả đạt được tuần 4:

*  **Cùng nhóm hiểu rõ quy trình MLOps End-to-End:** từ data ingestion => preprocessing => training => evaluation => model registry => deployment => monitoring. Phân tích xong dataset Telco Churn.

* Làm chủ CloudWatch: Logs, Log Insights, Metrics, Alarms. Thiết lập monitoring cho tài nguyên AWS.

* Hiểu SNS (push notification) và SQS (pull message queue) - phân biệt Standard vs FIFO, hiểu cơ chế Dead Letter Queue.

* Nắm vững EventBridge: event bus, rules, event pattern matching, input transformation.

* Sử dụng API Gateway thành thạo: tạo HTTP API, tích hợp Lambda, cấu hình throttling và CORS.

* Tham dự Career Talk - thu nhận góc nhìn thực tế về job market thời AI, sức mạnh của referral, và mindset cầu tiến.
