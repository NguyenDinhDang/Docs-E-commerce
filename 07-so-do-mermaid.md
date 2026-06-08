# Sơ đồ Mermaid — E-Commerce Frontend

---

## 1. Tổng quan luồng người dùng

```mermaid
flowchart TD
    User([👤 Người dùng])

    User --> Home[🏠 Trang chủ]
    Home --> Shop[📦 Danh sách sản phẩm]

    Shop --> QV[🔍 Quick View]
    Shop --> Detail[📄 Chi tiết sản phẩm]
    Shop --> WL[❤️ Wishlist]

    QV --> Cart[🛒 Thêm vào giỏ]
    Detail --> Cart
    Detail --> WL

    Cart --> CartPage[🛒 Trang giỏ hàng]
    CartPage --> Checkout[💳 Checkout]
    Checkout --> Account[👤 My Account]

    style User fill:#f0f4ff,stroke:#4a6fa5,color:#1a2e4a
    style CartPage fill:#fff7e6,stroke:#d48806,color:#7c4a00
    style Checkout fill:#fff7e6,stroke:#d48806,color:#7c4a00
    style Account fill:#f6ffed,stroke:#52c41a,color:#135200
    style WL fill:#fff0f6,stroke:#eb2f96,color:#780650
```

---

## 2. Kiến trúc hệ thống

```mermaid
flowchart LR
    subgraph Client["🖥️ Trình duyệt"]
        direction TB
        User([👤 Người dùng])
        subgraph NextJS["Next.js App Router"]
            UI[UI Components]
            LocalState[Local State\nuseState / tabs]
        end
        subgraph StateLayer["Zustand Stores"]
            CartStore[cartStore]
            WishStore[wishlistStore]
            QVStore[quickViewStore]
            AuthStore[authStore]
        end
        subgraph DataLayer["Dữ liệu"]
            ShopData[shopData.ts\nStatic product data]
            Images[/public/images/]
        end
        LS[(localStorage\npersisted state)]
    end

    User --> UI
    UI --> LocalState
    UI <--> StateLayer
    ShopData --> UI
    Images --> UI
    StateLayer <--> LS

    style Client fill:#fafafa,stroke:#d9d9d9
    style NextJS fill:#e6f7ff,stroke:#1890ff
    style StateLayer fill:#fff7e6,stroke:#fa8c16
    style DataLayer fill:#f6ffed,stroke:#52c41a
    style LS fill:#f9f0ff,stroke:#722ed1
```

---

## 3. Luồng dữ liệu sản phẩm

```mermaid
flowchart TD
    SD[("📁 shopData.ts\nNguồn dữ liệu sản phẩm")]

    SD --> Home[🏠 Home\nFeatured Products]
    SD --> Listing[📋 ShopWithSidebar\nProduct Listing]
    SD --> Gallery[🖼️ ShopDetails\nImage Gallery]
    SD --> QV[🔍 Quick View Modal]

    QV -->|set product| QVStore[useQuickViewStore]
    QVStore -->|đọc product| Detail[📄 ShopDetails Page]
    Detail -->|persist| LS[(localStorage\nproductDetails)]
    LS -->|hydrate khi reload| Detail

    style SD fill:#e6f7ff,stroke:#1890ff,color:#003a8c
    style QVStore fill:#fff7e6,stroke:#fa8c16,color:#7c4a00
    style LS fill:#f9f0ff,stroke:#722ed1,color:#391085
```

---

## 4. Luồng giỏ hàng

```mermaid
flowchart LR
    PC[🛍️ Product Card\nhoặc Quick View]

    PC -->|addItem| CS[useCartStore]

    CS <-->|persist / hydrate| LS[(localStorage\ncart-storage)]

    CS --> CP[🛒 Cart Page]
    CS --> Modal[🪟 Cart Sidebar\nModal]

    CP --> UQ[✏️ Cập nhật\nsố lượng]
    CP --> RM[🗑️ Xoá\nsản phẩm]
    CP --> CC[❌ Xoá toàn\nbộ giỏ]
    CP --> Summary[💰 Tổng tiền\n& số lượng]

    style CS fill:#fff7e6,stroke:#fa8c16,color:#7c4a00
    style LS fill:#f9f0ff,stroke:#722ed1,color:#391085
    style CP fill:#e6f7ff,stroke:#1890ff,color:#003a8c
```

