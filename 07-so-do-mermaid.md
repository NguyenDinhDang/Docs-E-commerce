# Sơ đồ Mermaid — E-Commerce Frontend

---

## 1. Tổng quan luồng người dùng

```mermaid
flowchart TD
    User([Nguoi dung])

    User --> Home[Trang chu]
    Home --> Shop[Danh sach san pham]

    Shop --> QV[Quick View]
    Shop --> Detail[Chi tiet san pham]
    Shop --> WL[Wishlist]

    QV --> Cart[Them vao gio hang]
    Detail --> Cart
    Detail --> WL

    Cart --> CartPage[Trang gio hang]
    CartPage --> Checkout[Checkout]
    Checkout --> Account[My Account]
```

---

## 2. Kien truc he thong

```mermaid
flowchart LR
    subgraph Client["Trinh duyet"]
        direction TB
        User([Nguoi dung])

        subgraph NextJS["Next.js App Router"]
            UI[UI Components]
            LocalState[Local State / Tabs]
        end

        subgraph StateLayer["Zustand Stores"]
            CartStore[cartStore]
            WishStore[wishlistStore]
            QVStore[quickViewStore]
            AuthStore[authStore]
        end

        subgraph DataLayer["Du lieu tinh"]
            ShopData[shopData.ts]
            Images[public/images]
        end

        LS[(localStorage)]
    end

    User --> UI
    UI --> LocalState
    UI <--> StateLayer
    ShopData --> UI
    Images --> UI
    StateLayer <--> LS
```

---

## 3. Luong du lieu san pham

```mermaid
flowchart TD
    SD[("shopData.ts")]

    SD --> Home[Home — Featured Products]
    SD --> Listing[ShopWithSidebar — Listing]
    SD --> Gallery[ShopDetails — Gallery]
    SD --> QV[Quick View Modal]

    QV -->|set product| QVStore[useQuickViewStore]
    QVStore -->|doc product| Detail[ShopDetails Page]
    Detail -->|persist| LS[(localStorage — productDetails)]
    LS -->|hydrate khi reload| Detail
```

---

## 4. Luong gio hang

```mermaid
flowchart LR
    PC[Product Card / Quick View]

    PC -->|addItem| CS[useCartStore]
    CS <-->|persist / hydrate| LS[(localStorage — cart-storage)]

    CS --> CP[Cart Page]
    CS --> Modal[Cart Sidebar Modal]

    CP --> UQ[Cap nhat so luong]
    CP --> RM[Xoa san pham]
    CP --> CC[Xoa toan bo gio]
    CP --> Summary[Tong tien / So luong]
```

---

## 5. Luong Wishlist

```mermaid
flowchart LR
    Trigger[Product Card / Detail Page]

    Trigger -->|addItem| WS[useWishlistStore]
    WS <-->|persist / hydrate| LS[(localStorage — wishlist-storage)]
    WS --> WP[Wishlist Page]

    WP --> RM[Xoa san pham]
    WP --> Check[isInWishlist / getItemCount]
```

---

## 6. Luong Auth Demo

```mermaid
flowchart TD
    Form[Signin / Signup Form]

    Form -->|login hoac signup| AS[useAuthStore]
    AS --> Gen[Tao demo user]
    Gen <-->|persist / hydrate| LS[(localStorage — auth-storage)]

    LS --> MA[My Account]
    MA -->|updateProfile| AS
```

---

## 7. Luong Checkout

```mermaid
flowchart TD
    Cart[Cart Data — useCartStore]

    Cart --> CO[Checkout Page]

    CO --> Login[Login Block]
    CO --> Billing[Billing Details]
    CO --> Shipping[Shipping Info]
    CO --> Notes[Ghi chu don hang]
    CO --> Coupon[Coupon]
    CO --> ShipMethod[Phuong thuc van chuyen]
    CO --> Payment[Phuong thuc thanh toan]
    CO --> OrderSum[Order Summary]
```

---

## 8. Luong tab My Account

```mermaid
stateDiagram-v2
    [*] --> Dashboard

    Dashboard --> Orders
    Orders --> Downloads
    Downloads --> Addresses
    Addresses --> AccountDetails
    AccountDetails --> Dashboard

    Orders --> Dashboard
    Dashboard --> Addresses
```

---

## 9. Luong tab Chi tiet san pham

```mermaid
stateDiagram-v2
    [*] --> Description

    Description --> AdditionalInformation
    AdditionalInformation --> Reviews
    Reviews --> Description

    AdditionalInformation --> Description
    Description --> Reviews
```

---

## 10. Luong Build va Deploy

```mermaid
flowchart LR
    Src[Source Code]

    subgraph Dev["Development"]
        Src --> DevServer[npm run dev\nlocalhost:3000]
    end

    subgraph Build["Build"]
        Src --> BuildCmd[npm run build]
        BuildCmd --> OutDir[out/ — Static files]
    end

    subgraph Deploy["Deploy Targets"]
        Vercel[Vercel]
        Netlify[Netlify]
        GHP[GitHub Pages]
        Nginx[Nginx / Apache]
        S3[S3 + CloudFront]
    end

    OutDir --> Vercel
    OutDir --> Netlify
    OutDir --> GHP
    OutDir --> Nginx
    OutDir --> S3
```