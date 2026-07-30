---
title: "Worklog Tuần 1"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Kết nối, làm quen với team admin và các thành viên trong First Cloud AI Journey.
* Hiểu tổng quan về AWS Cloud, các nhóm dịch vụ và mô hình Shared Responsibility.
* Làm quen với giao diện AWS Management Console, cài đặt và sử dụng AWS CLI.
* Tìm hiểu EC2 và triển khai máy chủ ảo đầu tiên.
* Tham dự FCAJ Meetup #1 (trước khi chương trình bắt đầu) và FCAJ Meetup (13/06).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| *Trước | **Tham dự FCAJ Meetup #1 (06/06/2026):** <br>&emsp; + AWS WebSocket Real-time Game <br>&emsp; + Docker Basics <br>&emsp; + GraphRAG với Amazon Bedrock <br>&emsp; + AWS WAF & ML-based NIDS <br>&emsp; + Hành trình IT Helpdesk => Senior Sysadmin | 06/06/2026 | 06/06/2026 | AWS Study Group Community |
| 2   | - Gặp gỡ team admin và các thành viên FCAJ <br> - Đọc và nắm các nội quy, quy định tại đơn vị thực tập | 08/06/2026 | 08/06/2026 | |
| 3   | - Tìm hiểu tổng quan AWS Cloud: <br>&emsp; + Region, AZ, Edge Location <br>&emsp; + Shared Responsibility Model <br>&emsp; + Các nhóm dịch vụ: Compute, Storage, Database, Networking, Security, Analytics, ML | 09/06/2026 | 09/06/2026 | [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/) |
| 4   | - Tạo AWS Free Tier account <br> - Làm quen AWS Management Console <br> - Cài đặt và cấu hình AWS CLI <br> - **Thực hành:** tạo IAM User, cấu hình Access Key, chạy lệnh CLI cơ bản | 10/06/2026 | 10/06/2026 | [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/) |
| 5   | - Tìm hiểu EC2: <br>&emsp; + Instance types (t, m, c, r, i families) <br>&emsp; + AMI, EBS volumes, Key Pairs <br>&emsp; + Security Groups cơ bản <br> - Các phương thức kết nối SSH vào EC2 <br> - **Thực hành:** launch EC2, SSH, cài Apache | 11/06/2026 | 11/06/2026 | [EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/) |
| 6   | - Thực hành thêm EC2: test Security Group rules, snapshot EBS <br> - Ôn lại kiến thức EC2 tuần 1 | 12/06/2026 | 12/06/2026 | |
| 7   | - **Tham dự FCAJ Meetup (13/06/2026):** <br>&emsp; + URL Shortener trên AWS cho người mới <br>&emsp; + Vai trò chiến lược của Data Engineer (vượt ra ngoài làm dashboard) <br>&emsp; + Tầm quan trọng của Culture Fit trong tuyển dụng <br>&emsp; + Quy trình làm việc dưới góc nhìn của một DevOps Engineer | 13/06/2026 | 13/06/2026 | AWS Study Group Community |
| CN  | - Viết recap Event 1 & Event 2 <br> - Ghi chép nhật ký công việc | 14/06/2026 | 14/06/2026 | |

### Kết quả đạt được tuần 1:

* Nắm được tổng quan AWS Cloud: Region, AZ, Edge Location, Shared Responsibility Model, và 7 nhóm dịch vụ chính.

* Tạo và kích hoạt thành công tài khoản AWS Free Tier.

* Sử dụng thành thạo AWS Management Console: tìm, truy cập và cấu hình dịch vụ từ giao diện web.

* Cài đặt AWS CLI, cấu hình Access Key/Secret Key, default region, output format. Thực hiện được các lệnh: aws sts get-caller-identity, aws ec2 describe-regions, aws ec2 describe-instances.

* Hiểu các EC2 Instance families và biết chọn instance phù hợp workload. Launch thành công EC2 đầu tiên với Apache web server.

* Tham dự 2 sự kiện cộng đồng: FCAJ Meetup #1 (06/06, trước khi chương trình bắt đầu) mở rộng hiểu biết về WebSocket, Docker, GraphRAG, WAF, NIDS; và FCAJ Meetup (13/06) giúp thấy rõ vai trò Data Engineer, Culture Fit, DevOps workflow.
