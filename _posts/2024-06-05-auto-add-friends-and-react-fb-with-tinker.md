---
layout: post
title:  'Tự động kết bạn, thả cảm xúc FB với Tinker'
summary: 'Tự động kết bạn, thả cảm xúc Facebook với Tinker Browser'
author: dieudv
date: '2024-06-05 00:00:00 +0000'
category: 'tricks'
thumbnail: /assets/img/posts/tinker-title.webp
keywords: tinker browser, auto add friends, auto reaction
usemathjax: true
permalink: /blog/2024-06-05-auto-add-friends-and-react-fb-with-tinker/
---

**Tinker Browser** là trình duyệt android mình đang phát triển với khả năng tùy chỉnh cao, ngoài ra Tinker còn hỗ trợ một số tính năng tự động cho Facebook như tự động kết bạn, tự động thả cảm xúc.

Để sử dụng tính năng này bạn cần tải app **[Tinker Browser](https://play.google.com/store/apps/details?id=tinker.browser)** trên Google Play.

Đăng nhập bằng mật khẩu như bạn sử dụng một trình duyệt bình thường, hoặc sử dụng cookies.
Khuyến nghị đăng nhập sử dụng cookie theo hướng đẫn ở [bài viết này](/blog/2024-06-03-login-fb-with-cookie-tinker-browser/).

Nếu đã đăng nhập Facebook, bạn sẽ thấy menu `Tools` khi bấm vào dấu 3 chấm ở góc phải màn hình, bạn sẽ thấy các chức năng **`Auto Reaction`** và **`Friend Request`**

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-2-1.webp" alt="drawing" width="48%"/>
    <img src="/assets/img/posts/tinker-tutor-2-2.webp" alt="drawing" width="48%"/>
</p>


## Auto Reaction

Đây là chức năng tự động thả cảm xúc vào viết của bạn bè, bạn sẽ không cần cài đặt đặc biệt vì tool sẽ tự làm hết cho bạn. Mỗi 5 phút 1 lần, tool sẽ kiểm tra bài đăng trên news feed của bạn và tự động lựa chọn cảm xúc phù hợp với bài đăng đó để thả, và chỉ thả cảm xúc vào bài đăng của bạn bè và bỏ qua bài viết của fanpage hay trong nhóm.

Chức năng này rất dễ sử dụng, bạn chỉ cần bấm vào nút `Start` để chạy thôi.

<p align="center">
    <img src="/assets/img/posts/tinker-ar-log.webp" alt="drawing" width="48%"/>
</p>

Sau khi chạy tầm 15p, bạn bấm vào menu `Activity log` ở bên góc trên bên phải để kiểm tra xem mình đã thả cảm xúc vào những bài đăng nào nhé.

## Friend Request

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-2-3.webp" alt="drawing" width="48%"/>
</p>

Đây là chức năng tự động kết bạn tự động với các chức năng con sau đây:

- **Add people may you know**: Kết bạn với những người bạn có thể biết
- **Add memmbers of group**: Kết bạn với thành viên của nhóm
- **Confirm friend request**: Xác nhận kết bạn với những lời mời kết bạn người khác gửi cho mình
- **Cancel sent request**: Hủy những lời mời kết bạn mà mình đã gửi, trong trường hợp bạn gửi quá nhiều rồi, để lâu rồi mà người ta không chấp nhận.

Đối với 2 tính năng **Confirm friend request** và **Cancel sent request**, bạn chỉ cần chỉnh sửa thông số `Limit` giới hạn số bạn bè mà bạn sẽ xác nhận kết bạn hoặc hủy lời mời.
Điều này sẽ hạn chế việc FB xem đó là hành động spam và khóa tính năng.

<p align="center">
    <img src="/assets/img/posts/tinker-confirm-req.webp" alt="drawing" width="48%"/>
    <img src="/assets/img/posts/tinker-cancel.webp" alt="drawing" width="48%"/>
</p>

### Add people may you know

**Thêm những người bạn có thể biết**.

<p align="center">
    <img src="/assets/img/posts/tinker-add-may-know.webp" alt="drawing" width="48%"/>
</p>

Tính năng này có 2 thông số là `Limit` như trên và `Mutual friends`.
`Mutual friends` là giới hạn số bạn chung mà bạn và người đó có, ví dụ bạn cài đặt là 10, thì tool sẽ chỉ kết bạn với những người bạn có bạn chung lớn hơn hoặc bằng 10.

### Add memmbers of group

**Thêm thành viên của nhóm**.

Để sử dụng tính năng này bạn cần quay ra màn hình chính, vào một nhóm mà bạn muốn, để tool có thể nhận diện được nhóm mà bạn muốn thêm bạn bè là nhóm nào. Bạn vào nhóm mà bạn muốn, tại nhóm đó reload lại FB một lần nữa. Ở đây mình ví dụ là nhóm J2Team nhé.

Sau đó quay lại tool, bạn sẽ thấy tên nhóm và ID nhóm được hiển thị.

<p align="center">
    <img src="/assets/img/posts/tinker-tutor-2-7.webp" alt="drawing" width="48%"/>
    <img src="/assets/img/posts/tinker-add-gr-mem.webp" alt="drawing" width="48%"/>
</p>

Set limit và bấm `Start` để chạy thôi.

Để xem bạn đã kết bạn với ai thì bấm vào menu bên phải để xem nhé.

<p align="center">
    <img src="/assets/img/posts/tinker-fr-log.webp" alt="drawing" width="48%"/>
</p>

Để dừng thì bạn quay lại tool và bấm `Stop` nhé.

Lưu ý rằng bạn không thể chạy `Auto Reaction` và `Friend Request` cùng lúc nha, chỉ có thể chạy một trong 2, chạy cái này phải tắt cái kia đi.

Chúc bạn thành công!