# Sơ đồ Mermaid

## 1. Tổng quan luồng người dùng

```mermaid
flowchart TD
  A[Người dùng] --> B[Trang chủ]
  B --> C[Danh sách sản phẩm]
  C --> D[Quick View]
  C --> E[Chi tiết sản phẩm]
  E --> F[Thêm vào giỏ hàng]
  D --> F
  F --> G[Giỏ hàng]
  G --> H[Checkout]
  H --> I[My Account]
  C --> J[Wishlist]
  E --> J
```

## 2. Kiến trúc người dùng -> hệ thống

```mermaid
flowchart LR
  U[Người dùng] --> UI[Next.js UI Components]
  UI --> S1[Zustand Stores]
  UI --> S2[Local State / Tabs]
  UI --> D1[shopData.ts]
  S1 --> LS[(localStorage)]
  D1 --> UI
  LS --> S1
  UI --> P[Public Images]
```

## 3. Luồng dữ liệu sản phẩm

```mermaid
flowchart TD
  A[src/components/Shop/shopData.ts] --> B[Home Featured Products]
  A --> C[ShopWithSidebar Listing]
  A --> D[ShopDetails Gallery]
  A --> E[Quick View]
  E --> F[useQuickViewStore]
  F --> G[ShopDetails Page]
  G --> H[localStorage productDetails]
```

## 4. Luồng giỏ hàng

```mermaid
flowchart TD
  A[Product Card] --> B[useCartStore.addItem]
  B --> C[cart-storage localStorage]
  C --> D[Cart Page]
  D --> E[Update Quantity]
  D --> F[Remove Item]
  D --> G[Clear Cart]
  D --> H[Get Total / Item Count]
```

## 5. Luồng wishlist

```mermaid
flowchart TD
  A[Product Card / Detail] --> B[useWishlistStore.addItem]
  B --> C[wishlist-storage localStorage]
  C --> D[Wishlist Page]
  D --> E[Remove Item]
  D --> F[Count / Check Exists]
```

## 6. Luồng auth demo

```mermaid
flowchart TD
  A[Signin / Signup Form] --> B[useAuthStore.login or signup]
  B --> C[Generate demo user]
  C --> D[auth-storage localStorage]
  D --> E[My Account]
  E --> F[Update Profile]
  F --> D
```

## 7. Luồng checkout

```mermaid
flowchart TD
  A[Cart Data] --> B[Checkout Page]
  B --> C[Login Block]
  B --> D[Billing Block]
  B --> E[Shipping Block]
  B --> F[Notes Block]
  B --> G[Coupon]
  B --> H[Shipping Method]
  B --> I[Payment Method]
  B --> J[Order Summary]
```

## 8. Luồng tab My Account

```mermaid
stateDiagram-v2
  [*] --> dashboard
  dashboard --> orders
  orders --> downloads
  downloads --> addresses
  addresses --> account_details
  account_details --> dashboard
```

## 9. Luồng tab chi tiết sản phẩm

```mermaid
stateDiagram-v2
  [*] --> Description
  Description --> AdditionalInformation
  AdditionalInformation --> Reviews
  Reviews --> Description
```

