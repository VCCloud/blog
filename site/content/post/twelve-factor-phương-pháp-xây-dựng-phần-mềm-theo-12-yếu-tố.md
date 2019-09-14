---
title: Twelve-Factor - Phương pháp xây dựng phần mềm theo 12 yếu tố
date: 2019-09-14T00:04:56.946Z
description: >-
  Trong thời đại mới, phần mềm thường được cung cấp người dùng ở dạng dịch vụ
  Web, gọi là web-app hay Software as a Service. Phương pháp 12 Yếu tố là phương
  pháp để xây dựng các phần mềm dạng SaaS.
image: /img/annotation-2019-09-14-071055.png
tags:
  - Development
---
Twelve-Factor là 1 phương pháp luận cho phát triển phần mềm, nội dung chi tiết các bạn có thể xem ở <https://12factor.net/>, bản dịch tiếng Việt nằm ở <https://code2080.com/12-factor-p1/> và <https://code2080.com/12-factor-p2>, bài viết này chỉ lược lại các ý chính và vấn đề rút ra từ việc áp dụng ở VCCloud.

Phương pháp này được đưa ra để nhằm mục đích:

* Giảm thiểu tối đa thời gian và công sức khi có nhân sự mới tham gia vào phát triển sản phẩm
* Tăng tính linh động và đồng nhất giữa các môi trường cài đặt (Production, Staging, Testing...)
* Phần mềm đáp ứng tốt cho việc triển khai trên môi trường Cloud (Cloud native app), và mới hơn là Container
* Phần mềm đáp ứng tốt cho quy trình CI/CD.
* Mang lại cho phần mềm khả năng mở rộng linh hoạt.
