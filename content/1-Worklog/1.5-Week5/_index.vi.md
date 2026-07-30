---
title: "Worklog Tuần 5"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Học Amazon CloudWatch: Logs, Metrics, Alarms, Dashboards.
* Tìm hiểu Amazon SNS, SQS và EventBridge cho kiến trúc Event-Driven.
* Làm quen với Amazon API Gateway và các loại API (REST, HTTP, WebSocket).
* Tham dự Swinburne Cloud Mastery Career Talk.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - CloudWatch: Log Groups, Log Insights, Metrics, Alarms <br> - CloudWatch Agent & Custom Metrics <br> - **Thực hành:** tạo CloudWatch Alarm theo dõi CPU EC2, gửi cảnh báo qua SNS | 29/06/2026 | 29/06/2026 | [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/) |
| 3   | - SNS: Topics, Subscriptions (Email, SMS, Lambda, SQS) <br> - SQS: Standard vs FIFO Queues, Dead Letter Queues, Message Retention <br> - **Thực hành:** tạo SNS Topic + Subscription gửi email, SQS Queue trigger Lambda | 30/06/2026 | 30/06/2026 | [SNS Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/) |
| 4   | - EventBridge: Event Bus, Rules, Event Patterns, Input Transformer <br> - SQS vs SNS vs EventBridge - khi nào dùng gì? <br> - **Thực hành:** tạo EventBridge Rule bắt S3 events => Lambda | 01/07/2026 | 01/07/2026 | [EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/) |
| 5   | - API Gateway: REST API, HTTP API, WebSocket API <br> - Stages, API Keys, Usage Plans, Throttling, CORS <br> - **Thực hành:** tạo HTTP API với Lambda integration | 02/07/2026 | 02/07/2026 | [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/) |
| 6   | - **Tham dự Swinburne Cloud Mastery Career Talk (04/07/2026):** <br>&emsp; + Navigating Job Market in the AI Era <br>&emsp; + Communication & Referrals as Career Skills <br>&emsp; + School vs Work & AI as a Learning Tool | 04/07/2026 | 04/07/2026 | AWS Study Group Community |
| 7   | - Viết recap Event 5 <br> - Ghi chép nhật ký công việc | 05/07/2026 | 05/07/2026 | |

### Kết quả đạt được tuần 5:

* Nắm vững CloudWatch: Logs, Log Insights, Metrics, Alarms. Thiết lập monitoring real-time cho resource AWS.

* Hiểu SNS (push notification) và SQS (pull message queue) - phân biệt Standard vs FIFO, hiểu cơ chế Dead Letter Queue.

* Nắm cách EventBridge hoạt động: event bus, rules, event pattern matching, input transformation.

* Thành thạo API Gateway: tạo HTTP API, tích hợp Lambda, cấu hình throttling và CORS.

* Tham dự Career Talk - thu nhận góc nhìn thực tế về job market thời AI, sức mạnh của referral, và mindset cầu tiến.
