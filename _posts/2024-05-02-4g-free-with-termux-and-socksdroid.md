---
layout: post
title:  "4G 0đ with Termux & SocksDroid"
summary: Truy cập 4G miễn phí 0đ, chỉ với 2 ứng dụng Termux và SocksDroid
author: dieudv
date: '2024-05-02 00:00:00 +0000'
category: 'tricks'
thumbnail: /assets/img/posts/4g-0d.jpg
keywords: 4g free, termux, socksdroid
usemathjax: true
permalink: /blog/4g-free-with-termux-and-socksdroid/
---

# 4G 0đ với Termux và SocksDroid trên Android

 - Ưu điểm: Hoàn toàn miễn phí, không tốn một đồng
 - Nhược điểm: Mạng không ổn định, dùng lướt web, xem maps, không thích hợp để chơi game.

## Yêu cầu

**Sử dụng Android và cài 2 ứng dụng sau:**

- [Termux](https://play.google.com/store/apps/details?id=com.termux)
- [SocksDroid](https://apkcombo.com/socksdroid/net.typeblog.socks/)

## Cài đặt

Khi cài đặt, bạn cần kết nối mạng bình thường.

**Copy, dán mã sau vào Termux và nhấn enter:**

    pkg upgrade -y && pkg install wget -y && \
    wget https://github.com/dieudv/4g0d/releases/download/v1/v1.zip && \
    unzip v1.zip -d 4g0d && cd 4g0d && \
    chmod a+x 4g && chmod a+x psiphon-tunnel-core && \
    echo 'PATH="$PATH:$HOME/4g0d"' >> $HOME/.bashrc && source $HOME/.bashrc && \
    echo 'PATH="$PATH:$HOME/4g0d"' >> $HOME/.zshrc && source $HOME/.zshrc && clear && cd

Trong quá trình chạy, nếu nó có hỏi gì thì nhấn enter hết nhé.

<p align="center">
    <img src="https://github.com/dieudv/4g0d/assets/12602709/4fc9b88f-33c2-429a-9370-06bd3c635a89" alt="drawing" width="32%"/>
</p>

## Cấu hình & cách dùng

### Cấu hình SocksDroid:

DNS Server điền: `203.113.131.6`

Bật các mục: `Connect on Boot`, `Pre-app proxy`, `Bypass Mode`.

App List điền: `com.termux`

Xong thì gạt nút ở trên thanh tiêu đề để bật SocksDroid.    

<p align="center">
<img src="https://github.com/dieudv/4g0d/assets/12602709/8059213a-b814-4438-af06-00d52d6d7b14" alt="drawing" width="32%"/><img src="https://github.com/dieudv/4g0d/assets/12602709/a3d5de23-2d44-4c96-9911-0bf90cb80c0c" alt="drawing" width="32%"/>
</p>

### Cách dùng:

Mở Termux và gõ `4g` và nhấn enter để bắt đầu sử dụng. Termux hiện thị dòng chữ màu vàng Connected là ok.

<p align="center">
    <img src="https://github.com/dieudv/4g0d/assets/12602709/bf08b296-7383-4a15-a016-653de0bbece7" alt="drawing" width="32%"/><img src="https://github.com/dieudv/4g0d/assets/12602709/e0d0aa8b-12fe-482a-b736-b11f14edc96a" alt="drawing" width="32%"/>
</p>