---

## 5. Luồng Wishlist

```mermaid
flowchart LR
    Trigger[🛍️ Product Card\nhoặc Detail Page]

    Trigger -->|addItem| WS[useWishlistStore]
    WS <-->|persist / hydrate| LS[(localStorage\nwishlist-storage)]
    WS --> WP[❤️ Wishlist Page]

    WP --> RM[🗑️ Xoá sản phẩm]
    WP --> Check[✅ isInWishlist\n& getItemCount]

    style WS fill:#fff7e6,stroke:#fa8c16,color:#7c4a00
    style LS fill:#f9f0ff,stroke:#722ed1,color:#391085
    style WP fill:#fff0f6,stroke:#eb2f96,color:#780650
```

---

## 6. Luồng Auth Demo

```mermaid
flowchart TD
    Form[📝 Signin / Signup Form]

    Form -->|login hoặc signup| AS[useAuthStore]
    AS --> Gen[⚙️ Tạo demo user\nkhông xác thực thật]
    Gen <-->|persist / hydrate| LS[(localStorage\nauth-storage)]

    LS --> MA[👤 My Account]
    MA -->|updateProfile| AS

    style AS fill:#fff7e6,stroke:#fa8c16,color:#7c4a00
    style LS fill:#f9f0ff,stroke:#722ed1,color:#391085
    style Gen fill:#fff1f0,stroke:#f5222d,color:#820014
    style MA fill:#f6ffed,stroke:#52c41a,color:#135200
```

---

## 7. Luồng Checkout

```mermaid
flowchart TD
    Cart[🛒 Cart Data\nfrom cartStore]

    Cart --> CO[💳 Checkout Page]

    CO --> Login[🔐 Login Block\ndemo auth]
    CO --> Billing[📋 Billing Details]
    CO --> Shipping[🚚 Shipping Info]
    CO --> Notes[📝 Ghi chú\nđơn hàng]
    CO --> Coupon[🏷️ Coupon]
    CO --> ShipMethod[📦 Phương thức\nvận chuyển]
    CO --> Payment[💳 Phương thức\nthanh toán]
    CO --> OrderSum[🧾 Order Summary]

    style Cart fill:#fff7e6,stroke:#fa8c16,color:#7c4a00
    style CO fill:#e6f7ff,stroke:#1890ff,color:#003a8c
    style OrderSum fill:#f6ffed,stroke:#52c41a,color:#135200
```

---

## 8. Luồng tab My Account

```mermaid
stateDiagram-v2
    [*] --> Dashboard : vào trang

    Dashboard --> Orders : xem đơn hàng
    Orders --> Downloads : nội dung tải về
    Downloads --> Addresses : quản lý địa chỉ
    Addresses --> AccountDetails : chỉnh thông tin
    AccountDetails --> Dashboard : quay về tổng quan

    Dashboard --> Addresses : truy cập nhanh
    Orders --> Dashboard : quay lại
```

---

## 9. Luồng tab Chi tiết sản phẩm

```mermaid
stateDiagram-v2
    [*] --> Description : mặc định

    Description --> AdditionalInfo : xem thêm thông số
    AdditionalInfo --> Reviews : xem đánh giá
    Reviews --> Description : quay lại mô tả

    Description --> Reviews : nhảy thẳng
    AdditionalInfo --> Description : quay lại
```

---

## 10. Luồng Build & Deploy

```mermaid
flowchart LR
    subgraph Dev["💻 Development"]
        Src[Source Code\nNext.js + React + TS]
        Dev2[npm run dev\nlocalhost:3000]
        Src --> Dev2
    end

    subgraph Build["⚙️ Build"]
        Src2[npm run build]
        Out[/out/ \nStatic HTML/CSS/JS]
        Src2 --> Out
    end

    subgraph Deploy["🚀 Deploy Targets"]
        Vercel[Vercel]
        Netlify[Netlify]
        GHP[GitHub Pages]
        Nginx[Nginx / Apache]
        S3[S3 + CloudFront]
    end

    Src --> Src2
    Out --> Vercel
    Out --> Netlify
    Out --> GHP
    Out --> Nginx
    Out --> S3

    style Dev fill:#e6f7ff,stroke:#1890ff
    style Build fill:#fff7e6,stroke:#fa8c16
    style Deploy fill:#f6ffed,stroke:#52c41a
```