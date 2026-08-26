# 點樣改 Shopify Schema（步驟 + 可貼內容）

## 停：根本冇一個叫 `ld+json` 嘅檔

你喺 Edit code **搵唔到 `ld+json` 呢個檔案，係正常。** Shopify **從來都唔會** 有一個 file 名叫：

- `ld+json`
- `ld+json.liquid`
- `application-ld-json.liquid`

`application/ld+json` 只係 HTML 裏面一句標籤：

```html
<script type="application/ld+json">
  { "@type": "Organization", ... }
</script>
```

呢段文字 **藏喺某個 `.liquid` 檔的內容入面**（多數係 `layout/theme.liquid` 或 `snippets/` 某個 seo／meta／social 檔），唔係獨立檔名。

**Edit code 左上個搜尋盒，有時只搜檔名。** 所以你打 `ld+json` 會 0 結果。要改做：

1. 打開 **`layout/theme.liquid`**（檔名就叫呢個，一定有）
2. 檔入面 `Ctrl+F` / `Cmd+F` 搜：`sameAs` 或 `ld+json` 或 `Organization`
3. 若 `theme.liquid` 冇：逐個打開 `snippets/` 裏面檔名有 `seo`、`meta`、`head`、`social` 的，每個檔入面再 `Ctrl+F`
4. 仍然 0：Themes → ⋯ → **Download theme file**，解壓後用電腦搜尋資料夾內容 `sameAs`（一定搵到，因為網站原始碼已經有呢段）

**搵唔到都唔使停。** Duplicate theme → 打開 `layout/theme.liquid` → 搜 `</head>` → **喺佢上一行**貼本檔第二部份嗰整段 FurnitureStore `<script>`。Google 會讀到灣仔地址。舊嗰份瘦 Organization 之後再刪。

---

## 停：Edit code 搜 `schema` 會搵錯嘢

Shopify 入面 **「schema」有兩個完全唔同的意思**：

| 你搜 `schema` 見到的 | 真正係咩 | 同 Google SEO 有冇關 |
| --- | --- | --- |
| `{% schema %} { "name": "Header", "settings": [ ... ] } {% endschema %}` | Theme 區塊的 **後台設定表**（Customize 那些顏色、勾選） | **無關**。一大堆 default 係正常，**唔好改呢啲** |
| `<script type="application/ld+json"> { "@type": "Organization" ...}` | **JSON-LD**：寫俾 Google／AI 讀「呢間店係邊、貨幾錢」 | **有關**。我講的 schema 問題係呢舊 |

所以你喺 Edit code 搜 `schema` 見到 Header／Product section 的 settings JSON，**唔係我講嗰個問題**，亦唔使「改善」那些 default。

### 正確第一步：喺 **網站** 睇，唔係喺 theme 盲搜

1. 無痕開 https://colourliving.shop/  
2. 右鍵 → **查看網頁原始碼**  
3. 搜：`application/ld+json` 或 `@type`  
4. 你會見到而家實際輸出（呢個先係「問題」）：

```json
{
  "@type": "Organization",
  "name": "COLOURLIVING",
  "logo": "https://colourliving.shop/cdn/shop/files/COLOURLIVING_LOGO2.png?...",
  "sameAs": ["", "https://www.facebook.com/colourliving.hk", "", "https://www.instagram.com/colourliving.hk/", "", "https://wa.me/85259217909", "", "", "小紅書..."],
  "url": "https://colourliving.shop"
}
```

**問題用白話講：**

1. Google 知你叫 COLOURLIVING、有 logo、有幾個社交。  
2. **唔知** 你喺灣仔洛克道、電話、營業時間、係傢俬店。  
3. `sameAs` 夾住好多 `""`（空社交欄），等於無效連結。  
4. 產品頁另外有一份 Product（價錢 HKD）——**呢份合格，唔好郁。**

