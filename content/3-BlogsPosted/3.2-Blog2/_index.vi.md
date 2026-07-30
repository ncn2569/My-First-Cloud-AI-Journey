---
title: "Blog 2"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# BẢO MẬT TRONG PHÁT TRIỂN PHẦN MỀM — KHÔNG CHỈ LÀ VIẾT CODE AN TOÀN

### 1. Lời mở đầu

Trong quá trình học AWS, cả nhóm nhận ra một điều khá thú vị. Khi mới làm project, hầu hết chúng ta chỉ tập trung vào việc **"làm sao cho ứng dụng chạy được"**. Nhưng một khi ứng dụng được đưa lên Internet, câu hỏi quan trọng hơn nhiều lại là: **làm sao để ứng dụng vẫn an toàn?**

Một ứng dụng có thể chạy rất mượt về mặt chức năng, nhưng chỉ cần một cấu hình sai hoặc một lỗ hổng nhỏ, dữ liệu có thể bị lộ hoặc hệ thống bị tấn công bất cứ lúc nào. AWS không chỉ cho mình hạ tầng để triển khai ứng dụng, mà còn có cả một loạt dịch vụ giúp xây dựng kiến trúc bảo mật ngay từ đầu, chứ không phải chờ đến khi có sự cố mới đi vá.

---

### 2. 5 Bài học Bảo mật Quan trọng trên AWS

#### 2.1. Không nên lưu Access Key trong mã nguồn

Đây là lỗi mà rất nhiều người mới làm cloud từng dính phải. Ví dụ điển hình:

```
AWS_ACCESS_KEY="AKIAxxxxxxxx"
AWS_SECRET_KEY="xxxxxxxxxxxxxxxx"
```

Rồi vô tình push cả project lên GitHub. Nếu repo để Public, bất kỳ ai cũng lấy được cặp key này và dùng luôn tài nguyên AWS của bạn. Trong thực tế đã có không ít trường hợp tài khoản bị lợi dụng để đào tiền mã hóa, khởi tạo hàng trăm EC2 Instance cùng lúc, khiến chi phí phát sinh cực lớn chỉ trong vài giờ.

Thay vì nhét Access Key thẳng vào source code, AWS khuyến khích dùng:

- **IAM Role**
- **Environment Variables**
- **AWS Secrets Manager**
- **AWS Systems Manager Parameter Store**

Đây đều là những cách giúp giảm rủi ro rò rỉ thông tin xác thực so với việc hardcode.

#### 2.2. Nguyên tắc "Least Privilege"

Một khái niệm cả nhóm thấy khá quan trọng khi học IAM: **chỉ cấp đúng quyền cần thiết, không cấp nhiều hơn**.

Ví dụ, một EC2 chỉ cần đọc dữ liệu từ Amazon S3. Thay vì cấp thẳng `AmazonS3FullAccess`, chỉ cần cấp `s3:GetObject` cho đúng bucket cần dùng là đủ. Làm vậy giúp giảm thiểu thiệt hại nếu tài khoản hoặc dịch vụ đó chẳng may bị xâm nhập — và đây cũng là nguyên tắc rất phổ biến trong các hệ thống doanh nghiệp.

#### 2.3. Không phải tài nguyên nào cũng nên mở ra Internet

Một sai lầm khá phổ biến khi triển khai hệ thống là đưa hết mọi dịch vụ vào Public Subnet — kiểu Internet nối thẳng tới Backend, rồi Backend nối thẳng tới Database. Nếu database có IP Public và Security Group cấu hình lỏng lẻo, nguy cơ bị quét cổng hay bị tấn công tăng lên đáng kể.

Kiến trúc an toàn hơn thường tách bạch rõ ràng:

> **Internet → Load Balancer → Backend (Public Subnet) → Database (Private Subnet)**

Database nằm ở Private Subnet, chỉ cho phép Backend truy cập chứ không mở trực tiếp ra ngoài. Đây là kiểu kiến trúc được nhắc đến rất nhiều trong **AWS Well-Architected Framework**.

#### 2.4. Bảo vệ ứng dụng khỏi các cuộc tấn công Web

Ngay cả khi code viết tốt, ứng dụng vẫn có thể bị tấn công bằng những request độc hại — SQL Injection, Cross-Site Scripting (XSS), bot tự động dội hàng nghìn request, hay DDoS ở tầng ứng dụng.

**AWS WAF (Web Application Firewall)** được sinh ra để lọc các request này trước khi chúng chạm tới ứng dụng. WAF có thể:

- Chặn IP đáng ngờ
- Giới hạn số request từ một địa chỉ IP
- Phát hiện các mẫu tấn công phổ biến theo chuẩn OWASP
- Chặn request chứa payload độc hại

Nhờ vậy ứng dụng vừa giảm tải, vừa chống chịu tốt hơn trước các cuộc tấn công đến từ Internet.

#### 2.5. Hệ thống đã chạy rồi, làm sao biết có dấu hiệu bị tấn công?

Bảo mật không dừng lại ở việc cấu hình đúng ngay từ đầu — nó còn cần được **giám sát liên tục**. AWS có khá nhiều dịch vụ hỗ trợ chuyện này:

