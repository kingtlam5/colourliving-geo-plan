# 09 — 執行 FAQ：域名、Canonical、NAP、Schema、Sitemap、hreflang、Local SEO

對應你提出的實操問題。2026-08-26 用公開 HTTP 覆核過現況。Vendor 要唔要改網址見第 9 題。

---

## 1. 點樣 audit 已關三年、冇 CMS 的 colourliving.com？

**係，GSC 係最準的「Google 而家仲當邊啲 URL 存在」來源。** 冇 CMS 唔等於冇得盤點。你要盤的唔係「舊站而家有咩頁」（多數已死），而係「Google／互聯網仲記得邊啲 URL」。

### 而家公開見到嘅狀態（重要）

| URL | 實際行為 |
| --- | --- |
| `https://colourliving.com/` | **302** 去 `https://colourliving.shop`（只去首頁，唔帶路徑） |
| `https://www.colourliving.com/` | 同樣 **302** 去 `.shop` 首頁 |
| `https://colourliving.com/pages/about-us` 等內頁 | **404** |

即係：根網址已經有轉址，但係 **臨時 302、唔保留路徑**。內頁 404。  
**2026-08-26 覆核：** `site:colourliving.com` 同新加嘅 GSC 都顯示 **幾乎冇內頁索引**——舊 catalog 已退出 Google。而家 SEO 優先係把首頁 **302 改 301**，唔係以為仲有幾百頁喺度搶排名。詳情：[colourliving-com-current-index.md](../playbooks/colourliving-com-current-index.md)。

### 盤點來源（由準到粗）

**A. Google Search Console（首選）**

即使舊站關咗，而家加 `colourliving.com` 的 Domain property **可以完全空白**——唔一定係故障。`.shop` 加 GSC 即日有數，係因為 Google 已爬咗兩個月；`.com` 索引裡幾乎冇內頁。新 property 圖表仍可能要 1–3 日；等完預期仍係 0 已編入索引，或首頁列入「有重新導向」。用 **URL 檢查** 即時睇 `https://colourliving.com/`。