Edit code 要搵呢段時，搜 **檔案內容**，唔係搵一個叫 `ld+json` 嘅檔名。  
**冇** `ld+json.liquid` 呢個 file。佢藏喺某個 `.liquid` 入面，可能仲拆開幾行。

喺 Edit code **左上搜尋盒** 逐個試（要搜 **內容**，唔係只過濾檔名）：

1. `sameAs` ← Hyper 最易中  
2. `schema.org`  
3. `Organization`  
4. `application/ld+json`

請打開這些檔逐個 `Ctrl+F`（唔好靠左邊檔案列表名叫 schema）：

- `layout/theme.liquid`
- `layout/theme.pagefly.liquid`（如有）
- `snippets/` 入面所有檔名有 `meta`、`head`、`seo`、`social`、`json`、`schema` 的（呢度的 schema 有時係 JSON-LD，有時係設定表，打開睇有冇 `ld+json`）
- `sections/header.liquid`

若搜尋盒只搜檔名、搜唔到內容：用瀏覽器下載 theme（Themes → ⋯ → **Download theme file**），解壓後用電腦「在資料夾中搜尋」`sameAs`。

### 搵唔到都可以加地址（備案）

唔好無限搵檔。Duplicate theme 後，打開 **`layout/theme.liquid`**，搵 `</head>`，**喺佢前面**貼上 [how-to-edit-schema.md](how-to-edit-schema.md) 第二部份嗰整段 FurnitureStore `<script>`。

缺點：網站可能短暫有 **兩份** Organization（舊瘦嘅 + 新完整嘅）。Google 通常仍讀到地址；之後用下載 theme 搜 `sameAs` 再刪舊嗰份就得。  
**仍然唔好** 再加 Product script。

---

### 喺 backend 點 walk 到（唔經「搜 schema」）

**A. 先唔開 Edit code（見到問題本體）**

1. Shopify 左邊唔使撳。用 Chrome 開 https://colourliving.shop/  
2. View Source → 搜 `ld+json`  
3. 第一個 script 就係 Organization。對住上面 JSON 睇缺地址、空 sameAs。

**B. 改空 sameAs（Theme 設定，仍然唔使 code）**

1. Admin → **Online Store → Themes → Customize**  
2. 左下角 **齒輪 Theme settings**  
3. 開 **Social media**（或 Social accounts）  
4. 清空所有冇連結的欄；只留 Facebook／Instagram／小紅書／WhatsApp  
5. Save → 再 View Source 睇 `sameAs` 仲有冇 `""`

**C. 先至 Edit code（要加地址先入呢步）**

1. Themes → Duplicate → **Edit code**  
2. 左上 **搜尋檔案** 打：`ld+json`（唔好打 schema）  
3. 打開含 `"@type": "Organization"` 的檔（常見 `layout/theme.liquid` 或 `snippets/` 底下 meta／head）  
4. **只改嗰一個 Organization 的 `<script>...</script>`**  
5. 下面 `"@type": "WebSite"` 同產品檔裡的 Product **唔好刪**

然後先做下面「第一部份」清社交；再做「第二部份」貼上完整 FurnitureStore JSON。

---

你用緊 theme：**Hyper（Preset：Pillar Beige v1.4.0）**。  
要改的係 **公司／店舖身份**，**唔好改、唔好再加一份 Product**。

---

## 你要改咩、唔好改咩

| 項目 | 而家 | 你要做 |
| --- | --- | --- |
| Product（價錢、HKD、brand、sku） | 合格 | **唔郁**。唔好裝 JSON-LD app |
| WebSite + SearchAction | 合格 | **留住** |
| Organization | 只有名、logo、url、殘缺 sameAs | **擴充／取代呢一份** |
| sameAs 空字串 `""` | Facebook／IG／WhatsApp／小紅書之間夾住空白 | 清 Theme 社交空欄，或改 Liquid 唔輸出空 URL |
| 地址、電話、營業時間、FurnitureStore | **完全冇** | 寫入 Organization |
| shippingDetails 黃燈 | Shopify 預設冇 | **唔使改 schema**；去 Merchant Center 填運費／退貨 |

