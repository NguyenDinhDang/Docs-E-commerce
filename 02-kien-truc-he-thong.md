# Kiến trúc hệ thống

## 1. Stack công nghệ

- Next.js 16 với App Router.
- React 19.
- TypeScript 5.
- Tailwind CSS 3.
- Zustand để quản lý state client-side.
- Swiper cho carousel/slider.
- React Hot Toast cho thông báo.

## 2. Cấu trúc thư mục chính

### `src/app`

Chứa routing theo App Router.

- `src/app/(site)/page.tsx`: trang chủ.
- `src/app/(site)/(pages)/cart/page.tsx`: giỏ hàng.
- `src/app/(site)/(pages)/checkout/page.tsx`: thanh toán.
- `src/app/(site)/(pages)/contact/page.tsx`: liên hệ.
- `src/app/(site)/(pages)/mail-success/page.tsx`: màn hình gửi mail thành công.
- `src/app/(site)/(pages)/my-account/page.tsx`: tài khoản người dùng.
- `src/app/(site)/(pages)/shop-details/page.tsx`: chi tiết sản phẩm.
- `src/app/(site)/(pages)/shop-with-sidebar/page.tsx`: danh sách sản phẩm có sidebar.
- `src/app/(site)/(pages)/signin/page.tsx`: đăng nhập.
- `src/app/(site)/(pages)/signup/page.tsx`: đăng ký.
- `src/app/(site)/(pages)/wishlist/page.tsx`: wishlist.

### `src/components`

Chứa các khối UI và page-level components.

- `Header`, `Footer`, `Common`: layout dùng lại.
- `Home`: các section trên trang chủ.
- `Shop`: dữ liệu và item card sản phẩm.
- `ShopWithSidebar`: danh sách sản phẩm, bộ lọc, toggle grid/list.
- `ShopDetails`: chi tiết sản phẩm và các tab nội dung.
- `Cart`, `Checkout`, `Wishlist`: luồng mua hàng.
- `MyAccount`: dashboard tài khoản và tabs.
- `Auth`: form đăng nhập/đăng ký.
- `Blog`, `Orders`, `Contact`, `Error`, `MailSuccess`: các màn phụ trợ.

### `src/store`

Chứa Zustand stores đang dùng thực tế.

- `cartStore.ts`
- `wishlistStore.ts`
- `quickViewStore.ts`
- `authStore.ts`
- `cartSidebarModalStore.ts`

### `src/redux`

Thư mục Redux vẫn còn trong source, nhưng hiện là lớp di sản. Khi bàn giao, nên ưu tiên `src/store` vì đây là luồng đang vận hành trên UI.

## 3. Cấu hình build

File `next.config.js` đang bật:

- `output: 'export'`
- `trailingSlash: true`

Điều đó có nghĩa:

- Build ra web tĩnh.
- Không dùng API routes.
- Không dùng server logic động.
- Route và asset phải phù hợp static hosting.

## 4. Nguyên tắc dữ liệu

### 4.1. Dữ liệu sản phẩm

Sản phẩm gốc được khai báo tĩnh trong `src/components/Shop/shopData.ts`.

### 4.2. Dữ liệu người dùng

Auth demo, cart, wishlist và một số trạng thái UI được giữ bằng Zustand.

### 4.3. Hình ảnh

Ảnh nằm trong `public/images/...` và được tham chiếu bằng path từ root, ví dụ:

```ts
"/images/products/product-1-bg-1.png"
```

## 5. Luồng render

1. Next.js render các page trong `src/app`.
2. Page import component tương ứng trong `src/components`.
3. Component đọc dữ liệu từ `shopData` hoặc Zustand store.
4. UI cập nhật theo state local hoặc persisted state trong browser.

