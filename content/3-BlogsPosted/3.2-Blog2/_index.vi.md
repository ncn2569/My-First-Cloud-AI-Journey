---
title: "Blog 2"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# BẢO MẬT TRONG PHÁT TRIỂN PHẦN MỀM TRÊN AWS — NHỮNG BÀI HỌC THỰC TẾ CỦA CẢ NHÓM

### Lời mở đầu

Trong suốt quá trình học AWS, cả nhóm bọn mình nhận ra một điều rất thật: khi bắt tay vào làm một project, câu hỏi đầu tiên luôn là **"làm sao để chạy được?"**. Nhưng càng đi sâu, bọn mình càng thấy câu hỏi quan trọng hơn lại là **"liệu nó có an toàn không?"**

Một ứng dụng có thể chạy rất mượt về mặt chức năng, nhưng chỉ cần một cấu hình sai, một cặp key bị lộ, hay một security group mở quá rộng — hậu quả có thể rất nghiêm trọng. AWS không chỉ cung cấp hạ tầng để deploy, mà còn có cả một hệ sinh thái dịch vụ bảo mật được xây dựng để dùng **ngay từ đầu**, chứ không phải đến lúc xảy ra sự cố mới loay hoay đi vá.

Dưới đây là những bài học thực tế mà cả nhóm đã cùng nhau đúc kết sau khi vừa học, vừa làm, và vừa... mắc lỗi.

---

### 1. Tuyệt đối không hardcode Access Key — bài học từ những "tai nạn" có thật

Đây là lỗi mà hầu như ai mới làm cloud cũng từng dính ít nhất một lần. Cả nhóm bọn mình cũng không ngoại lệ.

Hồi mới bắt đầu, để test nhanh, một bạn trong nhóm đã viết thẳng Access Key và Secret Key vào file Python như thế này:

