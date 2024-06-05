---
layout: post
title:  'Đăng nhập Facebook bằng cookie sử dụng Tinker Browser'
summary: 'Đăng nhập Facebook không cần mật khẩu bằng cookie sử dụng Tinker Browser'
author: dieudv
date: '2024-06-03 00:00:00 +0000'
category: 'tricks'
thumbnail: /assets/img/posts/tinker-title.webp
keywords: tinker browser, login facebook with cookie
usemathjax: true
permalink: /blog/2024-06-03-login-facebook-with-cookie-tinker-browser/
---

Tinker Browser là trình duyệt android mình đang phát triển với khả năng tùy chỉnh cao, có thể chỉnh user agent, cookie theo ý muốn.
Ngoài ra Tinker còn hỗ trợ một số tính năng tự động cho Facebook như tự động kết bạn, tự động thả cảm xúc.

Tải app **[Tinker Browser](https://play.google.com/store/apps/details?id=tinker.browser)** trên Google Play.

Để đăng nhập Facebook bằng cookie mà không cần mật khẩu sử dụng Tinker Browser, bạn làm theo hướng dẫn sau đây.

Đầu tiên, bạn cần một trình duyệt đã đăng nhập sẵn Facebook trên máy tính để lấy cookie, nếu như bằng cách nào đó bạn có được cookie rồi thì không cần điều này nữa.

Cách lấy cookie như sau (áp dụng cho tất cả trình duyệt Edge, Chrome, Brave...):

- Trên trình duyệt bạn mở Facebook, sau đó nhấn `F12`, chuyển qua tab `Application`, tìm và lưu lại 2 giá trị `c_user` và `xs`.
Đây sẽ là 2 giá trị cookie mà chúng ta sẽ sử dụng

<p align="center">
    <img src="/assets/img/posts/fb-cookie.webp" alt="drawing" width="80%"/>
</p>

Ngoài ra chúng ta cần một giá trị khác cần sử dụng là User Agent, đôi khi không cần thiết lắm, nhưng nó sẽ giúp đồng bộ thông tin trình duyệt, tránh các các phiền phức khi F.B nó báo rằng tài khoản bị hack do đăng nhập trên trình duyệt lạ.

- Cũng trên `F12`, bạn chuyển qua tab `Console`, nhấn `Ctrl + Shift + M` hoặc nhấn vào biểu tượng khoanh tròn.

Sau đó gõ vào đoạn code `window.navigator.userAgent`

<p align="center">
    <img src="/assets/img/posts/fb-user-agent.webp" alt="drawing" width="80%"/>
</p>

Copy và lưu lại thông tin User Agent này.

Sau khi đã có thông tin cần thiết bạn có thể đóng máy tính và mở Tinker Browser trên điện thoại lên rồi.

Đầu tiên bạn vào Facebook bằng Tinker, bằng cách nhập vào thanh địa chỉ `m.facebook.com`.

Trước tiên bạn cần đổi User Agent đã lấy được ở trên bằng cách bấm vào dấu 3 chấm => Settings => User Agent
Nhập giá trị User Agent đã lưu ở trên.

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-2.webp" alt="drawing" width="45%"/>
    <img src="/assets/img/posts/tinker-tutor-3.webp" alt="drawing" width="45%"/>
</p>

Tiếp theo để thêm cookie, bạn bấm vào dấu 3 chấm => Developers => Storage Manager => Cookies

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-4.webp" alt="drawing" width="45%"/>
    <img src="/assets/img/posts/tinker-tutor-5.webp" alt="drawing" width="45%"/>
</p>

Cookie name thứ nhất nhập là: `c_user` và giá trị đã lấy ở trên; Cookie Domain nhập là `.facebook.com` (có dấu chấm ở trước) và nhấn `Add Cookie`

Tương tự thêm cookie cho `xs`.

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-6.webp" alt="drawing" width="50%"/>
</p>

Nhập xong bạn nhớ kiểm tra lại xem đã thêm thành công như nhé!

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-7.webp" alt="drawing" width="50%"/>
</p>

Xong xuôi, bạn quay ra màn hình chính, reload lại trang, nếu thành công bạn sẽ vào được FB của bạn.

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-8.webp" alt="drawing" width="50%"/>
</p>

Chúc thành công!