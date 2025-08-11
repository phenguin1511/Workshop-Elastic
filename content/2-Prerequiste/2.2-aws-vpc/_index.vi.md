---
title: "Tạo VPC và Subnet"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>2.2 </b>"
---

## 1. Tạo VPC

Để tạo **VPC** (Virtual Private Cloud) trên AWS, thực hiện theo các bước sau:

1. Truy cập **VPC Console** tại:  
   [https://console.aws.amazon.com/vpc](https://console.aws.amazon.com/vpc)

2. Ở menu điều hướng bên trái, chọn **Your VPCs**.

   ![Your VPCs](/images/2.prerequisite/vpc-1.png)

3. Nhấn **Create VPC**.

4. Cấu hình thông số VPC như hình minh họa:

   ![Create VPC](/images/2.prerequisite/vpc-2.png)

   - **Name tag**: `redis-ha-vpc`  
     > *Tên hiển thị trong bảng quản lý, khuyến nghị đặt theo chuẩn đặt tên của dự án.*
   - **IPv4 CIDR block**: `10.0.0.0/16`  
     > *CIDR block xác định dải địa chỉ IP cho toàn bộ VPC. `/16` cung cấp ~65,536 địa chỉ IP khả dụng.*  
   - **Tenancy**: *Default*  
     > *Chọn Dedicated chỉ khi cần tách biệt phần cứng vật lý, sẽ phát sinh chi phí cao hơn.*

5. Nhấn **Create VPC** để khởi tạo.

   ![VPC Created](/images/2.prerequisite/vpc-3.png)

6. Sau khi tạo, VPC mới sẽ xuất hiện trong danh sách **Your VPCs** với trạng thái *Available*.

---

## 2. Tạo Subnet

Subnet là các phân vùng con trong VPC, mỗi subnet nằm trong **một** Availability Zone (AZ). Để triển khai hệ thống HA (High Availability), cần tạo nhiều subnet ở các AZ khác nhau.

### Các bước thực hiện

1. Trong **VPC Console**, chọn **Subnets** ở menu bên trái.

   ![Subnets Menu](/images/2.prerequisite/subnet-1.png)

2. Nhấn **Create subnet**.

3. Ở mục **VPC ID**, chọn VPC vừa tạo (`redis-ha-vpc`).

4. Tạo lần lượt các subnet sau:

   **a. Subnet cho AZ1**  
   - **Subnet name**: `AZ1`  
   - **Availability Zone**: chọn AZ1 của region đang sử dụng  
   - **IPv4 CIDR block**: `10.0.1.0/24`  
     > *Cung cấp 256 địa chỉ IP, dùng cho một phần workload trong AZ1.*

   **b. Subnet cho AZ2**  
   - **Subnet name**: `AZ2`  
   - **Availability Zone**: khác với AZ1 và AZ3  
   - **IPv4 CIDR block**: `10.0.2.0/24`

   **c. Subnet cho AZ3**  
   - **Subnet name**: `AZ3`  
   - **Availability Zone**: khác với AZ1 và AZ2  
   - **IPv4 CIDR block**: `10.0.3.0/24`

   **d. Public Subnet** (dùng cho Bastion Host)  
   - **Subnet name**: `Public-Subnet`  
   - **Availability Zone**: cùng AZ1 để tối ưu chi phí  
   - **IPv4 CIDR block**: `10.0.10.0/24`  
     > *Public subnet sẽ gắn Internet Gateway để cho phép kết nối từ bên ngoài.*

5. Nhấn **Create subnet** sau khi cấu hình xong.

   ![Subnets Created](/images/2.prerequisite/subnet-2.png)

6. Kết quả sau khi tạo thành công:

   ![Subnets List](/images/2.prerequisite/subnet-3.png)

---

## 💡 Lưu ý kỹ thuật

- **Quy hoạch địa chỉ IP trước**: Tránh để các CIDR block của subnet chồng lấn nhau hoặc trùng với hệ thống mạng hiện có.
- **Tách biệt public và private subnet**: Public subnet gắn Internet Gateway, private subnet dùng NAT Gateway/Bastion để truy cập ra ngoài.
- **HA (High Availability)**: Nên trải subnet trên ít nhất 2-3 AZ để tăng khả năng chịu lỗi khi một AZ gặp sự cố.
- **Naming convention**: Dùng quy tắc đặt tên thống nhất để dễ dàng quản lý (VD: `<env>-<purpose>-<az>`).
- **CIDR block nhỏ gọn**: Chỉ cấp đủ IP cần thiết cho từng subnet, để dành không gian cho các subnet khác trong tương lai.
