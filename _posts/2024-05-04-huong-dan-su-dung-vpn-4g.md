---
layout: post
title:  'Free data với ứng dụng VPN 4G trên Android'
summary: 'Hướng dẫn free data 4G trên android dành cho người nghèo ;))'
author: dieudv
date: '2024-05-04 00:00:00 +0000'
category: 'tricks'
thumbnail: /assets/img/posts/vpn4g.png
keywords: 4g free, termux, socksdroid
usemathjax: true
permalink: /blog/huong-dan-su-dung-vpn-4g/
---

Áp dụng với sim Viettel, Vina thì hơi hên xui tí vì có thể kiểu sáng dùng được chiều lại không, Mobi thì mình chưa test được, 
mọi người dùng thì test trước ngày xem sao đã nhé.

#### Bước 1: Cài đặt
Tải app **[VNP 4G](https://play.google.com/store/apps/details?id=vn.vpn4g)** trên Google Play.
App mình viết nên đảm bảo an toàn nhé!

#### Bước 2: Đăng ký gói nền

Gói nền là gì?

Gói nền là các gói cước 4G do nhà mạng cung cấp riêng cho các dịch vụ như Tiktok, Liên Quân, Youtube, Facebook... với giá cước rẻ hơn so với các gói cước 4G thông thường, nhưng chỉ giới hạn với dịch vụ đó, ví dụ bạn đăng ký gói Tiktok thì chỉ sử dụng được mỗi Tiktok, thông qua VPN 4G bạn có thể sử dụng cho các ứng dụng khác ngoài Tiktok.

Hiện tại bạn có thể đăng ký gói TikTok hoặc Liên Quân, các gói khác bạn có thể tìm hiểu thêm tuỳ thời điểm và tuỳ nhà mạng.

- **Viettel**
    - Liên Quân:
        - Gói ngày  -   2k/ngày     -   `DK LQ` gửi `9029`
        - Gói tuần  -   10k/tuần    -   `DK LQ7` gửi `9029`
        - Gói tháng -   20k/tháng   -   `DK LQ30` gửi `9029`

    - TikTok:
        - Gói ngày:	2k/ngày     -   `DK T1` gửi `191`
        - Gói tuần:	10k/tuần    -   `DK T7` gửi `191`
        - Gói tháng: 30k/tháng  -   `DK T30` gửi `191` (hiện tại gói cước T30 đã ngừng đăng ký mới)


- **Vina**: bạn tìm hiểu thêm nhé, mình không xài ina nên không rành lắm ;)

Bạn có thể test thử trước gói ngày, để đảm bảo app hoạt động.

Sau khi đăng ký gói nền thành công bạn chuyển qua bước 3.

#### Bước 3: Sử dụng

Mở app **VPN 4G**

Đối với gói nền Tiktok bạn chỉ cần để như mặc định và bấm kết nối là được.
Đối với các gói nền khác bạn bấm vào chữ SNI và sửa đổi theo gói nền của bạn, ví dụ:

- SNI Liên Quân: `dl.kgvn.garenanow.com`
- SNI Free Fire: `dl.aw.garenanow.com`
- SNI Youtube: `m.youtube.com`
- SNI Tiktok: `m.tiktok.com` hoặc `v9.tiktokcdn.com`
...

<p align="center">
    <img src="/assets/img/posts/vpn4g-0.png" alt="drawing" width="50%"/>
</p>

Ngoài ra bạn có thể thay đổi server để đảm bảo tốc độ nhanh nhất, bạn bấm vào tên server, bấm vào vào biểu tượng giống chữ V để test ping, đợi một lúc để app test kết quả, chọn server bạn muốn, lưu ý test ping bạn cần kết nối mạng bình thường.

<p align="center">
    <img src="/assets/img/posts/vpn4g-2.png" alt="drawing" width="50%"/>
</p>

Hoặc bạn có thể thay đổi server bằng cách bấm vào nút xoay tròn ở ngoài màn hình chính.
Danh sách server sẽ được cập nhật hằng ngày.

Chúc bạn thành công!

**Lưu ý**: Nếu bạn đang xài các gói 4G chính, thì nó vẫn trừ data của gói 4G chính trước.