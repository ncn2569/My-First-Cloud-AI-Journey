---
title: "Worklog Tuần 7"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Xây dựng SageMaker Pipeline cho Telco Churn: Processing => HPO => Evaluation => Condition => Register.
* Triển khai Data Drift detection với Lambda + S3 Event trigger, tự động chạy lại pipeline.
* Cấu hình Auto-Deploy: EventBridge bắt sự kiện Approved => Lambda Deployer cập nhật Serverless Endpoint.
* Thiết lập Inference API: Lambda Predict Handler + API Gateway POST endpoint.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Viết preprocessing.py: làm sạch dữ liệu, One-Hot Encoding, chia train/val/test <br> - Viết evaluate.py: giải nén model tốt nhất từ HPO, đánh giá AUC <br> - Build Pipeline: ProcessingStep => TuningStep => EvalStep => ConditionStep (AUC ≥ 0.80) => ModelStep (Register) | 13/07/2026 | 14/07/2026 | [SageMaker Processing](https://docs.aws.amazon.com/sagemaker/latest/dg/processing-job.html) |
| 3   | - Viết Lambda DriftChecker: so sánh phân phối thống kê giữa data baseline và data mới <br> - Cấu hình S3 Event Notification: sự kiện PUT => Lambda DriftChecker <br> - **Thực hành:** upload data mới, kiểm tra DriftChecker trigger Pipeline | 15/07/2026 | 15/07/2026 | [S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) |
| 4   | - Viết Lambda Auto-Deployer (TelcoChurnAutoDeployer): tạo EndpointConfig => update Serverless Endpoint <br> - Cấu hình EventBridge Rule: Model Registry Approved event => Lambda Deployer <br> - Cấu hình IAM PassRole + Inline Policy cho Deployer | 16/07/2026 | 16/07/2026 | [EventBridge from SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/automating-sagemaker-with-eventbridge.html) |
| 5   | - Viết Lambda Predict Handler: parse request từ API Gateway => invoke SageMaker Endpoint => trả về prediction <br> - Tạo HTTP API trong API Gateway với Lambda integration <br> - **Thực hành:** POST sample payload, kiểm tra kết quả {"Churn": "Yes", "Probability": 0.87} | 17/07/2026 | 17/07/2026 | [SageMaker Runtime](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_runtime_InvokeEndpoint.html) |
| 6   | - Ôn tập kiến trúc toàn hệ thống <br> - Ghi chép nhật ký công việc | 19/07/2026 | 19/07/2026 | |

### Kết quả đạt được tuần 7:

* Xây dựng thành công SageMaker Pipeline 4 bước: Processing (chuẩn bị dữ liệu) => HPO (tuning XGBoost) => Evaluation (kiểm tra AUC) => Condition/Register. Pipeline tự động approve model khi AUC ≥ 0.80.

* Triển khai Data Drift detection: Lambda DriftChecker so sánh phân phối thống kê của data mới với data baseline. S3 Event Notification trigger DriftChecker, DriftChecker trigger SageMaker Pipeline khi phát hiện drift.

* Triển khai Auto-Deploy: EventBridge bắt sự kiện "Approved" từ Model Registry => Lambda Deployer tự động cập nhật Serverless Endpoint. Đạt zero-touch deployment từ model training đến production.

* Xây dựng Inference API: API Gateway + Lambda Predict Handler => SageMaker Endpoint, trả về JSON prediction.


