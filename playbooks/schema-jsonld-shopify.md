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

驗證：https://search.google.com/test/rich-results 貼首頁 URL。
