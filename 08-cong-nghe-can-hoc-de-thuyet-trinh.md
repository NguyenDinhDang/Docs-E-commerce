# Công nghệ cần học để thuyết trình dự án

Tài liệu này giúp bạn nắm đúng những công nghệ cốt lõi của dự án để có thể trình bày mạch lạc, trả lời câu hỏi kỹ thuật rõ ràng, và giải thích được luồng chạy của hệ thống mà không bị vấp.

## 1. Mục tiêu học

Bạn không cần học tất cả mọi thứ trong codebase. Chỉ cần nắm các nhóm sau:

- Next.js App Router.
- React component và state.
- TypeScript type.
- Tailwind CSS.
- Zustand.
- localStorage.
- Static export trong Next.js.
- Cách dữ liệu đi từ `shopData` đến UI rồi vào cart/wishlist/quick view.

## 2. Thứ tự nên học

### 2.1. Học kiến trúc tổng thể trước

Bạn cần trả lời được 3 câu:

1. Trang nào được render ở đâu.
2. Dữ liệu đi từ đâu đến đâu.
3. Trạng thái nào lưu tạm ở client.

### 2.2. Học routing sau

Biết route nào tương ứng với file nào:

- `/` -> trang chủ.
- `/shop-with-sidebar` -> danh sách sản phẩm.
- `/shop-details` -> chi tiết sản phẩm.
- `/cart` -> giỏ hàng.
- `/checkout` -> thanh toán.
- `/wishlist` -> yêu thích.
- `/my-account` -> tài khoản.

### 2.3. Học state cuối cùng

Nếu hiểu `Zustand + localStorage`, bạn sẽ giải thích được 80% luồng nghiệp vụ.

## 3. Next.js cần học gì

### 3.1. App Router

Project này dùng cấu trúc `src/app`.

Bạn cần biết:

- Mỗi thư mục `page.tsx` là một route.
- `layout.tsx` là khung bao ngoài cho nhiều trang.
- Component trong `src/components` được kéo vào page để render UI.

### 3.2. Static export

File `next.config.js` bật `output: 'export'`.

Ý nghĩa:

- App được build ra file tĩnh.
- Không có API route.
- Không có server logic chạy runtime.
- Khi deploy, bạn chỉ cần host các file static trong `out/`.

### 3.3. Cách trả lời khi bị hỏi

Nếu bị hỏi: “Vì sao dùng Next.js?”

Bạn có thể trả lời:

> Dự án dùng Next.js để tổ chức routing theo file, dễ chia page theo từng màn hình thương mại điện tử, và build ra static site nên dễ deploy.

## 4. React cần học gì

### 4.1. Component

Mỗi màn hình trong dự án là một component ghép từ nhiều component nhỏ.

Ví dụ:

- `Header`
- `Footer`
- `ProductItem`
- `QuickViewModal`
- `CartSidebarModal`

### 4.2. State và props

Bạn cần hiểu:

- `props` dùng để truyền dữ liệu từ cha xuống con.
- `useState` dùng cho trạng thái local của component.
- `useEffect` dùng cho side effect như:
  - gắn event listener
  - lưu localStorage
  - xử lý đóng modal khi click ngoài

### 4.3. Luồng hay gặp

Ví dụ trong `ShopDetails`:

- `useState` quản lý tab, số lượng, ảnh đang xem.
- `useQuickViewStore` lấy product đã chọn.
- `useEffect` lưu product vào `localStorage`.

### 4.4. Cách trả lời khi bị hỏi

Nếu bị hỏi: “Dòng này chạy như thế nào?”

Bạn nên mô tả theo thứ tự:

1. Component được render.
2. State ban đầu được khởi tạo.
3. Người dùng click hoặc nhập liệu.
4. State thay đổi.
5. UI re-render.

## 5. TypeScript cần học gì

### 5.1. Type và interface

Dự án dùng TypeScript để mô tả:

- `Product`
- `CartItem`
- `WishlistItem`
- `User`

### 5.2. Tại sao quan trọng

TypeScript giúp:

- tránh truyền sai dữ liệu vào component.
- biết object cần có field nào.
- giảm lỗi khi thêm sản phẩm mới hoặc sửa store.

