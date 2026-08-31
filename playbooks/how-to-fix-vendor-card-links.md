# 產品卡品牌連去 `/collections/vendors?q=` 點改

## 點解你撳產品卡會覺得「全部去 PDP」

**圖同產品名**（`h3.product-card__title`）**已經正確**去 `/products/...`。你 check 嗰啲 link 冇錯。

`/collections/vendors?q=` **唔喺圖、唔喺標題**。佢係標題 **上面** 一行細字品牌名（class `product-card__vendor`），Hyper 用 `reversed-link`：**平時無底線，好似淨係 label，hover 先有底線**。右鍵嗰個字「Flos」／「B&B Italia」（唔好右鍵張相）→ Copy link，先見到 `vendors?q=`。

View Source / 開發者工具搜 `vendors?q=` 亦會中。2026-08-31 再抓：主頁 3 條；`/collections/gessi` 每張卡都有（15 條）；Flos PDP 品牌名 1 條。

**優先極低。** 客人撳相買嘢唔受影響。只影響撳品牌細字會去弱 vendor 搜尋頁，而唔係 `/collections/flos`。唔急、可以當 backlog。

---

## 喺邊（畫面）

**唔係**「Haute Living Brands」logo 牆（嗰啲已經去 `/collections/gessi` 等）。

係首頁 **Where Every Room Tells a Story**（「Tap into each space…」）右邊三張產品卡，**價錢上面、產品名上面嗰行細字品牌**：

| 卡 | 你見到 | 而家 href |
| --- | --- | --- |
| 燈 | FLOS | `/collections/vendors?q=Flos` |
| 梳化椅 | B&B ITALIA | `/collections/vendors?q=B%26B%20Italia` |
| 床 | B&B ITALIA | 同上 |

產品 **標題** 已經去正確 PDP。問題只係 **品牌細字**。

同一套 product card 用喺 collection／搜尋，所以 Fix 一次，全站卡都會跟。

---

## 點解 Customize 改唔到呢條

Hyper 產品卡用 Shopify 的 `product.vendor | url_for_vendor`，**永遠**生成 `/collections/vendors?q=品牌名`。  
呢個唔係 Products bundle 入面可以揀的「Brand URL」。換三隻產品都一樣。

---

## 做法 A（推薦）：改 theme 一句 vendor 連結

Duplicate theme → **⋯ → Edit code** → 搜：

```
url_for_vendor
```

或搜 `product-card__vendor`／`Vendor:`。

典型會似：

```liquid
<a href="{{ product.vendor | url_for_vendor }}">{{ product.vendor }}</a>
```

換成（handle 同你們已有品牌 collection 對得上：`flos`、`b-b-italia`）：

```liquid
<a href="/collections/{{ product.vendor | handleize }}">{{ product.vendor }}</a>
```

Save → Preview 撳 FLOS，網址應係 `/collections/flos` 而唔係 `vendors?q=`。

若某品牌未開 collection，handleize 會 404。可加 fallback：

```liquid
{% assign vendor_collection = collections[product.vendor | handleize] %}
{% if vendor_collection %}
  <a href="{{ vendor_collection.url }}">{{ product.vendor }}</a>
{% else %}
  <span>{{ product.vendor }}</span>
{% endif %}
```

**只改 vendor 那條 `<a>`。** 唔好改產品標題的 `/products/...`。

---

## 做法 B：唔顯示品牌細字

Customize → Theme settings → Product card → 關閉 **Show vendor**（名可能係 Vendor / Brand）。  
GEO 弱少少（卡上看唔到品牌），但唔會再推弱 `vendors?q=` 頁。

---

## 唔好做

唔好逐張卡喺 Products bundle 搵 Brand URL——無呢欄。  
唔好改 Haute Living Brands 的 logo 連（已經啱）。
