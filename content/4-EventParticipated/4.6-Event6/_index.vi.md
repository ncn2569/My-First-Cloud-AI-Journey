---
title: "Event 6"
date: 2026-07-01
weight: 6
chapter: false
pre: " <b> 4.6. </b> "
---

# Bài Thu Hoạch: FCAJ Community Day – AABW Hackathon Showcase

**Thời gian:** 25 Tháng 7, 2026
**Địa điểm:** Tầng 26, tòa nhà Bitexco, số 02 đường Hải Triều, phường Sài Gòn, TP. Hồ Chí Minh
**Hình thức:** Showcase & Chia sẻ trực tiếp
**Tổ chức:** Cộng đồng First Cloud & AI Journey (FCAJ)

---

### Mục Tiêu Sự Kiện

- Tổng kết và trình bày kết quả các dự án được xây dựng trong cuộc thi hackathon **Agentic AI Build Week (AABW)**
- Tạo cơ hội để các đội chia sẻ hành trình, thử thách và bài học từ quá trình thi đấu
- Truyền cảm hứng cho cộng đồng FCAJ về việc ứng dụng Agentic AI vào các bài toán thực tế

---

### Các Đội Trình Bày

| # | Đội | Sản phẩm | Chủ đề |
|---|-----|----------|--------|
| 1 | **Six Pillars** *(đội của tôi)* | Adaptive AML/KYC Workflow Engine | Tự động hóa điều tra chống rửa tiền bằng Agentic AI |
| 2 | **3KA** | Crowd Management System | Quản lý đám đông thời gian thực bằng Computer Vision & AI |
| 3 | **Plan V** | SA Professional Native App | AI tool hỗ trợ Solution Architect thiết kế kiến trúc AWS |
| 4 | **SignalScout** | SignalScout Platform | Phân tích tín hiệu chiến lược doanh nghiệp bằng AI |
| 5 | **One Team** | AI-Powered Conversation Ordering | Hệ thống đặt hàng thông minh bằng hội thoại AI |

---

### Nội Dung Chính

#### Phần 1 – Six Pillars: Adaptive AML/KYC Workflow Engine
*Trình bày bởi nhóm Six Pillars (Bùi Hoàng Việt, Nguyễn Lâm Anh, Nguyễn Văn Linh, Nguyễn Cảnh Nguyên, Nguyễn Minh Nhật, Trần Phương Huyền)*

- **Bài toán:** Quy trình điều tra AML truyền thống tốn khoảng ~3 giờ/case, đòi hỏi kiểm tra thủ công KYC (~15 phút), phân tích giao dịch bằng SQL (~17 phút), xây dựng báo cáo (~25–60 phút) và QC (~60 phút).
- **Giải pháp:** Xây dựng hệ thống Agentic AI 3 tầng (Fast Detection => Agentic Investigation => Case Management) tự động hóa toàn bộ quá trình thu thập và làm giàu dữ liệu điều tra, chỉ giữ lại bước cuối cùng cho con người review.
- **Kiến trúc AWS:** Sử dụng Amazon Bedrock, AWS Lambda, DynamoDB, KMS, IAM, GuardDuty, CloudWatch, và Security Hub để đảm bảo bảo mật cấp enterprise.
- **Kết quả:** Hệ thống có thể rút ngắn thời gian xử lý từ ~3 giờ/case xuống còn vài phút, đồng thời đảm bảo tính minh bạch và tuân thủ pháp lý (legally compliant reports).
- **Key Takeaways từ hành trình hackathon:** *Scope Over Scale, Execution is Teamwork, Nothing to Lose Mindset.*

---

#### Phần 2 – 3KA: Crowd Management System
*Quản lý đám đông thời gian thực*

- Sử dụng **Computer Vision** kết hợp **Object Tracking** để phát hiện và theo dõi người trong thời gian thực.
- Tích hợp **Agentic AI** với hai vai trò: *Autonomous Monitor* (tự động phát hiện tắc nghẽn và cảnh báo sớm) và *Operator Copilot* (cho phép nhân viên đặt câu hỏi bằng ngôn ngữ tự nhiên và nhận phản hồi dựa trên dữ liệu thực).
- Thách thức lớn: Duy trì video stream ổn định, giảm độ trễ inference và đảm bảo tracking nhất quán giữa các frame.
- Lessons Learned: Kết hợp real-time computer vision, cloud inference và AI agentic trong một hệ thống vận hành là bài toán cực kỳ phức tạp.

---

#### Phần 3 – Plan V: SA Professional Native App
*AI tool hỗ trợ Solution Architect*

- **Bài toán:** Solution Architect phải đọc BRD/PRD thủ công, bắt đầu từ trang trắng mỗi lần và ước tính chi phí theo kinh nghiệm cá nhân.
- **Giải pháp:** Ứng dụng AI phân tích yêu cầu bằng ngôn ngữ tự nhiên, tự động tạo sơ đồ kiến trúc AWS (Drawio, AWS Icons), ước tính chi phí cho region ap-southeast-1, và cho phép tinh chỉnh qua chat sidebar.
- **Tác động:** Từ việc đọc tài liệu thủ công => Upload + chat tự nhiên để có Requirements Catalogue trong vài phút; Từ bắt đầu từ trang trắng => Có kiến trúc draft ngay lập tức để phản hồi và điều chỉnh.

---

