---
title: "Kết Nối Và Kiểm Thử"
date: 2025-08-10
weight: 4
chapter: false
pre: "<b>4.</b>"
---

## 1. Kết nối đến Redis

### Bước 1: Khởi chạy Redis
Mở **terminal** trên EC2 và chạy:

```bash
redis-server
```

## 2: Kết nối Redis từ terminal khác
Mở một **terminal** khác, kết nối đến EC2, sau đó truy cập shell Redis:

```bash
redis-cli
```
## 3: Kiểm thử lưu và lấy dữ liệu
Trong **redis-cli**, nhập:

```bash
set key1 "hello"
get key1
```
![Test](/images/2.prerequisite/test.png)

✅ Nếu kết quả trả về "hello", Redis của bạn đã hoạt động và có thể lưu/lấy dữ liệu thành công.

Lưu ý kỹ thuật


Nếu chạy set key1 "hello" hoặc get key1 trực tiếp trong shell EC2 (không vào redis-cli) sẽ bị báo lỗi command not found.

Nguyên nhân: Đây là lệnh Redis, không phải lệnh Linux.

Cách đúng: Vào redis-cli trước rồi mới nhập các lệnh Redis.