- **Amazon GuardDuty:** Dựa vào dữ liệu từ AWS CloudTrail, VPC Flow Logs và DNS Logs để phát hiện hành vi bất thường — đăng nhập từ vị trí địa lý lạ, một EC2 đột nhiên đẩy lượng lớn dữ liệu ra ngoài, gọi API theo kiểu giống bot, hoặc truy cập từ IP đã bị đánh dấu là độc hại. Thay vì phải ngồi lọc hàng triệu dòng log, GuardDuty tự động đưa ra cảnh báo để quản trị viên vào điều tra.

- **Amazon Inspector:** Giải quyết một vấn đề khác — một ứng dụng có thể chạy bình thường nhưng vẫn tồn tại lỗ hổng bên trong. Inspector quét EC2 Instance, Container Image, và các thư viện phần mềm để phát hiện package đã hết hạn hỗ trợ, thư viện dính lỗ hổng CVE, hay cấu hình chưa an toàn — rất hữu ích với các hệ thống dùng Docker hoặc chạy theo mô hình microservices.

- **AWS Security Hub:** Đóng vai trò trung tâm tổng hợp khi doanh nghiệp dùng nhiều dịch vụ bảo mật cùng lúc. Nó gom kết quả từ GuardDuty, Inspector, IAM Access Analyzer, AWS Config, Macie lại và hiển thị trên một bảng điều khiển duy nhất, giúp đội vận hành nắm tình trạng bảo mật của cả hệ thống dễ dàng hơn nhiều.

---

### 3. Những vấn đề thường gặp khi triển khai

#### 3.1. Server chậm khi có nhiều người truy cập

Đây không hẳn là lỗi, mà là tình huống rất hay gặp. Một website của nhóm bình thường chỉ có vài chục người vào thì chạy êm ru, nhưng đến ngày bảo vệ đồ án, 200 sinh viên cùng truy cập một lúc thì server quá tải ngay: trang tải rất lâu, API phản hồi chậm, một số request bị timeout.

Kết hợp **Amazon EC2 Auto Scaling** với **Elastic Load Balancer**, hệ thống có thể tự tạo thêm máy chủ khi cần và phân phối yêu cầu đều ra giữa nhiều instance, nhờ đó ứng dụng vẫn giữ được hiệu năng ngay cả khi lượng truy cập tăng đột biến.

#### 3.2. Mất dữ liệu sau khi thay server

Một lỗi khá phổ biến khi mới làm project là lưu toàn bộ hình ảnh hay file upload ngay trên server (kiểu thư mục `uploads/` nằm luôn trong EC2). Vấn đề là nếu phải tạo EC2 mới, hoặc server gặp sự cố, những file này có thể biến mất nếu chưa kịp backup.

Đó là lý do **Amazon S3** thường được dùng để lưu hình ảnh, video, file PDF, bản backup, hay nhật ký hệ thống — còn EC2 chỉ tập trung xử lý logic ứng dụng. Tách riêng nơi lưu trữ dữ liệu và nơi chạy ứng dụng vừa giảm rủi ro mất dữ liệu, vừa dễ mở rộng hơn về sau.

---

### 4. Điều cả nhóm rút ra

Sau khi học AWS và tìm hiểu thêm các giải pháp bảo mật, điều cả nhóm nhận ra là: **bảo mật không phải một tính năng thêm vào sau khi dự án đã xong**, mà cần là một phần của quá trình thiết kế hệ thống ngay từ đầu. Cũng như phần lớn sự cố khi triển khai ứng dụng thường không xuất phát từ việc "code sai", mà đến từ cách hệ thống được cấu hình và vận hành.

Một số nguyên tắc hữu ích để ghi nhớ:

- Không lưu thông tin xác thực trong mã nguồn
- Áp dụng nguyên tắc cấp quyền tối thiểu (Least Privilege)
- Phân tách rõ tài nguyên Public và Private
- Giám sát hệ thống liên tục thay vì chỉ phản ứng khi có sự cố
- Thường xuyên quét lỗ hổng và cập nhật thư viện
- Theo dõi trạng thái hoạt động, ghi log đầy đủ
- Thiết kế hệ thống có khả năng chịu lỗi và có phương án mở rộng khi lượng người dùng tăng

Với các dự án học tập, không phải lúc nào cũng cần triển khai đủ GuardDuty hay Security Hub. Nhưng hiểu vì sao chúng tồn tại, và bài toán mà chúng giải quyết, sẽ giúp cả nhóm hình thành tư duy xây dựng những hệ thống an toàn và chuyên nghiệp hơn khi bước vào các dự án thực tế.

Đó cũng là lý do AWS không chỉ cung cấp dịch vụ tính toán hay lưu trữ, mà còn xây dựng cả một hệ sinh thái hỗ trợ triển khai, giám sát và vận hành ứng dụng trong môi trường thực tế.

---

**Nhóm tác giả:** Thành Nhân, Nguyễn Bá Nam, Nam Phan, Nguyễn Trọng Nhân

**Tài liệu tham khảo:**
- [IAM Best Practices (AWS Docs)](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Well-Architected – Security – IAM](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec-iam.html)
- [AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html)
- [Amazon GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
- [Amazon Inspector](https://aws.amazon.com/inspector/)