目標：全站只得 **一個** Organization，類型包含店舖，官方 URL 永遠係 `https://colourliving.shop`（唔好用 About 頁自己的 URL）。

---

## 第一部份：唔使改 code（先做，5 分鐘）

空 `sameAs` 多數因為 Theme 把 Twitter、YouTube、LinkedIn 等 **空欄都印出嚟**。

1. **Online Store → Themes → Customize**
2. 左下 **Theme settings**（齒輪）
3. 搵 **Social media** / **Social accounts**
4. **只留有真實連結的欄：**
   - Facebook：`https://www.facebook.com/colourliving.hk`
   - Instagram：`https://www.instagram.com/colourliving.hk/`
   - WhatsApp：`https://wa.me/85259217909`（若有呢欄）
   - 小紅書：`https://www.xiaohongshu.com/user/profile/6472fd56000000001c029135`
5. Twitter / X、TikTok、Pinterest、YouTube、LinkedIn、Vimeo：**刪到空白**（唔好填 `#` 或空格）
6. Save

另外：

1. **Settings → Store details**
2. 填地址：`333 Lockhart Road, Wan Chai, Hong Kong`
3. 電話：`+852 2295 6263`  
   （Theme 未必自動入 schema，但 footer／其他 app 會用呢份）

核對：無痕開首頁 → View Source → 搜 `sameAs` → 應該 **冇** `""`。

呢步只修空連結。**地址仍然要第二部份先入到 schema。**

---

## 第二部份：改 Organization 內容（要 Edit code）

### Step 1 — 複製 theme

Themes → 現行 **Pillar** → **⋯ → Duplicate**。喺副本改。

### Step 2 — 搵而家嗰段 Organization

1. 副本 → **⋯ → Edit code**
2. 左上搜尋（Search files）打：

   ```
   "@type": "Organization"
   ```

   或

   ```
   application/ld+json
   ```

3. Hyper／Pillar 常見位置（你會喺其中一個見到同網站一樣的 `sameAs` 陣列）：
   - `layout/theme.liquid`
   - `snippets/meta-tags.liquid`
   - `snippets/head.liquid`
   - `snippets/schema.liquid`
   - `layout/theme.pagefly.liquid`（若有，都要一齊改或唔用）

4. 你應見到類似：

```liquid
<script type="application/ld+json">
  {
    "@context": "http://schema.org",
    "@type": "Organization",
    "name": "...",
    "logo": "...",
    "sameAs": [ ... ],
    "url": "..."
  }
</script>
```

**只改呢一個 Organization 區塊。** 下面果個 `"@type": "WebSite"` **唔好刪。**  
產品 template 裡的 Product JSON-LD **唔好刪。**

### Step 3 — 用下面整段取代 Organization 嗰個 `<script>...</script>`

喺外部編輯器（VS Code / 記事本）貼好，再貼入 Shopify，避免 Admin 自動轉成彎引號。

```liquid
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": ["Organization", "FurnitureStore"],
  "@id": {{ shop.url | append: '#organization' | json }},
  "name": "COLOURLIVING",
  "legalName": "B.S.C. COLOURLIVING LIMITED",
  "url": {{ shop.url | json }},
  "logo": {
    "@type": "ImageObject",
    "url": {{ shop.brand.logo | image_url: width: 600 | prepend: 'https:' | json }}
  },
  "image": {{ shop.brand.logo | image_url: width: 600 | prepend: 'https:' | json }},
  "telephone": "+852-2295-6263",
  "email": "info@colourliving.com",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "333 Lockhart Road",
    "addressLocality": "Wan Chai",
    "addressRegion": "Hong Kong",
    "postalCode": "",
    "addressCountry": "HK"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 22.2779,
    "longitude": 114.1774
  },
  "hasMap": "https://maps.google.com/?q=333+Lockhart+Road+Wan+Chai+Hong+Kong",
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
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
  "currenciesAccepted": "HKD",
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

**寫死 `sameAs` 的原因：** 唔再靠 theme 空欄。若你之後加 YouTube／LinkedIn，喺呢個陣列加多一條完整 `https://...` URL，逗號要啱（最後一條後面冇逗號）。

