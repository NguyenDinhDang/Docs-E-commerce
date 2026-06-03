# Hướng dẫn vận hành

## 1. Chạy dự án

```bash
npm install
npm run dev
```

Mở:

```text
http://localhost:3000
```

## 2. Build production

```bash
npm run build
```

## 3. Chạy bản build

```bash
npm run start
```

## 4. Kiểm tra lint

```bash
npm run lint
```

## 5. Deploy

Do project đang dùng static export, có thể deploy `out/` lên:

- Vercel static
- Netlify
- GitHub Pages
- Nginx
- Apache
- S3/CloudFront

## 6. Các lưu ý vận hành quan trọng

### 6.1. Ảnh

Ảnh phải nằm trong `public/` và được gọi bằng path bắt đầu từ `/`.

### 6.2. localStorage

Nếu test giỏ hàng, wishlist hoặc auth demo và muốn reset dữ liệu, cần xóa key tương ứng trong browser storage.

### 6.3. Static export

Không nên thêm:

- API routes.
- Dynamic route server-side.
- Logic phụ thuộc server runtime.

### 6.4. Kiểm tra route

Khi thêm menu hoặc trang mới, phải đảm bảo route đã có file `page.tsx` tương ứng trong App Router.

## 7. Các vấn đề dễ gặp

- Ảnh không hiển thị do path sai.
- Cart/Wishlist không thay đổi vì browser còn dữ liệu cũ trong storage.
- Tab My Account không hiển thị vì `activeTab` không khớp key.
- Checkout không khớp dữ liệu giỏ vì phần summary vẫn hard-code.

