---
title: "Blog 1"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# BÀI TOÁN CẠN KIỆT KẾT NỐI KHI KẾT HỢP AWS LAMBDA VỚI RDS — VÀ CÁCH AMAZON RDS PROXY GIẢI QUYẾT

### Lời mở đầu

Trong quá trình học AWS, cả nhóm bọn mình có cơ hội đào sâu vào các dịch vụ database trên cloud — từ RDS, DynamoDB cho đến ElastiCache. Nhưng có một vấn đề khiến cả nhóm tranh luận khá nhiều và cuối cùng phải ngồi lại tìm hiểu cùng nhau: chuyện gì sẽ xảy ra nếu đem mô hình **Serverless** — cụ thể là AWS Lambda — kết hợp với cơ sở dữ liệu quan hệ truyền thống như RDS?

Ở trường, khi học Hệ quản trị Cơ sở dữ liệu, bọn mình được dạy về Connection Pooling như một kỹ thuật tối ưu chuẩn mực. Nhưng khi mang lý thuyết ấy lên môi trường cloud với hàng nghìn hàm Lambda chạy song song, cả nhóm mới tá hỏa nhận ra: mọi thứ không đơn giản như trong giáo trình. Hôm nay, bọn mình muốn chia sẻ lại toàn bộ hành trình tìm hiểu về bài toán **Connection Exhaustion** và cách **Amazon RDS Proxy** giải quyết nó.

---

### 1. Hai triết lý đối lập — mầm mống của thảm họa

Khi cả nhóm bắt đầu phân tích, điều đầu tiên nhận ra là **Lambda và RDS sinh ra từ hai thế giới hoàn toàn khác nhau**:

**AWS Lambda** được thiết kế để scale linh hoạt đến mức gần như không giới hạn. Chỉ cần một đợt traffic tăng đột biến, API Gateway có thể kích hoạt hàng nghìn execution environment chạy cùng một lúc. Mỗi environment là một container riêng biệt, hoàn toàn stateless, và có vòng đời cực kỳ ngắn — đôi khi chỉ tồn tại vài trăm mili giây rồi biến mất.

**Amazon RDS** thì ngược lại. Đây là dịch vụ database quan hệ được quản lý, nhưng bên dưới nó vẫn là một máy chủ PostgreSQL hoặc MySQL truyền thống. Và cũng như mọi RDBMS truyền thống, mỗi connection đến database không hề "miễn phí". Cụ thể với PostgreSQL, mỗi connection mới buộc OS phải fork ra một process riêng, ngốn trung bình khoảng **10MB RAM**. Với một RDS instance db.t3.medium có 4GB RAM, trừ đi buffer pool và OS overhead, số connection tối đa (`max_connections`) thường chỉ loanh quanh vài trăm.

**Kịch bản va chạm mà cả nhóm đã mô phỏng thử:**

> Một đợt khuyến mãi khiến lượng truy cập API tăng gấp 10 lần. API Gateway trigger 2,000 Lambda functions chạy đồng thời. Theo logic mặc định, mỗi function mở một connection thẳng đến RDS. Database chỉ chịu được tối đa 500 connections. Kết quả: RDS lập tức từ chối toàn bộ connection mới với lỗi **"FATAL: remaining connection slots are reserved for non-replication superuser connections"** — ứng dụng sập không kịp trở tay.

Đây không phải lỗi code, mà là **xung đột về mặt triết lý thiết kế** giữa hai service.

---

### 2. Tại sao Connection Pooling truyền thống không cứu được?

Phản xạ đầu tiên của cả nhóm khi đọc đến đây là: "Thế dùng Connection Pool đi, có gì đâu?" Đúng là trong các ứng dụng monolithic truyền thống, thư viện như **pg-pool (Node.js)** hay **HikariCP (Java)** duy trì sẵn một pool các connection mở, dùng đi dùng lại, rất hiệu quả.

Nhưng khi cả nhóm thử áp dụng logic này lên Lambda thì mọi chuyện vỡ ra:

- Mỗi Lambda function chạy trong một **môi trường cô lập hoàn toàn**. Không có shared memory, không có shared state.
- Nếu 2,000 Lambda cùng cold start, bạn sẽ có **2,000 Connection Pool độc lập**, mỗi pool lại mở thêm 5-10 connections riêng.
- Tổng số connections thực tế đến RDS không những không giảm, mà còn **tăng gấp bội**.

Vấn đề không nằm ở bản thân Connection Pooling, mà nằm ở chỗ **connection pool hoạt động ở tầng application** — và Lambda scale ở tầng infrastructure, nằm ngoài tầm kiểm soát của pool. Cả nhóm gọi đùa đây là tình huống "giải pháp đúng, nhưng đặt sai chỗ."

---

### 3. Amazon RDS Proxy — đặt lớp đệm vào đúng chỗ

Sau một hồi đào tài liệu và test thử, cả nhóm phát hiện ra AWS đã lường trước bài toán này từ lâu. Giải pháp là **Amazon RDS Proxy** — một service proxy database được quản lý hoàn toàn, nằm giữa Lambda và RDS. Ý tưởng cốt lõi rất đơn giản: thay vì để hàng nghìn Lambda function nối thẳng vào database, tất cả sẽ đi qua một "người gác cổng" duy nhất.