```
AWS_ACCESS_KEY = "AKIAxxxxxxxxxxxx"
AWS_SECRET_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

Định bụng "tí nữa xóa sau", nhưng rồi quên mất. May mắn là repo để private nên không ai lấy được. Nhưng sau khi tìm hiểu thêm, cả nhóm mới biết chuyện này nghiêm trọng đến mức nào. Trên thực tế, có vô số trường hợp tài khoản AWS bị chiếm quyền chỉ vì vô tình push access key lên GitHub public. Hacker dùng key đó để đào coin, spin hàng trăm EC2 instance — có người nhận bill **hàng nghìn USD chỉ sau vài giờ**.

Bài học nhóm rút ra: **tuyệt đối không để credential trong code**. Thay vào đó:

| Cách làm | Mô tả |
|----------|-------|
| **IAM Role** | Gán role trực tiếp cho EC2/Lambda, SDK tự động lấy credential. Không cần Access Key. |
| **AWS Secrets Manager** | Lưu credential nhạy cảm, rotate tự động, tích hợp với RDS, Lambda dễ dàng. |
| **AWS Systems Manager Parameter Store** | Lưu config & secret đơn giản, chi phí cực thấp, phù hợp cho non-sensitive config. |
| **Environment Variables** | Chỉ nên dùng cho config không nhạy cảm. Nếu bắt buộc phải dùng cho secret thì cần mã hóa KMS. |

Điểm mấu chốt không phải là "dùng service nào", mà là **tư duy tách biệt code và credential ngay từ đầu**. Một khi đã hình thành thói quen này, nguy cơ lộ key giảm đi rất nhiều.

---

### 2. Least Privilege — cấp đúng quyền, không cấp thừa

Đây là nguyên tắc mà cả nhóm nghe đi nghe lại nhiều nhất khi học IAM, và cũng là nguyên tắc mà bọn mình thấy **dễ bị bỏ qua nhất** khi làm vội.

Tình huống cụ thể: một EC2 instance chỉ cần đọc ảnh từ một S3 bucket duy nhất để hiển thị lên web. Phản xạ nhanh thường là: "gắn luôn policy **AmazonS3FullAccess** cho nhanh". Nhưng làm vậy nghĩa là nếu EC2 đó bị chiếm quyền, attacker có thể đọc, ghi, xóa **toàn bộ bucket trong account**.

Thay vào đó, chỉ cần một policy tối giản như thế này:

```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-images-bucket/*"
}
```

Cả nhóm đã có một buổi ngồi review tất cả các IAM policies đang dùng trong project và phát hiện khá nhiều chỗ bị "over-permission". Việc kiểm tra định kỳ bằng **IAM Access Analyzer** và **Credential Report** giúp phát hiện những policy quá rộng mà mình không để ý.

Nguyên tắc nhóm ghi nhớ: **"Nếu không chắc chắn cần quyền gì, hãy bắt đầu từ chối hết, rồi mở dần từng quyền một khi cần."**

---

### 3. Không phải tài nguyên nào cũng nên public

Một sai lầm khá phổ biến mà cả nhóm từng thấy (và suýt mắc phải lúc mới thiết kế kiến trúc) là đưa hết mọi thứ vào Public Subnet — kiểu Internet => Backend => Database, tất cả đều public IP hết.

Hậu quả thế nào? Nếu database có public IP, dù đã đặt password mạnh, nó vẫn là một điểm có thể bị dò quét từ Internet. Chưa kể nếu security group lỡ mở port 3306 (MySQL) hoặc 5432 (PostgreSQL) ra 0.0.0.0/0 — coi như "mở cửa mời vào."

Kiến trúc mà cả nhóm thấy hợp lý và áp dụng vào project của mình:

```
Internet => Application Load Balancer (Public Subnet)
         => Backend EC2/Lambda (Public Subnet)
         => Database RDS (Private Subnet — KHÔNG có public IP)
```

Database nằm trong Private Subnet, chỉ cho phép backend truy cập qua security group rule cụ thể. Không có Internet Gateway route đến Private Subnet, không có cách nào từ bên ngoài "nhìn thấy" database. Đây là mô hình được nhắc đến rất nhiều trong **AWS Well-Architected Framework** — và cả nhóm thấy nó thực sự hiệu quả khi áp dụng.

---

### 4. AWS WAF — tấm khiên trước các cuộc tấn công web

Ngay cả khi backend code đã được viết cẩn thận, ứng dụng vẫn có thể bị tấn công ở tầng HTTP request — SQL Injection, Cross-Site Scripting (XSS), bot tự động spam, hay DDoS tầng ứng dụng.

**AWS WAF (Web Application Firewall)** là service mà cả nhóm thấy khá "underrated" — nhiều người biết đến nhưng ít người dùng, một phần vì tưởng nó phức tạp. Thực ra WAF hoạt động khá trực quan:

- Định nghĩa **Web ACL** — tập hợp các rule lọc request.
- Mỗi rule kiểm tra một điều kiện: IP có trong danh sách đen không? Request có chứa SQL injection pattern không? Số lượng request từ một IP có vượt ngưỡng không?
- Nếu vi phạm, request bị block **trước khi đến được ứng dụng**.

Cả nhóm đã thử setup một Web ACL đơn giản với 3 rule:
1. **AWS Managed Rule - SQL Database** — chặn SQL injection patterns.
2. **Rate-based Rule** — giới hạn 100 request/phút từ mỗi IP.
3. **IP Set Rule** — block các IP đã bị flag từ GuardDuty.

Kết quả: ứng dụng vừa giảm tải (bot không còn spam được), vừa an toàn hơn trước các request độc hại. Một công cụ nhỏ nhưng hiệu quả lớn.

---

### 5. Hệ thống đã chạy — làm sao biết có dấu hiệu bị tấn công?

Bảo mật không kết thúc ở bước cấu hình. Sau khi deploy, câu hỏi tiếp theo là: **"Làm sao để biết hệ thống đang bị tấn công?"** Cả nhóm đã dành thời gian tìm hiểu ba service chính của AWS cho vấn đề này:

#### Amazon GuardDuty

GuardDuty phân tích liên tục ba nguồn dữ liệu: **CloudTrail logs** (hành vi API), **VPC Flow Logs** (lưu lượng mạng), và **DNS logs**. Điểm mạnh là nó dùng machine learning + threat intelligence để phát hiện bất thường mà không cần cấu hình gì. Một số pattern nó phát hiện được:

- Đăng nhập từ vị trí địa lý bất thường (ví dụ: account đang xài ở Vietnam, tự nhiên có người login từ Nga).
- EC2 instance bất ngờ đẩy lượng lớn data ra ngoài (dấu hiệu data exfiltration).
- Gọi API với pattern giống bot — tần suất cao, lặp đi lặp lại cùng một hành động.
- Truy cập từ IP đã có trong danh sách threat intelligence toàn cầu.

Cái hay là GuardDuty tự động generate finding ra console, không cần ngồi lọc hàng triệu dòng log thủ công.

#### Amazon Inspector

Trong khi GuardDuty tập trung vào hành vi bất thường, Inspector giải quyết bài toán lỗ hổng nội tại — một ứng dụng chạy bình thường vẫn có thể dính CVE. Inspector tự động quét:

- **EC2 instances**: package nào hết hạn support, còn thiếu security patch nào?
- **Container images (ECR)**: image có chứa thư viện dính critical CVE không?
- **Lambda functions**: dependency trong function code có lỗ hổng nào không?

Rất hữu ích cho các hệ thống dùng Docker hoặc microservice, nơi số lượng dependency có thể lên đến hàng trăm mà developer khó theo dõi hết.

#### AWS Security Hub

Khi dùng nhiều dịch vụ bảo mật cùng lúc, vấn đề là mỗi service có một dashboard riêng, muốn xem tổng quan phải mở 3-4 tab. Security Hub giải quyết đúng điểm này: nó **tổng hợp finding** từ GuardDuty, Inspector, IAM Access Analyzer, AWS Config, Macie và hiển thị trên một dashboard duy nhất, kèm severity score theo chuẩn **AWS Security Finding Format (ASFF)**.

Cả nhóm thấy Security Hub rất phù hợp với production environment, nơi cần một cái nhìn tổng quan nhanh thay vì phải check từng service.

---

### 6. Hai tình huống "đời thường" nhưng dễ mắc phải

Ngoài các nguyên tắc bảo mật thuần túy, cả nhóm còn gặp hai vấn đề thực tế mà nếu không để ý thì ảnh hưởng khá lớn đến trải nghiệm người dùng:

**Server chậm khi đông người truy cập:** Website của nhóm chạy ngon lành với vài chục người test, nhưng đến ngày demo trước hội đồng, gần 100 người cùng truy cập — server quá tải ngay. CPU EC2 vọt lên 100%, request timeout liên tục. Giải pháp: kết hợp **EC2 Auto Scaling** (tự động thêm instance khi CPU > 70%) và **Application Load Balancer** (phân phối request đều). Sau khi setup, hệ thống chịu được lượng truy cập gấp 3-4 lần bình thường mà vẫn mượt.

**Mất dữ liệu khi thay server:** Một bạn trong nhóm đã lưu toàn bộ ảnh upload vào thư mục `uploads/` ngay trên EC2. Khi cần thay instance mới (vì instance cũ bị lỗi), toàn bộ ảnh biến mất — chưa kịp backup. Sau sự cố, cả nhóm chuyển sang dùng **S3** để lưu file tĩnh và **EFS** cho shared storage giữa các EC2 instance. Tách biệt storage với compute — một bài học cơ bản nhưng phải trả giá mới nhớ.

---

### 7. Điều cả nhóm đúc kết được

Sau tất cả, điều lớn nhất bọn mình nhận ra là: **bảo mật không phải là một "tính năng" để thêm vào cuối dự án**. Nó cần là một phần của quá trình thiết kế kiến trúc ngay từ ngày đầu. Phần lớn sự cố bảo mật không đến từ code sai, mà đến từ **cách hệ thống được cấu hình và vận hành** — một security group mở quá rộng, một IAM policy quá hào phóng, một cặp key bị bỏ quên.

Những nguyên tắc cả nhóm sẽ mang theo vào các dự án sau này:

- Tách bạch code và credential — dùng IAM Role, Secrets Manager.
- Áp dụng Least Privilege triệt để — review policy định kỳ.
- Phân tách rạch ròi public/private subnet — không để database lộ ra Internet.
- Dùng WAF như một lớp bảo vệ mặc định cho mọi web application.
- Giám sát liên tục với GuardDuty + Inspector + Security Hub — không đợi sự cố mới kiểm tra.
- Tách storage khỏi compute — S3/EFS cho dữ liệu, EC2/Lambda cho xử lý.

Với các dự án học tập, không nhất thiết phải bật hết tất cả các service trên. Nhưng **hiểu tại sao chúng tồn tại và bài toán chúng giải quyết** sẽ giúp tụi mình xây dựng tư duy thiết kế hệ thống an toàn và chuyên nghiệp hơn khi bước vào môi trường thực tế.

---

**Nhóm tác giả:** Thành Nhân, Nguyễn Bá Nam, Nam Phan, Nguyễn Trọng Nhân, Nguyễn Cảnh Nguyên

**Link Blog:** [Security in Software Development on AWS](https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2228803837884576&notif_id=1785383944402087&notif_t=feedback_reaction_generic_tagged)


**Tài liệu tham khảo:**
- [IAM Best Practices — AWS Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Security Pillar — AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/)
- [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/)
- [Amazon GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/)
- [Amazon Inspector — Automated Vulnerability Management](https://docs.aws.amazon.com/inspector/latest/user/)
- [AWS Security Hub User Guide](https://docs.aws.amazon.com/securityhub/latest/userguide/)
- [AWS Security Best Practices Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/aws-security-best-practices/)