### 5.3. Cách trả lời khi bị hỏi

Nếu bị hỏi: “TypeScript giúp gì ở đây?”

Bạn có thể nói:

> TypeScript giúp đảm bảo dữ liệu sản phẩm, giỏ hàng và wishlist có đúng cấu trúc, tránh lỗi khi component nhận thiếu field hoặc truyền sai kiểu.

## 6. Tailwind CSS cần học gì

### 6.1. Utility class

Giao diện được viết trực tiếp trong `className`.

Ví dụ:

- `flex`
- `grid`
- `gap-4`
- `rounded-lg`
- `bg-white`
- `text-dark`

### 6.2. Điều cần hiểu

- Layout được chia bằng utility class.
- Responsive dùng prefix như `sm:`, `lg:`, `xl:`.
- Trạng thái hover, active cũng là class.

### 6.3. Cách trả lời khi bị hỏi

Nếu bị hỏi: “Sao không dùng CSS riêng?”

Bạn có thể nói:

> Dự án ưu tiên Tailwind để giữ giao diện nhanh, đồng nhất và dễ chỉnh sửa theo component mà không phải tạo nhiều file CSS riêng.

## 7. Zustand cần học gì

Đây là phần quan trọng nhất nếu bạn muốn giải thích state mà không vấp.

### 7.1. Zustand là gì

Zustand là thư viện quản lý state client-side gọn hơn Redux.

Trong dự án, Zustand đang dùng cho:

- cart
- wishlist
- quick view
- cart sidebar modal
- preview slider modal
- auth demo

### 7.2. Bạn cần nhớ 3 khái niệm

- `create(...)`: tạo store.
- `set(...)`: cập nhật state.
- `get(...)`: đọc state hiện tại.

### 7.3. Dòng chạy của một action

Ví dụ thêm vào giỏ:

1. Người dùng bấm nút `Thêm vào giỏ`.
2. Component gọi `addItem(...)`.
3. Zustand cập nhật `items`.
4. Store được persist vào `localStorage`.
5. `Cart` hoặc `CartSidebarModal` đọc store mới.
6. UI tự render lại.

### 7.4. Cách trả lời khi bị hỏi

Nếu bị hỏi: “Zustand làm gì ở đây?”

Bạn có thể trả lời:

> Zustand giữ state dùng chung như giỏ hàng, wishlist, quick view và modal, để nhiều component khác nhau có thể đọc và cập nhật cùng một dữ liệu mà không cần truyền props qua nhiều cấp.

## 8. localStorage cần học gì

### 8.1. Vai trò

localStorage lưu dữ liệu trên trình duyệt để refresh trang không mất state.

Trong dự án đang có:

- `cart-storage`
- `wishlist-storage`
- `auth-storage`
- `productDetails`

### 8.2. Điều cần hiểu

- Dữ liệu chỉ tồn tại trên máy của người dùng.
- Không phải database.
- Không dùng cho dữ liệu cần đồng bộ thật giữa nhiều thiết bị.

### 8.3. Cách trả lời khi bị hỏi

Nếu bị hỏi: “Vì sao refresh mà giỏ vẫn còn?”

Bạn trả lời:

> Vì store Zustand được persist xuống localStorage, nên khi reload lại, state được đọc từ storage và khôi phục lên UI.

## 9. Dữ liệu sản phẩm cần học gì

### 9.1. File chính

- `src/components/Shop/shopData.ts`

### 9.2. Điều cần nhớ

Mỗi sản phẩm có:

- `id`
- `title`
- `category`
- `description`
- `price`
- `discountedPrice`
- `reviews`
- `rating`
- `imgs.thumbnails`
- `imgs.previews`

### 9.3. Cách dữ liệu chạy

1. `shopData` chứa danh sách sản phẩm.
2. Trang chủ lấy vài sản phẩm đầu.
3. Trang shop lấy toàn bộ danh sách.
4. Card sản phẩm mở quick view.
5. Quick view đẩy product vào store.
6. Shop details đọc product từ store/localStorage.

### 9.4. Câu hỏi hay bị hỏi

- Dữ liệu lấy từ đâu?
- Có backend không?
- Vì sao đổi ảnh chỉ cần sửa `public/images`?
- Khi thêm sản phẩm mới thì sửa file nào?