**經緯度：** 用 Google Maps 搵「333 Lockhart Road, Wan Chai」→ 右鍵座標核對後改 `latitude` / `longitude`。上面係灣仔洛克道附近約數。

**公眾假期：** Schema 冇「假期」欄；Sunday 已用 12:00–19:00。假期同周日一致就唔使加。

### Step 4 — 確認 Organization 的 url 用 `shop.url`

若你舊 code 係：

```liquid
"url": "{{ canonical_url }}"
```

About 頁會變成公司官方 URL = About。新稿用 `{{ shop.url | json }}`，每頁都係店根網址。

### Step 5 — Save → Preview 核對

副本 Preview 開首頁，View Source，搜 `FurnitureStore`。應見到地址 `333 Lockhart Road`，sameAs **冇** `""`。

再開一個產品頁：應 **仍然有** Product schema（價錢），**另外** 有你份 Organization。總共大約 2 個 `ld+json`（產品頁）或 2 個（首頁 Organization + WebSite）。

**唔好** 出現兩個 `"@type": "Organization"`。若有兩個，即係你加多咗、舊嗰份冇刪。

### Step 6 — Publish 後用 Google 測

1. https://search.google.com/test/rich-results  
   貼 `https://colourliving.shop/`  
   睇 Organization／Local business 有冇地址錯誤
2. 再貼一隻產品 URL  
   Product 必須仍然 **Valid**
3. https://validator.schema.org/ 貼同一頁原始碼（可選）

GSC 可能仍報缺 `shippingDetails` → 忽略，去 Merchant Center 填香港運送／退貨。

---

## 若搜尋搵唔到 Organization 區塊

Hyper 有時把 JSON 拆咗喺 snippet。Edit code 搜 `sameAs`，改嗰個 loop：

**唔好：**

```liquid
"sameAs": [
  "{{ settings.social_twitter }}",
  "{{ settings.social_facebook }}"
]
```

空設定會出 `""`。

**改成（若你想保留 theme 設定、唔寫死）：**

```liquid
"sameAs": [
  {%- assign social_links = "" | split: "" -%}
  {%- if settings.social_facebook != blank -%}
    {%- assign social_links = social_links | push: settings.social_facebook -%}
  {%- endif -%}
```

`push` 喺 Shopify Liquid **唔一定有**。最穩係用上面 Step 3 **寫死四條真實 URL**，同第一部份清空欄一齊做。

---

## 產品 schema：真係要改先睇呢度

**而家唔建議改 Product JSON-LD。**

若將來要加廠方型號 `mpn`：

1. 產品後台 **SKU／Barcode** 填廠方型號（例如 `LY153`、`3502097090`）
2. 先唔改 Liquid；部分 theme 會自動讀 barcode 做 gtin（**冇 GTIN 唔好亂填 barcode**）
3. 真要 `mpn`：喺產品 template 搜 `"sku"`，喺隔離加  
   `"mpn": {{ product.selected_or_first_available_variant.sku | json }}`  
   只加欄位進 **現有** Product 物件，唔好再貼多一個 `<script type="application/ld+json">` Product

---

## 完成檢查清單

- [ ] Theme settings 空社交欄已清空
- [ ] 全站只有 **一個** Organization script
- [ ] `@type` 含 `FurnitureStore`
- [ ] `url` 係 `https://colourliving.shop`（About 頁都係）
- [ ] `sameAs` 冇 `""`
- [ ] 產品頁 Product 仍然有效
- [ ] Rich Results Test 首頁通過
- [ ] 冇新裝 SEO schema app
