# Tính năng và UI

## 1. Trang chủ

File chính:

- `src/components/Home/index.tsx`

### Các khu vực chính

- Sidebar danh mục mua hàng.
- Hero banner lớn.
- Khối quick stats.
- Khối sản phẩm nổi bật.
- Newsletter.

### Tab/section trên trang chủ

Trang chủ không dùng tab đúng nghĩa, nhưng có các section UI:

- Category sidebar.
- Hero.
- Featured products.
- Newsletter.

### Dữ liệu hiển thị

- Danh mục cứng nằm trong component Home.
- Sản phẩm nổi bật lấy từ `shopData.slice(0, 6)`.

## 2. Trang danh sách sản phẩm

File chính:

- `src/components/ShopWithSidebar/index.tsx`

### Tính năng chính

- Sidebar lọc sản phẩm.
- Chọn kiểu hiển thị `grid` hoặc `list`.
- Sticky sidebar trên mobile.
- Bấm ngoài sidebar để đóng.
- Custom select sắp xếp.

### Các trạng thái UI

- `productStyle`: chuyển đổi giữa grid và list.
- `productSidebar`: mở/đóng sidebar trên mobile.
- `stickyMenu`: đổi vị trí nút sidebar khi cuộn trang.

### Sidebar filter

Các khối lọc đang có:

- Category
- Gender
- Size
- Color
- Price

Lưu ý: đây là UI filter mô phỏng, chưa có logic lọc dữ liệu thật theo state.

### Grid/List tab

Khối hiển thị sản phẩm hoạt động như tab:

- `grid` hiển thị `SingleGridItem`.
- `list` hiển thị `SingleListItem`.

## 3. Trang chi tiết sản phẩm

File chính:

- `src/components/ShopDetails/index.tsx`

### Tính năng chính

- Hiển thị ảnh preview lớn.
- Chọn thumbnail để đổi ảnh.
- Mở preview slider.
- Chọn option storage, type, sim, quantity.
- Hiển thị các tab nội dung mô tả sản phẩm.
- Hiển thị recently viewed.
- Newsletter phía dưới.

### Tabs trong chi tiết sản phẩm

1. `Description`
2. `Additional Information`
3. `Reviews`

### Luồng dữ liệu sản phẩm

- Sản phẩm được lấy từ `quickViewStore` hoặc từ `localStorage` key `productDetails`.
- Khi có product, component ghi lại vào `localStorage` để giữ trạng thái khi refresh.

## 4. Giỏ hàng

File chính:

- `src/components/Cart/index.tsx`

### Tính năng

- Hiển thị danh sách item trong cart.
- Hiển thị màn trạng thái rỗng khi chưa có hàng.
- Có khối discount.
- Có order summary.

### Hành vi

- Giỏ lấy dữ liệu từ `useCartStore`.
- Khi cart rỗng, trang hiển thị CTA sang shop.

## 5. Checkout

File chính:

- `src/components/Checkout/index.tsx`

### Các khối trong checkout

- Login
- Billing
- Shipping
- Notes
- Order list
- Coupon
- Shipping method
- Payment method

### Nhận xét kỹ thuật

Trang checkout hiện là form mô phỏng, các phần order summary và danh sách sản phẩm đang hard-code, chưa nối động trực tiếp với cart store.

## 6. My Account

File chính:

- `src/components/MyAccount/index.tsx`
- `src/components/MyAccount/tabsData.tsx`

### Tabs của My Account

1. `dashboard`
2. `orders`
3. `downloads`
4. `addresses`
5. `account details`

### Nội dung từng tab

- `dashboard`: thông tin người dùng, email, phone, địa chỉ.
- `orders`: danh sách đơn hàng, action, modal chi tiết.
- `downloads`: nội dung tải xuống.
- `addresses`: thông tin địa chỉ, mở `AddressModal`.
- `account details`: chỉnh sửa thông tin cá nhân và đổi mật khẩu.

### Lưu ý

Tab state hiện được quản lý bằng `useState` trong component, chưa tách thành store riêng.

## 7. Header menu

File chính:

- `src/components/Header/menuData.ts`

### Cấu trúc menu

- Trang chủ
- Sản phẩm
- Liên hệ
- Tài khoản

### Menu con dưới tài khoản

- Thanh toán
- Giỏ hàng
- Yêu thích
- Đăng nhập
- Đăng ký
- Tài khoản của tôi

## 8. Wishlist

File chính:

- `src/components/Wishlist/index.tsx`

### Tính năng

- Lưu sản phẩm yêu thích.
- Xóa item.
- Giữ trạng thái qua refresh nhờ persist store.