#### Phần 4 – One Team: AI-Powered Conversation Ordering
*Hệ thống đặt hàng thông minh bằng hội thoại AI*

- **Bài toán:** Quy trình đặt hàng truyền thống yêu cầu người dùng phải điều hướng qua nhiều bước, menu phức tạp - gây ra trải nghiệm không tự nhiên và tốn thời gian.
- **Giải pháp:** Xây dựng hệ thống cho phép người dùng đặt hàng thông qua hội thoại ngôn ngữ tự nhiên với AI, loại bỏ hoàn toàn sự cần thiết phải dùng UI truyền thống.
- **Kiến trúc:** Hệ thống được thiết kế theo hướng microservices, giải quyết các thách thức về service discovery, observability và CI/CD cho các lần release thường xuyên.
- **Bài học:** Chuyển đổi từ monolithic sang microservices cho phép từng service được deploy và scale độc lập, giảm sự phụ thuộc giữa các team và tăng tốc độ phát triển.

---

#### Phần 5 – SignalScout: Enterprise Strategic Signal Intelligence
*Nền tảng phân tích tín hiệu chiến lược doanh nghiệp*

- **Bài toán:** Các team chiến lược doanh nghiệp cần phát hiện sớm các thay đổi chiến lược từ đối thủ cạnh tranh nhưng dữ liệu bị phân tán và thiếu công cụ phân tích tự động.
- **Giải pháp:** Nền tảng tự động thu thập và phân tích tín hiệu từ nhiều nguồn dữ liệu doanh nghiệp, kết nối các tín hiệu phân tán thành một câu chuyện rõ ràng có bằng chứng, hỗ trợ các quyết định Maintain/Adapt/Accelerate.
- **Kiến trúc:** Sử dụng AWS Bedrock, AgentCore Runtime, DynamoDB, Amplify, Lambda, API Gateway, Cognito, CloudTrail, v.v. Tổng chi phí AWS ước tính từ ~$17–$130/tháng tùy quy mô.

---

### Những Gì Học Được

#### Kỹ Thuật & Kiến Trúc

- **Agentic AI là tương lai thực sự gần:** Cả 4 sản phẩm đều xây dựng xung quanh các hệ thống AI tự chủ, không chỉ là chatbot hay AI đơn giản, mà là các agent có khả năng lập kế hoạch, sử dụng công cụ và thực hiện nhiều bước để giải quyết bài toán phức tạp.
- **Kiến trúc AWS phục vụ thực tế là rất khác với học thuật:** Mỗi đội đều phải đưa ra các quyết định kiến trúc thực tế: chọn dịch vụ nào, trade-off giữa chi phí và hiệu năng, đảm bảo bảo mật và khả năng mở rộng.
- **"Scope it tiny - done well":** Bài học xuyên suốt từ tất cả các đội là thà làm một feature nhỏ thật tốt còn hơn làm nhiều feature dở dang.

#### Kỹ Năng Mềm & Sự Nghiệp

- **Trình bày trước đám đông là kỹ năng có thể rèn luyện:** Lần đầu đứng chia sẻ với tư cách speaker, cảm giác căng thẳng là thật, nhưng vượt qua được nó mang lại sự tự tin thực sự.
- **Hackathon không chỉ là cuộc thi kỹ thuật:** Đó là môi trường học tập nén, nơi bạn học cách làm việc nhóm dưới áp lực, ra quyết định nhanh, và xây dựng sản phẩm có thể demo được trong thời gian rất ngắn.

---

### Cảm Nhận Sự Kiện

Đây là sự kiện đặc biệt nhất trong suốt quá trình thực tập của tôi - không phải vì tôi được nghe chia sẻ, mà vì lần đầu tiên tôi là **người chia sẻ**.

Đứng trên góc độ speaker để kể lại hành trình hackathon của nhóm Six Pillars là một trải nghiệm hoàn toàn khác. Tôi phải tổ chức câu chuyện, chuẩn bị nội dung và truyền đạt nó một cách rõ ràng trước một cộng đồng thực sự - không phải bài tập giả định trong lớp học. Cảm giác căng thẳng trước khi bắt đầu là thật, nhưng khi thực sự nói, mọi thứ dần chảy tự nhiên hơn. Đó là khoảnh khắc tôi nhận ra rằng *dũng cảm không phải là không sợ - mà là hành động dù sợ*.

Ngoài phần trình bày của đội mình, được nghe ba nhóm khác chia sẻ cũng cực kỳ có giá trị. Mỗi đội có cách tiếp cận khác nhau - từ kiến trúc, công nghệ, đến cách đặt vấn đề - nhưng tất cả đều hội tụ ở một điểm chung: **Agentic AI đang mở ra một kỷ nguyên mới của phần mềm**, nơi các ứng dụng không chỉ phản hồi mà còn chủ động hành động.

#### Hình Ảnh Sự Kiện

![FCAJ Community Day - AABW Showcase](event6pic.png)
![FCAJ Community Day - AABW Showcase](image.jpg)
> Nhìn lại, Event 6 là sự kiện kết tinh nhiều thứ tôi đã học trong suốt kỳ thực tập: kỹ thuật từ các buổi meetup, kinh nghiệm hackathon từ AABW, và kỹ năng giao tiếp từ việc phải đứng trước cộng đồng. Đây không chỉ là điểm kết thúc của một hành trình - mà là điểm khởi đầu của sự tự tin mới.
