---
title: "Các bài blogs đã đăng"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Trong suốt thời gian thực tập tại FCAJ, nhóm chúng tôi đã cùng nhau nghiên cứu, thảo luận và viết 2 bài blog chuyên sâu chia sẻ kiến thức về AWS lên cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Mỗi bài blog là kết quả của quá trình tìm hiểu thực tế, đúc kết từ những vấn đề chúng tôi gặp phải khi làm việc với các dịch vụ AWS.

---

###  [Blog 1 - BÀI TOÁN CẠN KIỆT KẾT NỐI VỚI RDS PROXY](3.1-Blog1/)

Bài toán **Connection Exhaustion** xảy ra khi kết hợp kiến trúc Serverless (AWS Lambda) với cơ sở dữ liệu quan hệ truyền thống (Amazon RDS). Hàng nghìn hàm Lambda đồng thời mở kết nối khiến RDS bị quá tải và từ chối phục vụ. Blog phân tích chi tiết cơ chế gây lỗi và cách **Amazon RDS Proxy** giải quyết qua 3 tính năng cốt lõi: Multiplexing, Graceful Failover, và IAM Authentication.

> **Ngày đăng:** 20/06/2026 | **Nhóm tác giả:** Thành Nhân, Nguyễn Cảnh Nguyên, Nguyễn Trọng Nhân, Nam Phan, Nguyễn Bá Nam

---

###  [Blog 2 - BẢO MẬT TRONG PHÁT TRIỂN PHẦN MỀM TRÊN AWS](3.2-Blog2/)

Blog tổng hợp 5 bài học bảo mật quan trọng khi phát triển và triển khai ứng dụng trên AWS: không hardcode Access Key, áp dụng nguyên tắc **Least Privilege**, phân tách Public/Private Subnet, bảo vệ ứng dụng với **AWS WAF**, và giám sát liên tục với **GuardDuty, Inspector, Security Hub**. Kèm theo các tình huống thực tế thường gặp như quá tải server và mất dữ liệu khi thay server.

> **Ngày đăng:** 10/07/2026 | **Nhóm tác giả:** Thành Nhân, Nguyễn Bá Nam, Nam Phan, Nguyễn Trọng Nhân

---

{{% notice info %}}
Cả 2 bài blog đều được đăng tải trên group [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) — nơi cộng đồng cùng nhau chia sẻ và học hỏi kiến thức về AWS Cloud.
{{% /notice %}}