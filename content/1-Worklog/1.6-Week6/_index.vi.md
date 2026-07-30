---
title: "Worklog Tuần 6"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Làm quen với Amazon SageMaker và MLOps: Studio, Processing/Training Jobs, Hyperparameter Tuning, Pipelines, Model Registry.
* Viết Proposal cho hệ thống MLOps Platform dự đoán Telco Customer Churn.
* Tham gia AABW Hackathon - ứng dụng Agentic AI trên AWS (Bedrock, Lambda, DynamoDB).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Tổng quan MLOps: Data => Train => Evaluate => Deploy => Monitor <br> - SageMaker: Studio, Processing Jobs, Training Jobs, HPO <br> - Thiết lập SageMaker Studio Domain + User Profile | 06/07/2026 | 06/07/2026 | [SageMaker Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/) |
| 3   | - SageMaker Pipelines: ProcessingStep, TuningStep, ConditionStep, ModelStep <br> - SageMaker Model Registry: model groups, versions, approval status <br> - Nghiên cứu dataset Telco Customer Churn | 07/07/2026 | 07/07/2026 | [SageMaker Pipelines](https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html) |
| 4   | - Viết Proposal: Problem Statement, Solution Architecture <br> - Kiến trúc: S3 => Pipeline 4 bước => Model Registry => EventBridge => Lambda Deployer => Serverless Endpoint | 08/07/2026 | 08/07/2026 | |
| 5   | - Hoàn thiện Proposal: Timeline, Budget Estimation, Risk Assessment <br> - Vẽ sơ đồ kiến trúc thể hiện toàn bộ dịch vụ AWS trong hệ thống | 09/07/2026 | 09/07/2026 | |
| 6   | - **AABW Hackathon (10–12/07):** <br>&emsp; + Tham gia đội Six Pillars <br>&emsp; + Xây dựng Adaptive AML/KYC Workflow Engine <br>&emsp; + Sử dụng: Amazon Bedrock, Lambda, DynamoDB, GuardDuty, CloudWatch, Security Hub | 10/07/2026 | 12/07/2026 | [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/) |
| 7   | - Ghi chép nhật ký công việc | 12/07/2026 | 12/07/2026 | |

### Kết quả đạt được tuần 6:

* Hiểu rõ quy trình MLOps End-to-End: từ data ingestion => preprocessing => training => evaluation => model registry => deployment => monitoring.

* Nắm vững các thành phần SageMaker: Studio (IDE tích hợp), Processing Jobs, Training Jobs, Hyperparameter Tuning, Pipelines (tự động hóa), và Model Registry (quản lý phiên bản model).

* Hoàn thành Proposal MLOps Platform với đầy đủ: Problem Statement, Solution Architecture (8 dịch vụ AWS), Timeline 3 tuần, Budget, Risk Assessment.

* Thi AABW Hackathon - xây dựng Adaptive AML/KYC engine với Bedrock; lần đầu làm việc với Agentic AI, hiểu sự khác biệt giữa "LLM chatbot" và "autonomous agent dùng tools."