1. 去 [Google Search Console](https://search.google.com/search-console)
2. 加 property：優先 **Domain** `colourliving.com`（要驗證 DNS TXT，你有 domain login 就做得到）
3. 開 **網頁索引 → 網頁**，匯出「已編入索引」同「錯誤／404」
4. 開 **成效**，日期拉到最長（16 個月），匯出查詢同頁面  
   關站三年後，成效數據可能好少；**索引報告仍然有用**
5. 用 **URL 檢查** 抽幾條舊品牌／浴室 URL，睇 Google 最後一次爬到咩

若公司從來未開過 `.com` 的 GSC：而家加仍然值得，用來睇殘留 404 同之後 301 有冇被收錄。

**B. Google 自己搜**

瀏覽器搜：

```
site:colourliving.com
```

把出現的 URL 複製落試算表。再試：

```
site:colourliving.com/products
site:colourliving.com/collections
site:www.colourliving.com
```

**C. Wayback Machine（還原舊路徑結構）**

開 https://web.archive.org/web/*/colourliving.com/*  
睇關站前最後一年的快照：分類、品牌、產品 handle。唔使還原內容，只要 **舊路徑清單**。

**D. 其他**

- Bing Webmaster（若有）
- 舊報價 PDF、電郵簽名、品牌商 Where to buy 列出的舊 URL
- Ahrefs / Semrush 的「歷史頁面」（有訂閱先）

### 產出

一個試算表，欄位：

`old_url | last_seen | indexed_y/n | new_shop_url | redirect_type | priority`

Priority 只標：首頁、About、Contact、Gessi／B&B／Bath／Furniture 等品牌與品類。三年前的過時 SKU 大多數 **301 去對應品牌 collection 或 `/collections/bathroom`**，唔使逐隻對。

冇 CMS **唔阻** 呢步。阻你的係有冇 GSC／DNS 驗證權，而唔係有冇 Magento 後台。

---

## 2. 得返 colourliving.com 的 domain login，點樣 redirect？

**唔需要舊 CMS。** Redirect 發生在「訪客打舊網址 → DNS／轉址服務 → 新站」，同 Magento 無關。

長遠若 management 想 `.com` 做品牌站、`.shop` 做電商：品牌站未有內容前仍然應 301。可 disconnect 再開品牌站。階段計劃見 [10-domains-canonical-schema.md](10-domains-canonical-schema.md)。

你而家已經有一層轉址，但有三個問題：用緊 **302**、**只轉首頁**、內頁 **404**。目標改成 **301 永久**，並且處理路徑。而家 DNS 似註冊商 Forwarding，唔係 Shopify IP——見 [wayback-and-www.md](../playbooks/wayback-and-www.md)。

`colourliving.com` 同 `www.colourliving.com` **唔係兩個註冊域名**，但係兩個 hostname，**兩個都要** redirect 去 `.shop`。Shopify Connect `colourliving.com` 一次，DNS 同時改 `@` 同 `www`。

### 方案 A（最啱 Shopify，優先試）

把 `.com` **加進而家間 Shopify 店** 做額外網域，再設做「重新導向至主要網域」。

1. Shopify Admin → **Settings → Domains → Connect existing domain**
2. 輸入 `colourliving.com` 同 `www.colourliving.com`
3. 依指示改 DNS（通常 A 記錄指向 Shopify，或 CNAME `www`）
4. 主要網域保持 **`colourliving.shop`**
5. `.com` 選 **Redirect to primary domain**

Shopify 會對已連接網域做 **301**，並且多數會 **保留路徑**：

`colourliving.com/collections/gessi` → `colourliving.shop/collections/gessi`

注意：舊 Magento 路徑同新 Shopify handle **多數唔同**，所以「保留路徑」之後，舊 URL 可能變成 `.shop` 上的 404。呢個時候要喺 Shopify 開 **URL redirects**：

**Online Store → Navigation → URL Redirects**（或 Settings → Apps and sales channels → Online Store → URL redirects）

例：

| Redirect from | Redirect to |
| --- | --- |
| `/bath-spa` | `/collections/bathroom` |
| `/gessi` | `/collections/gessi` |

你可以 CSV 匯入大量舊路徑。呢步先要有第 1 題的 URL 清單。

DNS 改完要等 TTL（常見 5 分鐘–48 小時）。

### 方案 B（DNS 得、但唔想把 `.com` 接去 Shopify）

用 **Cloudflare**（免費）：把 `.com` nameserver 指去 Cloudflare，用 Redirect Rules：

- Hostname = `colourliving.com` 或 `www.colourliving.com`
- 動態目標：`concat("https://colourliving.shop", http.request.uri.path)`
- Status **301**
- 需要「佔位」A 記錄：`@` 同 `www` 指向 `192.0.2.1`，Proxy 開（橙雲）

之後高價值舊路徑再用 Bulk Redirects 對去正確 collection。

### 方案 C（註冊商 Domain Forwarding）

GoDaddy / Namecheap / HKIRC 的「Forwarding」好易，但常見問題：

- 預設 **302**
- 有時 **唔帶路徑**（正正係你而家根網址嘅情況）
- 有時唔支援 HTTPS 好好

只當臨時。長期用 A 或 B。

### 驗證

終端機或 https://httpstatus.io/ ：

```
https://colourliving.com/     → 301 → https://colourliving.shop/
https://colourliving.com/foo  → 301 → 你指定的 .shop URL（唔好 404）
```

GSC 兩個 property 都要有：`.com` 睇「轉址」、`.shop` 睇「接收」。

---

## 3. Canonical 係咩？Shopify 點寫？

**Canonical** = 告訴 Google：「呢頁嘅正規網址係呢條，請把權重集中喺度，唔好當重複內容。」

例：同一張床可能出現喺

- `https://colourliving.shop/products/alys-ly153-bed`
- `https://colourliving.shop/collections/furniture/products/alys-ly153-bed`
- `https://colourliving.com/products/alys-ly153-bed`（若未 301）

正規應該永遠係 **主要網域 + 產品 permalink**：

`https://colourliving.shop/products/alys-ly153-bed`

HTML 會見到：

```html
<link rel="canonical" href="https://colourliving.shop/">
```

（產品頁則係該產品的 `.shop` URL。）

### Shopify 你要做嘅（多數唔使手寫標籤）

1. **Settings → Domains**：Primary domain = `colourliving.shop`  
   Shopify 會用 `{{ canonical_url }}` 自動輸出。首頁已確認有呢條 tag。
2. **唔好** 喺 theme 再複製多一條 canonical，會衝突。
3. 單頁想改正規 URL（好少用）：該頁／產品／collection 的 **Search engine listing → Edit website SEO** 底下有時可改；一般 **唔好改** 去外站。
4. 篩選頁、sort 頁：Shopify `robots.txt` 已 disallow 大部分 filter，減少重複；canonical 通常仍指返乾淨 collection。

**Canonical 唔等於 Redirect。**  
Redirect 係瀏覽器同 Google 都轉去新 URL。Canonical 係「頁仍然打開，但聲明正規係另一條」。`.com` 要用 **301**，唔好只靠 canonical。

---

## 4. Entity 一致性 = 每一頁都要貼 NAP 嗎？

**唔係。** 一致性係指 **全網同一套事實**，唔係每篇產品描述都抄一次地址。

NAP = Name, Address, Phone。

| 地方 | 要唔要完整 NAP |
| --- | --- |
| Footer（全站一份） | 要。Shopify 改一次，所有頁都有 |
| About、Contact、Showroom 頁 | 要（人讀 + Local SEO） |
| 產品頁正文 | **唔需要** 再貼地址；有 footer + schema 就夠 |
| Google Business Profile、Facebook、品牌商 Where to buy | 要，同 footer **逐字一致** |
| Schema JSON-LD（見第 5 題） | 全站一份 Organization／LocalBusiness，機械讀 |

「每一頁的 entity 一致」= 唔好今日寫 Lockhart Road、聽日寫 Lockehart；品牌名永遠 COLOURLIVING。網址可以有兩個角色：citation／官網用 `colourliving.com`，購物按鈕用 `colourliving.shop`——見 [com-vs-shop-citations.md](../playbooks/com-vs-shop-citations.md)。唔好同一句「官網」有時 .com 有時 .shop。

### Shopify 點樣全站加 NAP（人眼可見）

**方法 1 — 頁尾（建議）**

Online Store → Themes → Customize → **Footer** 區塊加：

```
COLOURLIVING
333 Lockhart Road, Wan Chai, Hong Kong
香港灣仔洛克道 333 號
+852 2295 6263
Mon–Sat 10:00–19:00；Sun & PH 12:00–19:00
```

電話用 `tel:+85222956263` 連結。地址可連 Google Maps。

**方法 2 — 店舖地址**

Settings → Store details 填正確地址／電話。部分 theme 會自動拉 `shop.address`。填完檢查 footer 顯示係咪同一套。

**方法 3 — 唔好** 用 page metafield 喺 2000 個產品各貼一次。維護會爆。

標準字串 lock 喺 [playbooks/nap-source-of-truth.md](../playbooks/nap-source-of-truth.md)。

---

## 5. Schema 係咩？Shopify 寫邊度？

**Schema**（結構化資料）= 用 Google 約定的詞彙（schema.org），把頁面意思寫成機器可讀的 JSON，通常叫 **JSON-LD**。人睇網頁唔會見到呢段；Google／AI 會讀。

類比：產品頁人見到「Gessi 龍頭 $6,400」；schema 告訴機械：呢個係 Product，品牌 Gessi，貨幣 HKD，有貨。

### 你要 apply 邊啲、apply 邊度

| 類型 | 作用 | 放邊度 |
| --- | --- | --- |
| `Organization` + `FurnitureStore` | 公司係邊間、喺灣仔 | **全站** `theme.liquid`（一份就夠） |
| `Product` + `Offer` | 名、價、庫存、品牌 | **產品頁**；多數 theme **已經有**，先檢查再加 |
| `BreadcrumbList` | 層級 | 視 theme；有就唔使重複 |
| `FAQPage` | 只有該頁真係有獨特 FAQ 先加 | 品牌頁／指南頁 |
| `WebSite` + `SearchAction` | 站內搜尋 | 可選，theme.liquid |

**唔好** 裝三個 SEO app 再手寫多一份 Product schema，會重複同衝突。

### Shopify 操作

1. 瀏覽器開一個產品頁 → 右鍵 View Source → 搵 `application/ld+json`  
   首頁而家已有 **2** 段（theme 可能已出 Organization／WebSite 或 Product 相關）。
2. 把原始碼貼去 [Rich Results Test](https://search.google.com/test/rich-results)
3. 若 Product 已齊（name, brand, sku, price, priceCurrency, availability, url, image）→ **唔好再加第二份 Product**
4. 若缺少地址／sameAs／營業時間 → 只補 **一份** LocalBusiness／Organization

手寫位置：

Online Store → Themes → **… → Edit code** → `layout/theme.liquid`  
放喺 `</head>` 前。完整草稿見 [playbooks/schema-jsonld-shopify.md](../playbooks/schema-jsonld-shopify.md)。

改 theme 前 **複製一份 theme** 做草稿，以免更新 theme 蓋掉；長期可放喺自訂 snippet `snippets/schema-organization.liquid` 再用 `{% render 'schema-organization' %}`。

---

## 6. 點知 sitemap 係 200 定 500？交過一次夠唔夠？

**交過 ≠ 而家仍然健康。** GSC 只係「我叫 Google 去睇呢條 URL」；伺服器每次回應可以變。

2026-08-26 用 GET 覆核：

- `https://colourliving.shop/sitemap.xml` → **200**
- 子檔 `sitemap_products_1.xml`、`sitemap_pages_1.xml` → **200**

之前用部分抓取工具會見到 500（常見於 HEAD 請求或短暫故障）。**以 GSC 同瀏覽器 GET 為準。**

### 你自己點查（1 分鐘）

1. 無登入瀏覽器開：https://colourliving.shop/sitemap.xml  
   - 見到 XML、入面有 `sitemap_products_1.xml` 等 → 成功（200）  
   - 空白、Error、500 → 壞
2. GSC → **Sitemaps**  
   - 狀態應係 **成功**  
   - 「已發現的網頁」數字會變；若長期 0 或失敗，再查
3. 進階：https://httpstatus.io/ 貼 sitemap URL，睇 Status Code 欄

Shopify sitemap **唔使人手改**；有新產品會自動更新。你要做的係：GSC 維持提交 `https://colourliving.shop/sitemap.xml`，每週睇一次有冇失敗。

中文未 publish 時，sitemap **不應** 大量出現 `/zh/` 頁。Publish 之後先確認子 sitemap 有中文 URL。

---

## 7. 中文未 publish：可唔可以先做技術？hreflang 點變 zh-HK / en-HK？

**可以，而且應該。** 未 publish 的語言，Google 理論上不該大規模索引；你而家做地基唔會「提早暴露半成品中文」。仍要小心：

- 預覽連結、密碼頁、員工分享 URL 唔好公開
- Theme 唔好把未譯頁加 `hreflang` 指向 404
- 中文譯完、抽查無模板洩漏，先 **Publish language**

### Shopify 現實限制（講真）

你喺 Admin 見到只有 `en` 同 `zh`，好常見。Shopify 的 **語言** 同 **市場國家** 係兩層：

| 層 | 你要設 | 對 Google 的含義 |
| --- | --- | --- |
| Markets | 主要市場 = **Hong Kong** | 區域：香港 |
| Languages | English + Chinese (Traditional) | 語言：英／繁中 |
| 自動結果 | HTTP 已見 `content-language: en-HK` | 英文主站已被當成香港英文 |

即係：**en-HK 你可能已經有一半**（市場 = HK）。缺的係中文 publish 之後，hreflang 要變成 `zh-HK` 或 `zh-Hant-HK`，而唔係含糊的 `zh`。

### 建議設定（publish 前做）

1. **Settings → Markets**  
   - 一個主要市場：Hong Kong  
   - 網頁呈現用主要網域 `colourliving.shop`（唔好另開 `.com` 做第二個銷售站）
2. **Settings → Languages**  
   - 主要：English  
   - 新增：**Chinese (Traditional)**。若列表有 **Chinese (Hong Kong) / 中文（香港）** 或 locale `zh-HK`，**優先揀呢個**，唔好揀台灣 `zh-TW`（用字會偏台灣）
   - 狀態保持 **Unpublished**，直到譯文過關
3. Translate & Adapt：譯導航、政策、品牌頁、Top SKU（見內容計劃）
4. Publish 之後：瀏覽器 View Source 搵 `hreflang`

理想見到類似：

```html
<link rel="alternate" hreflang="en-HK" href="https://colourliving.shop/products/...">
<link rel="alternate" hreflang="zh-HK" href="https://colourliving.shop/zh-hk/products/...">
<link rel="alternate" hreflang="x-default" href="https://colourliving.shop/products/...">
```

實際 Shopify 可能輸出 `en` + `zh`，或 URL 係 `/zh/` 而唔係 `/zh-hk/`。  
**URL 前綴唔完美仍然可以做香港 SEO**，因為：GSC 地區、Market = HK、內容係香港繁體、GBP 喺灣仔。`zh-HK` 係加分，唔係成敗開關。

若 publish 後仍係 `hreflang="zh"`：

- 先確認語言係 Traditional 且 Market 係 Hong Kong（系統有時會合成 `zh-HK`／`zh-Hant-HK`）
- 唔好喺 theme 再手寫一套完整 hreflang 同系統重複
- 可改 `html` 的 `lang`：中文頁 `zh-HK`（theme.liquid 用 `request.locale.iso_code` 判斷）

### Publish 前技術清單

- [ ] Footer NAP 中英
- [ ] Organization schema 地址正確
- [ ] Canonical 只有 `.shop`
- [ ] `.com` 301 策略
- [ ] 中文頁無 JSON 洩漏、無亂碼
- [ ] 抽 5 個產品中英 title 公式
- [ ] 先 publish 語言，再喺 GSC 等中文 sitemap 出現後先「請求編入索引」英雄頁

---

## 8. Local SEO 係指咩？

**Local SEO** = 優化「附近／地圖／去邊間店」呢類搜尋，而唔係優化「網上買一隻 SKU」。

客人打：

- 灣仔傢俬店
- Gessi 香港門市
- furniture showroom Wan Chai
- COLOURLIVING 點去

Google 會展示：**地圖包、Google 商家檔案、路線、電話、營業時間、評論**，有時先於網站藍字。

對 COLOURLIVING，Local SEO 幾乎等於 **旗艦店生意**：高價貨要人去洛克道睇布、坐梳化、量浴室。

### 你要管的資產

1. **Google Business Profile（最重要）**  
   類別 Furniture store、地址 333 Lockhart Road、電話、時間、網站建議填 **colourliving.com**（301 去店；你自己控制，Stage B 唔使再改）。Shop 掣／廣告先用 `.shop`。
2. **網站上的本地頁**  
   About／獨立 Showroom 頁，NAP 同 GBP 逐字一致，內嵌地圖、點預約、點去（灣仔站 A1）
3. **Schema**  
   `FurnitureStore` + 地址 + `openingHoursSpecification`（第 5 題）
4. **一致 citation**  
   Facebook、Apple Maps、品牌商 locator：**地址電話逐字一致**；官網欄保持 `.com`，唔好群發改 `.shop`
5. **評論**  
   到店後邀請真實評價

Local SEO **唔係** 喺每張產品頁重複「我哋喺灣仔」。產品頁負責型號；本地意圖由 GBP + Showroom 頁接住。

同 GEO 的關係：AI 問「香港邊度可以睇 Gessi」，會抄 GBP 同你網站答案段。Local 做好，GEO 一齊受惠。

---

## 9. 301 之後，要唔要叫 vendor 把官網改成 colourliving.shop？

**唔使，亦不應該群發。** 301 令 `.com` 連結繼續用得；將來 `.com` 做品牌站時，同一批 locator 連結自動正確。只改廣告／EDM／產品深鏈去 `.shop`。完整取捨見 [com-vs-shop-citations.md](../playbooks/com-vs-shop-citations.md)。
