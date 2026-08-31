# Shopify：Organization / FurnitureStore JSON-LD

完整逐步（Hyper／Pillar theme、先清社交空欄再取代 Organization）：[how-to-edit-schema.md](how-to-edit-schema.md)。

放喺現有 Organization 區塊（搜 `"@type": "Organization"`），**取代**舊 script，唔好再加第二份。產品頁 Product schema 唔好動。

**先 View Source 確認 theme 未有同樣 `@type":"Organization"`，避免重複。**  
地址／電話必須同 [nap-source-of-truth.md](nap-source-of-truth.md) 一致。社交 URL 換成真實官方頁。

產品頁嘅 Product schema 交俾 theme；呢份只補「公司 + 實體店」。

```liquid
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": ["Organization", "FurnitureStore", "HomeGoodsStore"],
  "@id": "{{ shop.url }}#organization",
  "name": "COLOURLIVING",
  "legalName": "B.S.C. COLOURLIVING LIMITED",
  "description": "COLOURLIVING is Hong Kong’s House of Brands for European furniture, lighting and bathroom, including faucets, baths and sanitary ware. Flagship at 333 Lockhart Road, Wan Chai. Delivery within Hong Kong.",
  "url": {{ shop.url | json }},
  "logo": {{ shop.brand.logo | image_url: width: 600 | prepend: "https:" | json }},
  "telephone": "+852-2295-6263",
  "email": "info@colourliving.com",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "333 Lockhart Road",
    "addressLocality": "Wan Chai",
    "addressRegion": "Hong Kong",
    "addressCountry": "HK"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 22.2783,
    "longitude": 114.1717
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],
      "opens": "10:00",
      "closes": "19:00"
    },
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": "Sunday",
      "opens": "12:00",
      "closes": "19:00"
    }
  ],
  "areaServed": {
    "@type": "Country",
    "name": "Hong Kong"
  },
  "knowsAbout": [
    "European furniture",
    "lighting",
    "bathroom fittings",
    "B&B Italia",
    "Flos",
    "Gessi",
    "Dornbracht"
  ],
  "image": [
    "https://colourliving.shop/cdn/shop/files/Colourliving_1F_Fukasawa_Setting_6c706d46-ff6e-484e-bd06-fad5a678b8c9.jpg",
    {{ shop.brand.logo | image_url: width: 1200 | prepend: "https:" | json }}
  ],
  "priceRange": "$$$$",
  "sameAs": [
    "https://www.facebook.com/colourliving.hk",
    "https://www.instagram.com/colourliving.hk/",
    "https://www.xiaohongshu.com/user/profile/6472fd56000000001c029135",
    "https://wa.me/85259217909"
  ]
}
</script>
```

經緯度請用 Google Maps 店舖標點核對後再改。`sameAs` 只放 **確實存在** 的官方檔案。

`FurnitureStore` 包傢俬陳列；`HomeGoodsStore` 包浴室／燈／家居。兩個一齊放。可見定位段唔好隱藏：[homepage-positioning.md](homepage-positioning.md)。

---

## Rich Results 話 miss postalCode / priceRange / image

多數係 **Recommended**，唔係必填。黃燈唔等於 Local business 無效。

| 欄 | 點做 |
| --- | --- |
| **postalCode** | 香港 **無郵政編碼**。唔好填 `00000`、`999077` 或 `""`。呢欄唔寫。測試會繼續提，可忽略。只當 GBP 有填碼先抄同一個。 |
| **priceRange** | `"priceRange": "$$$$"`。呢度 **唔係** 港幣四蚊，亦唔係貨價。Google／schema 用 `$`–`$$$$` 表示相對檔次：`$` 平、`$$` 中、`$$$` 貴、`$$$$` 頂級。COLOURLIVING 歐洲旗艦用 `$$$$`。 |
| **image** | 要店的圖，單有 `logo` 唔夠。加陳列室實拍 HTTPS（約 192px+）。 |

你而家 live JSON：`knowsAbout` 嘅 `]` 同 `"sameAs"` 之間 **漏咗逗號**，整段可能 parse 唔完整。補逗號，並加：

```json
  ],
  "image": [
    "https://colourliving.shop/cdn/shop/files/Colourliving_1F_Fukasawa_Setting_6c706d46-ff6e-484e-bd06-fad5a678b8c9.jpg"
  ],
  "priceRange": "$$$$",
  "sameAs": [
```

圖可換成其他 `cdn/shop/files/` 店面相。Save 後再測主頁。

---

## 點解第一稿冇 `knowsAbout`／`hasOfferCatalog`

唔係漏欄。第一稿只做 Google Local **會用來出結果的欄**：類型、NAP、時間、`sameAs`。下面兩欄 **Rich Results Test／地圖唔靠佢哋**。

| | `knowsAbout` | `hasOfferCatalog` |
| --- | --- | --- |
| Schema 意思 | 呢間店「識／關於」咩題 | 呢間店「賣緊」一個目錄 |
| Google 搜尋 | 唔係 Local business 必填，多數忽略 | 唔取代 PDP 的 Product；唔入 Merchant 購物結果 |
| GEO | AI **有時**當提示（Gessi、浴室） | 理論上可連去 collection URL；多數模型仍讀可見頁同 `/llms.txt` |
| 風險 | 品牌名單過長、過期、同畫面對唔上，似塞詞 | 寫 2000 隻 SKU 一定過期；同 Product schema 重複 |

所以順序係：先令機械知 **邊間店、喺邊、咩類型**。品牌同貨盤的正經來源係 **collection／PDP** 同 **llms.txt**，唔係 Organization 一篇目錄。

而家 NAP 已上，**可以加薄的一層**（仍然唔好當品牌百科）：

**A. `knowsAbout`（建議加）** — 品類 + 定位段嗰幾個品牌，十個位以內：

```json
"knowsAbout": [
  "European furniture",
  "lighting",
  "bathroom fittings",
  "B&B Italia",
  "Flos",
  "Gessi",
  "Dornbracht"
]
```

放喺 `sameAs` 前面。有新主力品牌先加；Roca display、全 catalog 唔入。

**B. `hasOfferCatalog`（可選、更薄）** — 三個部門連去現有 collection，**唔列產品**：

```json
"hasOfferCatalog": {
  "@type": "OfferCatalog",
  "name": "COLOURLIVING",
  "itemListElement": [
    {
      "@type": "OfferCatalog",
      "name": "Furniture",
      "url": "https://colourliving.shop/collections/furniture"
    },
    {
      "@type": "OfferCatalog",
      "name": "Lighting",
      "url": "https://colourliving.shop/collections/lighting"
    },
    {
      "@type": "OfferCatalog",
      "name": "Bathroom",
      "url": "https://colourliving.shop/collections/bathroom-faucet"
    }
  ]
}
```

**唔好：** 為每個 SKU 寫 Offer；同 Product JSON-LD 再抄一次價錢。貨喺 PDP schema + GMC。

改完仍然只得 **一份** Organization。測主頁 Rich Results：Local business 唔應因為加咗呢兩欄而壞。
