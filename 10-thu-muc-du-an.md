# Sơ đồ Cấu trúc & Ánh xạ Giao diện (UI) thư mục `src`

Tài liệu này cung cấp sơ đồ toàn diện của thư mục `src` giúp bạn hiểu rõ từng tệp tin làm nhiệm vụ gì và hiển thị ở vị trí nào trên giao diện người dùng (UI).

---

## 1. Sơ đồ Tổng quan thư mục `src` (Next.js App Router)

```mermaid
graph TD
    src["src/"] --> app["app/ - Quản lý Tuyến đường & Giao diện chính"]
    src --> components["components/ - Các khối UI độc lập"]
    src --> store["store/ - Quản lý Trạng thái Zustand"]
    src --> utils["utils/ - Các hàm bổ trợ"]
    src --> types["types/ - Định nghĩa kiểu dữ liệu TypeScript"]

    app --> site["(site)/ - Chứa các trang"]
    app --> css["css/ - Chứa CSS Style của dự án"]
    
    site --> pages["(pages)/ - Các trang chức năng"]
    site --> layout_site["layout.tsx - Layout chung chứa Header & Footer"]
    site --> page_home["page.tsx - Trang chủ"]

    pages --> cart["cart/page.tsx - Giỏ hàng"]
    pages --> checkout["checkout/page.tsx - Thanh toán"]
    pages --> contact["contact/page.tsx - Liên hệ"]
    pages --> my_account["my-account/page.tsx - Quản lý tài khoản"]
    pages --> shop_details["shop-details/page.tsx - Chi tiết sản phẩm"]
    pages --> shop_sidebar["shop-with-sidebar/page.tsx - Cửa hàng"]
    pages --> auth["signin & signup/ - Đăng nhập & Đăng ký"]
    pages --> wishlist["wishlist/page.tsx - Yêu thích"]
```

---

## 2. Bản đồ Ánh xạ Component lên Giao diện (UI Map)

Dưới đây là mô tả chi tiết nhiệm vụ và vị trí hiển thị của từng component trong thư mục `src/components/`:

