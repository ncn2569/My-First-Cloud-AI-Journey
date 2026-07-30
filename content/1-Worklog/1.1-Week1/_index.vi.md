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
* Tham dự FCAJ Meetup #1.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
| --- | --------- | ------------ | --------------- | --------------- |
| 2   | - Gặp gỡ team admin và các thành viên FCAJ <br> - Đọc và nắm các nội quy, quy định tại đơn vị thực tập | 01/06/2026 | 01/06/2026 | |
| 3   | - Tìm hiểu tổng quan AWS Cloud: <br>&emsp; + Region, AZ, Edge Location <br>&emsp; + Shared Responsibility Model <br>&emsp; + Các nhóm dịch vụ: Compute, Storage, Database, Networking, Security, Analytics, ML | 02/06/2026 | 02/06/2026 | [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/) |
| 4   | - Tạo AWS Free Tier account <br> - Làm quen AWS Management Console <br> - Cài đặt và cấu hình AWS CLI <br> - **Thực hành:** tạo IAM User, cấu hình Access Key, chạy lệnh CLI cơ bản | 03/06/2026 | 03/06/2026 | [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/) |
| 5   | - Tìm hiểu EC2: <br>&emsp; + Instance types (t, m, c, r, i families) <br>&emsp; + AMI, EBS volumes, Key Pairs <br>&emsp; + Security Groups cơ bản <br> - Các phương thức kết nối SSH vào EC2 <br> - **Thực hành:** launch EC2, SSH, cài Apache | 04/06/2026 | 04/06/2026 | [EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/) |
| 6   | - **Tham dự FCAJ Meetup #1 (06/06/2026):** <br>&emsp; + AWS WebSocket Real-time Game <br>&emsp; + Docker Basics <br>&emsp; + GraphRAG với Amazon Bedrock <br>&emsp; + AWS WAF & ML-based NIDS <br>&emsp; + Hành trình IT Helpdesk => Senior Sysadmin | 06/06/2026 | 06/06/2026 | AWS Study Group Community |
| 7   | - Viết recap Event 1 <br> - Ghi chép nhật ký công việc | 07/06/2026 | 07/06/2026 | |

### Kết quả đạt được tuần 1:

* Nắm được tổng quan AWS Cloud: Region, AZ, Edge Location, Shared Responsibility Model, và 7 nhóm dịch vụ chính.

* Tạo và kích hoạt thành công tài khoản AWS Free Tier.

* Sử dụng thành thạo AWS Management Console: tìm, truy cập và cấu hình dịch vụ từ giao diện web.

* Cài đặt AWS CLI, cấu hình Access Key/Secret Key, default region, output format. Thực hiện được các lệnh: aws sts get-caller-identity, aws ec2 describe-regions, aws ec2 describe-instances.

* Hiểu các EC2 Instance families và biết chọn instance phù hợp workload. Launch thành công EC2 đầu tiên với Apache web server.

* Tham dự FCAJ Meetup #1 - mở rộng hiểu biết về WebSocket, Docker, GraphRAG, WAF, NIDS và câu chuyện nghề thực tế.
