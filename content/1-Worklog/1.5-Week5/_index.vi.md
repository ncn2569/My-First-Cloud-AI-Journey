---
title: "Worklog Tuần 5"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Thiết lập SageMaker Studio và làm quen với môi trường.
*  **Cùng nhóm thiết kế kiến trúc MLOps Pipeline và viết Proposal.**
* Tham gia AABW Hackathon (team Six Pillars - khác team AWS).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Thiết lập SageMaker Studio Domain + User Profile <br> - Khám phá giao diện Studio: notebooks, pipelines, models, endpoints | 06/07/2026 | 06/07/2026 | [SageMaker Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/) |
| 3   | - Tạo S3 bucket, tạo cấu trúc thư mục (raw/, processed/, models/) <br> - Upload dataset Telco Churn lên S3 | 07/07/2026 | 07/07/2026 | |
| 4   | - **Cùng nhóm thiết kế kiến trúc MLOps Pipeline hoàn chỉnh** - S3 => Pipeline 4 bước => Model Registry => EventBridge => Lambda Deployer => Serverless Endpoint <br> - **Cùng nhóm viết Proposal** - Problem Statement, Solution Architecture, Timeline | 08/07/2026 | 08/07/2026 | |
| 5   | - SageMaker Pipelines deep dive: ProcessingStep, TuningStep, ConditionStep, ModelStep <br> - SageMaker Model Registry: model groups, versions, approval status | 09/07/2026 | 09/07/2026 | [SageMaker Pipelines](https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html) |
| 6   | - Model Registry + Endpoint configurations <br> - Serverless Endpoint vs Real-time Endpoint <br> - Rà soát IAM Role cho SageMaker execution | 10/07/2026 | 10/07/2026 | |
| 7   | - **AABW Hackathon Day 1 (team Six Pillars):** <br>&emsp; + Xây dựng Adaptive AML/KYC Workflow Engine <br>&emsp; + Sử dụng: Amazon Bedrock, Lambda, DynamoDB, GuardDuty, CloudWatch, Security Hub | 11/07/2026 | 11/07/2026 | [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/) |
| CN   | - **AABW Hackathon Day 2:** <br>&emsp; + Hoàn thiện sản phẩm + pitch demo <br> - Ghi chép nhật ký công việc | 12/07/2026 | 12/07/2026 | |

### Kết quả đạt được tuần 5:

*  **Cùng nhóm thiết kế xong kiến trúc MLOps Pipeline hoàn chỉnh và viết Proposal đầy đủ với Problem Statement, Architecture Diagram, Timeline, Budget và Risk Assessment.**

* Thiết lập SageMaker Studio và làm quen toàn bộ các thành phần: notebooks, pipelines, models, endpoints.

* Tạo xong S3 bucket với cấu trúc thư mục phù hợp cho pipeline.

* Nắm vững SageMaker Pipeline: ProcessingStep, TuningStep, ConditionStep, ModelStep và quản lý phiên bản model.

* Thi AABW Hackathon - xây dựng Adaptive AML/KYC engine với Bedrock; lần đầu làm việc với Agentic AI, hiểu sự khác biệt giữa "LLM chatbot" và "autonomous agent dùng tools."
