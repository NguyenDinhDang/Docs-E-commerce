# State và dữ liệu

## 1. Zustand stores đang dùng

### 1.1. `cartStore.ts`

Quản lý giỏ hàng.

#### Data shape

```ts
{
  id: string;
  title: string;
  price: number;
  image: string;
  quantity: number;
  size?: string;
  color?: string;
}
```

#### Hàm chính

- `addItem`
- `removeItem`
- `updateQuantity`
- `clearCart`
- `getTotal`
- `getItemCount`

#### Persistence

- Lưu trong `localStorage` key `cart-storage`.

### 1.2. `wishlistStore.ts`

Quản lý danh sách yêu thích.

#### Data shape

```ts
{
  id: string;
  title: string;
  price: number;
  image: string;
  category?: string;
}
```

#### Hàm chính

- `addItem`
- `removeItem`
- `isInWishlist`
- `getItemCount`
- `clearWishlist`

#### Persistence

- Lưu trong `localStorage` key `wishlist-storage`.

### 1.3. `quickViewStore.ts`

Quản lý product đang xem nhanh.

#### Data shape

```ts
{
  id: string;
  title: string;
  price: number;
  image: string;
  description?: string;
  rating?: number;
  reviews?: number;
  inStock?: boolean;
  category?: string;
}
```

#### Hàm chính

- `openQuickView`
- `closeQuickView`

### 1.4. `authStore.ts`

Quản lý auth demo.

#### Data shape

```ts
{
  id: string;
  email: string;
  name: string;
  phone?: string;
  address?: string;
  city?: string;
  state?: string;
  zipCode?: string;
  country?: string;
}
```

#### Hàm chính

- `login`
- `signup`
- `logout`
- `updateProfile`

#### Lưu ý nghiệp vụ

- Đây là fake auth.
- Không có xác thực thật qua backend.
- Chỉ cần email/password/name hợp lệ theo điều kiện tối thiểu là set state.

### 1.5. `cartSidebarModalStore.ts`

Quản lý trạng thái mở/đóng modal cart sidebar.

## 2. Nguồn dữ liệu sản phẩm

### File chính

- `src/components/Shop/shopData.ts`

### Type

- `src/types/product.ts`

### Cấu trúc product

```ts
{
  title: string;
  reviews: number;
  price: number;
  discountedPrice: number;
  id: number;
  description?: string;
  rating?: number;
  category?: string;
  imgs: {
    thumbnails: string[];
    previews: string[];
  };
}
```

### Ý nghĩa business

- `price`: giá gốc.
- `discountedPrice`: giá hiện thị ưu đãi.
- `imgs.thumbnails`: ảnh nhỏ ở gallery.
- `imgs.previews`: ảnh lớn.

## 3. Cách các component đọc dữ liệu

- Trang chủ lấy từ `shopData` để render featured products.
- Shop page lấy từ `shopData` để render toàn bộ catalogue.
- Cart page lấy từ `cartStore`.
- Wishlist page lấy từ `wishlistStore`.
- Shop details nhận dữ liệu từ quick view hoặc localStorage.

## 4. Storage keys

- `cart-storage`
- `wishlist-storage`
- `auth-storage`
- `productDetails`

## 5. Dữ liệu legacy

Trong `src/redux` vẫn còn:

- cart slice
- wishlist slice
- quick view slice
- product details
- provider/store Redux

Hiện tại đây là phần để tham khảo hoặc phục vụ migration cũ. Nếu tiếp tục phát triển, nên chọn một nguồn state duy nhất để tránh lệch dữ liệu.