Bọn mình thấy RDS Proxy giải quyết được ba vấn đề rất đáng giá:

#### 3.1. Connection Pooling tập trung (Multiplexing)

Thay vì mỗi Lambda tự quản lý pool connections riêng, RDS Proxy duy trì một **warm pool duy nhất** các connections thực sự đến RDS. Cơ chế hoạt động cụ thể:

- Lambda A cần query => gửi request đến RDS Proxy.
- Proxy lấy một connection đang rảnh từ warm pool => thực thi query => trả kết quả cho Lambda A => **trả connection về pool**.
- Lambda B, C, D... tiếp tục dùng lại chính những connections đó.

Kỹ thuật này gọi là **connection multiplexing**. Điểm mấu chốt: hàng nghìn Lambda function chỉ cần dùng chung **vài chục connections thực tế** đến RDS. Cả nhóm test thử với 500 Lambda concurrent, RDS Proxy chỉ mở đúng 20 connections đến database mà vẫn phục vụ mượt mà.

#### 3.2. Graceful Failover — không đứt gãy khi database gặp sự cố

Một điểm cộng nữa khiến cả nhóm khá ấn tượng là khả năng xử lý failover. Trong kiến trúc Multi-AZ của RDS, khi primary database gặp sự cố, AWS tự động promote standby lên làm primary mới. Quá trình này thường mất **30-60 giây**, và nếu ứng dụng kết nối thẳng đến database, toàn bộ request trong khoảng thời gian đó sẽ thất bại với lỗi "connection refused".

RDS Proxy xử lý khác: nó **giữ lại các request đang chờ** trong hàng đợi nội bộ, chờ đến khi database mới sẵn sàng rồi tự động route lại. Phía Lambda chỉ thấy API response chậm hơn bình thường một chút, chứ không hề bị lỗi. Một chi tiết nhỏ nhưng cực kỳ quan trọng với production system.

#### 3.3. IAM Authentication — không còn password trong environment variable

Đây là điểm cả nhóm tâm đắc nhất về mặt bảo mật. Thay vì phải nhúng password database dạng plaintext vào environment variable của Lambda (một rủi ro bảo mật rất lớn), RDS Proxy cho phép Lambda xác thực bằng chính **IAM Role** của nó. Cụ thể:

- Lambda gửi request đến RDS Proxy kèm IAM token được generate tự động từ SDK.
- Proxy xác thực token đó qua IAM, rồi **tự mình** dùng credential quản lý trong AWS Secrets Manager để kết nối đến RDS.
- Lambda không bao giờ nhìn thấy database password.

Cả nhóm thấy cách làm này gọn và an toàn hơn hẳn so với việc tự quản lý credential bằng tay, đặc biệt là trong môi trường có hàng chục function cùng truy cập database.

---

### 4. Một chút thực tế — không phải bài toán nào cũng cần RDS Proxy

Sau khi hiểu rõ lợi ích, cả nhóm cũng ngồi lại bàn về câu hỏi ngược lại: **khi nào không cần RDS Proxy?** Vì dù sao đây cũng là một managed service có chi phí (tính theo giờ + số lượng connections), không phải lúc nào cũng cần bật lên.

Qua thảo luận, bọn mình thống nhất một số tình huống không cần thiết:

- Lambda function chỉ chạy vài lần mỗi giờ, không có nguy cơ bùng nổ connections.
- Ứng dụng monolithic chạy trên EC2 với HikariCP/pg-pool truyền thống — vì pool nằm chung một process, không bị phân mảnh như Lambda.
- Backend dùng DynamoDB thay vì RDS — DynamoDB dùng HTTP API, không có khái niệm connection pool.

Đây là bài học quan trọng: **hiểu rõ trade-off trước khi quyết định dùng một service, thay vì cứ thấy hay là bật lên.**

---

### 5. Tổng kết

Qua lần mổ xẻ này, điều khiến cả nhóm tâm đắc nhất không chỉ là biết thêm một service mới, mà là hiểu được **nguyên nhân gốc rễ** của vấn đề — tại sao hai service cùng thuộc AWS nhưng lại xung đột với nhau, và tại sao giải pháp được đặt ở tầng proxy thay vì tầng application. Đó là kiểu tư duy mà cả nhóm nghĩ sẽ còn hữu ích về lâu dài, với bất kỳ hệ thống phân tán nào, không chỉ riêng AWS.

Hi vọng bài viết này giúp ích cho những bạn đang tìm hiểu về kiến trúc Serverless + RDS. Nếu có thắc mắc hay muốn trao đổi thêm, hãy comment bên dưới — cả nhóm sẽ cùng thảo luận với các bạn nhé.

---

**Nhóm tác giả:** Thành Nhân, Nguyễn Cảnh Nguyên, Nguyễn Trọng Nhân, Nam Phan, Nguyễn Bá Nam

**Link Blog:** [Amazon RDS Proxy](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2227947781303515/)


**Tài liệu tham khảo:**
- [Tổng quan về quản lý kết nối với Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/)
- [Sử dụng RDS Proxy với AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/configuration-database.html)
- [Cơ chế Multiplexing & Connection Borrowing trong RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html)
- [So sánh RDS Proxy vs Direct Connection — AWS Database Blog](https://aws.amazon.com/blogs/database/using-amazon-rds-proxy-with-aws-lambda/)