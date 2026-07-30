---
title: "Worklog Tuần 6"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Viết script preprocessing và evaluation cho MLOps Pipeline.
* Code Lambda DriftChecker với S3 Event trigger.
*  **Cùng nhóm build SageMaker Pipeline hoàn chỉnh.**

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Ôn lại kết quả hackathon AABW <br> - Viết recap hackathon | 13/07/2026 | 13/07/2026 | |
| 3   | - Viết preprocessing.py: làm sạch dữ liệu, One-Hot Encoding, chia train/val/test <br> - Test preprocessing script trên SageMaker Processing Job | 14/07/2026 | 14/07/2026 | [SageMaker Processing](https://docs.aws.amazon.com/sagemaker/latest/dg/processing-job.html) |
| 4   | - Viết evaluate.py: giải nén model tốt nhất từ HPO, đánh giá AUC <br> - Cấu hình evaluation.json output cho ConditionStep | 15/07/2026 | 15/07/2026 | |
| 5   | - Viết Lambda DriftChecker: so sánh phân phối thống kê giữa data baseline và data mới <br> - Cấu hình S3 Event Notification: sự kiện PUT => Lambda DriftChecker | 16/07/2026 | 16/07/2026 | [S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) |
| 6   | - **Cùng nhóm build SageMaker Pipeline** - ProcessingStep => TuningStep => EvalStep => ConditionStep (AUC >= 0.80) => ModelStep (Register) <br> - Test Pipeline execution | 17/07/2026 | 17/07/2026 | [SageMaker Pipelines](https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html) |
| 7   | - Test toàn bộ Pipeline flow, review code <br> - Ghi chép nhật ký công việc | 18/07/2026 | 18/07/2026 | |

### Kết quả đạt được tuần 6:

*  **Cùng nhóm xây dựng thành công SageMaker Pipeline 4 bước:** Processing (chuẩn bị dữ liệu) => HPO (tuning XGBoost) => Evaluation (kiểm tra AUC) => Condition/Register. Pipeline tự động approve model khi AUC >= 0.80.

* Viết và test xong preprocessing.py và evaluate.py, tích hợp hoàn chỉnh với SageMaker Processing Jobs và Pipeline steps.

* Triển khai nền tảng Data Drift detection: Lambda DriftChecker so sánh phân phối thống kê của data mới với baseline. S3 Event Notification trigger DriftChecker mỗi khi có file mới upload.

* Ôn lại kết quả AABW Hackathon - đúc kết bài học về Agentic AI, làm việc nhóm dưới áp lực.
