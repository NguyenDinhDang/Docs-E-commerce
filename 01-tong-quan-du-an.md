# Tổng quan dự án

## 1. Tên dự án

Website thương mại điện tử frontend, xây dựng bằng Next.js, React, TypeScript, Tailwind CSS và Zustand.

## 2. Mục tiêu

Hệ thống mô phỏng một website bán hàng đầy đủ luồng cơ bản:

- Xem trang chủ và các khối sản phẩm nổi bật.
- Duyệt danh sách sản phẩm theo dạng lưới hoặc danh sách.
- Lọc sản phẩm qua sidebar.
- Xem chi tiết sản phẩm, preview nhanh, recently viewed.
- Thêm sản phẩm vào giỏ hàng.
- Lưu sản phẩm yêu thích vào wishlist.
- Thao tác với form checkout, thông tin tài khoản, đăng nhập và đăng ký demo.

## 3. Phạm vi bàn giao

Tài liệu này mô tả phần frontend hiện tại trong repository, bao gồm:

- Cấu trúc thư mục và routing của Next.js App Router.
- Các trang chính.
- Các tab/section trên từng màn hình.
- State management bằng Zustand.
- Luồng dữ liệu sản phẩm.
- Quy tắc lưu trữ localStorage và static export.

## 4. Mô hình triển khai hiện tại

Đây là ứng dụng frontend static:

- Không có backend API.
- Không có database.
- Không có server-side authentication thật.
- Dữ liệu giỏ hàng, wishlist và auth demo được lưu trong browser `localStorage`.
- Build tạo thư mục `out/` để deploy lên hosting tĩnh.

## 5. Các luồng người dùng chính

### 5.1. Mua hàng

Người dùng vào trang chủ, chuyển sang shop, lọc sản phẩm, mở quick view hoặc chi tiết sản phẩm, rồi thêm vào giỏ hàng.

### 5.2. Quản lý giỏ hàng

Người dùng xem danh sách sản phẩm trong cart, cập nhật số lượng, xóa item hoặc xóa toàn bộ giỏ.

### 5.3. Checkout

Người dùng đi qua các khối:

- Login demo.
- Billing details.
- Shipping.
- Notes.
- Order summary.
- Coupon.
- Shipping method.
- Payment method.

### 5.4. Tài khoản

Màn `My Account` chia thành nhiều tab để mô phỏng dashboard, orders, downloads, addresses và account details.