### A. Layout chung (Hiển thị ở TẤT CẢ các trang)
*   **[Header/index.tsx](file:///f:/Workspace/E-commerce/src/components/Header/index.tsx)**:
    *   *Vị trí trên UI:* Thanh điều hướng đầu trang (Navigation Bar).
    *   *Nhiệm vụ:* Logo trang web, ô Tìm kiếm sản phẩm, Dropdown chọn danh mục, thông tin số điện thoại hỗ trợ, nút dẫn tới tài khoản và Icon giỏ hàng kèm theo tổng tiền.
*   **[Footer/index.tsx](file:///f:/Workspace/E-commerce/src/components/Footer/index.tsx)**:
    *   *Vị trí trên UI:* Chân trang (Footer).
    *   *Nhiệm vụ:* Các thông tin liên hệ, liên kết chính sách mua hàng, đăng ký nhận bản tin khuyến mãi.
*   **[Common/CartSidebarModal/index.tsx](file:///f:/Workspace/E-commerce/src/components/Common/CartSidebarModal/index.tsx)**:
    *   *Vị trí trên UI:* Menu trượt ra từ bên phải màn hình khi click vào biểu tượng Giỏ hàng trên Header.
    *   *Nhiệm vụ:* Cho phép xem nhanh và chỉnh sửa nhanh các sản phẩm đang có trong giỏ, có nút chuyển nhanh đến trang Giỏ hàng hoặc trang Thanh toán.

---

### B. Trang chủ (`/`)
*   **[Home/index.tsx](file:///f:/Workspace/E-commerce/src/components/Home/index.tsx)**:
    *   *Vị trí trên UI:* Toàn bộ phần thân của Trang chủ.
    *   *Nhiệm vụ:* Chứa các banner trượt (Hero Section), danh sách danh mục sản phẩm nổi bật, các khu vực trưng bày sản phẩm mới và sản phẩm bán chạy nhất.
*   **[Shop/SingleGridItem.tsx](file:///f:/Workspace/E-commerce/src/components/Shop/SingleGridItem.tsx)**:
    *   *Vị trí trên UI:* Các ô thẻ sản phẩm (Product Cards) hiển thị trên Trang chủ và trang Cửa hàng.
    *   *Nhiệm vụ:* Hiển thị hình ảnh sản phẩm, tên, giá bán (VND), số sao đánh giá, nút thêm vào yêu thích và biểu tượng xem nhanh (mắt).

---

### C. Trang Cửa hàng (`/shop-with-sidebar`)
*   **[ShopWithSidebar/index.tsx](file:///f:/Workspace/E-commerce/src/components/ShopWithSidebar/index.tsx)**:
    *   *Vị trí trên UI:* Trang danh sách sản phẩm.
    *   *Nhiệm vụ:* Chứa bộ lọc tìm kiếm nâng cao ở bên trái và danh sách sản phẩm ở bên phải.
*   **Bộ lọc bên trái (Sidebar filters)**:
    *   `CategoryDropdown.tsx`: Bộ lọc theo Danh mục (Desktop, Laptop, Phone,...).
    *   `PriceDropdown.tsx`: Bộ lọc theo khoảng giá sản phẩm.
    *   `ColorsDropdwon.tsx`: Bộ lọc theo màu sắc.
    *   `SizeDropdown.tsx`: Bộ lọc theo dung lượng/kích cỡ.

---

### D. Trang Chi tiết Sản phẩm (`/shop-details`)
*   **[ShopDetails/index.tsx](file:///f:/Workspace/E-commerce/src/components/ShopDetails/index.tsx)**:
    *   *Vị trí trên UI:* Trang chi tiết khi nhấp vào bất kỳ sản phẩm nào.
    *   *Nhiệm vụ:*
        *   Bên trái: Trình chiếu hình ảnh chi tiết sản phẩm.
        *   Bên phải: Tên, giá bán, mô tả, các tùy chọn màu sắc/dung lượng, nút tăng giảm số lượng và nút "Thêm vào giỏ".
        *   Phần dưới: Các tab thông tin động gồm "Mô tả sản phẩm", "Thông số kỹ thuật" và "Đánh giá của khách hàng".
*   **[Common/QuickViewModal.tsx](file:///f:/Workspace/E-commerce/src/components/Common/QuickViewModal.tsx)**:
    *   *Vị trí trên UI:* Hộp thoại Modal hiện lên đè lên màn hình khi click vào icon Xem nhanh ở thẻ sản phẩm.
    *   *Nhiệm vụ:* Hiển thị nhanh các thông tin cơ bản của sản phẩm (ảnh, tên, giá, mô tả rút gọn) giúp người dùng thêm vào giỏ hàng ngay mà không cần chuyển trang.

---

### E. Trang Giỏ hàng (`/cart`) & Thanh toán (`/checkout`)
*   **[Cart/index.tsx](file:///f:/Workspace/E-commerce/src/components/Cart/index.tsx)**:
    *   *Vị trí trên UI:* Trang quản lý giỏ hàng chi tiết.
    *   *Nhiệm vụ:* Hiển thị bảng chi tiết các sản phẩm trong giỏ, cho phép tăng/giảm số lượng từng món, áp dụng mã giảm giá (`Discount.tsx`), và bảng tổng kết tổng tiền thanh toán (`OrderSummary.tsx`).
*   **[Checkout/index.tsx](file:///f:/Workspace/E-commerce/src/components/Checkout/index.tsx)**:
    *   *Vị trí trên UI:* Trang điền thông tin hoàn tất đơn hàng.
    *   *Nhiệm vụ:*
        *   `Shipping.tsx`: Form nhập Họ tên, Số điện thoại, Địa chỉ giao hàng của người nhận.
        *   `PaymentMethod.tsx`: Lựa chọn phương thức thanh toán (MB Bank, Ví MoMo, COD, PayPal).
        *   `OrderList.tsx`: Xem lại danh sách sản phẩm và tổng tiền trước khi đặt hàng.

---

## 3. Quản lý luồng bằng Zustand Store (`src/store/`)

Các store này đóng vai trò như các "kho chứa trạng thái" chạy ngầm dưới UI:
*   `cartStore.ts`: Lưu trữ danh sách sản phẩm người dùng chọn mua, tính tổng tiền giỏ hàng.
*   `wishlistStore.ts`: Lưu trữ các sản phẩm người dùng yêu thích (thả tim).
*   `quickViewStore.ts`: Quản lý việc đóng/mở và truyền dữ liệu sản phẩm vào hộp thoại xem nhanh (QuickView Modal).
*   `authStore.ts`: Quản lý trạng thái đăng nhập, thông tin tài khoản người dùng.