## 10. Routing cần học gì

Bạn cần nhớ mapping route quan trọng:

- `/` -> Home
- `/shop-with-sidebar` -> ShopWithSidebar
- `/shop-details` -> ShopDetails
- `/cart` -> Cart
- `/checkout` -> Checkout
- `/wishlist` -> Wishlist
- `/my-account` -> MyAccount
- `/signin` -> Signin
- `/signup` -> Signup

Nếu bị hỏi: “Menu này bấm đi đâu?”

Bạn chỉ cần chỉ ra `menuData.ts` và route tương ứng.

## 11. Flow nghiệp vụ cần thuộc

### 11.1. Flow xem sản phẩm

Người dùng -> Home/Shop -> chọn sản phẩm -> Quick View hoặc Shop Details.

### 11.2. Flow thêm giỏ

Người dùng -> bấm `Thêm vào giỏ` -> `cartStore` -> `localStorage` -> Cart page/Cart sidebar.

### 11.3. Flow wishlist

Người dùng -> bấm tim -> `wishlistStore` -> `localStorage` -> Wishlist page.

### 11.4. Flow preview

Người dùng -> mở Quick View hoặc Shop Details -> bấm zoom -> preview slider modal.

### 11.5. Flow account

Người dùng -> My Account -> đổi tab -> xem dashboard/orders/addresses/account details.

## 12. Những chỗ nên học theo mức ưu tiên

### Mức 1, bắt buộc

- Next.js App Router
- React state/props/useEffect
- Zustand
- localStorage
- route chính

### Mức 2, rất nên biết

- TypeScript interface/type
- Tailwind responsive class
- persistent store
- modal flow

### Mức 3, biết thêm để trả lời sâu

- static export
- dynamic state sharing
- data-driven UI

## 13. Những câu hỏi bảo vệ hay gặp

### 13.1. Dự án này làm gì?

Trả lời:

> Đây là website e-commerce frontend mô phỏng hành vi mua sắm cơ bản như xem sản phẩm, lọc, thêm giỏ, wishlist, checkout và tài khoản.

### 13.2. Dữ liệu ở đâu ra?

Trả lời:

> Hiện dữ liệu sản phẩm là static data trong code, còn cart/wishlist/auth demo lưu trên localStorage.

### 13.3. Có backend không?

Trả lời:

> Chưa có backend thật. Dự án đang là frontend static để trình diễn và bàn giao giao diện, luồng nghiệp vụ cơ bản.

### 13.4. Vì sao dùng Zustand thay vì Redux?

Trả lời:

> Vì state của dự án không quá phức tạp, Zustand gọn hơn, ít boilerplate hơn, dễ học hơn và vẫn đủ cho cart, wishlist, modal và auth demo.

### 13.5. Làm sao để refresh không mất giỏ?

Trả lời:

> Store được persist trong localStorage, khi reload app sẽ đọc lại dữ liệu đã lưu.

### 13.6. Dòng này chạy như thế nào?

Mẫu trả lời:

> Component render trước, state khởi tạo, người dùng bấm nút, handler gọi action của store, store cập nhật state và lưu localStorage nếu cần, sau đó UI re-render theo state mới.

## 14. Cách luyện nói để không vấp

Hãy nhớ công thức 4 bước:

1. Nói tên file hoặc component.
2. Nói dữ liệu đi từ đâu.
3. Nói action nào xảy ra khi người dùng thao tác.
4. Nói kết quả UI hoặc state thay đổi ra sao.

Ví dụ:

> Trong `src/components/Common/QuickViewModal.tsx`, khi người dùng bấm nút zoom, component lấy product từ Zustand store, mở modal preview, rồi hiển thị ảnh lớn bằng Swiper. Dữ liệu hiển thị phụ thuộc vào product đã được set trước đó từ card sản phẩm.

## 15. Kết luận

Nếu bạn học đúng các phần trên, bạn sẽ:

- hiểu được dự án đang chạy như thế nào,
- trả lời được câu hỏi về từng dòng code quan trọng,
- giải thích được luồng dữ liệu không bị rối,
- và trình bày dự án một cách mạch lạc, tự tin.

