# 03 — 地基：域名、實體、技術 SEO、Local SEO

呢一層做完，先有資格談內容同 GEO。

---

## A. 域名策略（P0）

### 目標狀態

**一個正規網址：`https://colourliving.shop`**

`colourliving.com` 只做 301 永久重定向到對應的 `.shop` URL（首頁對首頁、舊產品對新產品、無法對應則到最接近的品牌或品類頁）。

### 點解唔保留兩個站

- Google 會分薄連結權重
- AI 會讀到兩套互相矛盾的目錄（舊站 Furniture = 0，新站 Furniture = 198）
- 品牌搜尋 CTR 被舊站分走
- Merchant Center / GBP 無法定一個「官方 URL」

### 執行步驟

1. **盤點舊站 URL**  
   從舊 sitemap、GSC（若 `.com` 仍有 property）、以及主力品牌／品類路徑匯出清單。

2. **做對應表（redirect map）**  
   欄位：`old_url | new_url | type | notes`  
   優先對：首頁、About、Contact、品牌、Bath、Kitchen、主力產品 SKU。

3. **301，唔好 302，唔好 JS 跳轉。** 而家根網址已係 302，內頁 404；逐步改法見 [09-faq-implementation.md](09-faq-implementation.md)。

4. **Canonical 全站指向 `.shop`。** 舊站若暫時仍要開給內部，加 `noindex, follow` **加上** 301，雙重保險。長期應只留 301。

5. **同一日更新所有 citation**：GBP、Facebook、Instagram、LinkedIn、Apple Maps、Bing Places、經銷商「Where to buy」（Gessi、Dornbracht、B&B Italia、Flos、Roca）、HKTB PartnerNet、Time Out（可提交更正）。

6. **GSC**  
   - `.shop` 用 Domain property + URL prefix  
   - 提交新 sitemap  
   - 用 Change of Address（若符合 Google 資格）  
   - `.com` property 觀察 301 被收錄情況，3–6 個月後再決定是否移除

7. **Contact / Footer / Email 簽名 / 名片 / 報價 PDF** 全部改 `.shop`。而家 Contact 仍寫 `colourliving.com`，等於官方自己打自己。

### 過渡期話術

對外只講一個官網。內部可保留舊後台做檔案，但唔好再更新舊前台內容。

---

## B. 實體（Entity）一致性

Google 同 AI 用「知識圖譜」理解 COLOURLIVING。你要提供 **同一組可核對事實**：

| 欄位 | 標準寫法（鎖定，唔好每頁唔同） |
| --- | --- |
| 品牌名 | COLOURLIVING |
| 法律實體 | B.S.C. COLOURLIVING LIMITED |
| 一句定位 | Hong Kong flagship House of Brands for European furniture, lighting and bathroom |
| 地址 | 333 Lockhart Road, Wan Chai, Hong Kong |
| 中文地址 | 香港灣仔洛克道 333 號 |
| 電話 | +852 2295 6263 |
| Email | info@colourliving.com（可保留此電郵） |
| 官網 | https://colourliving.shop |
| 營業 | Mon–Sat 10:00–19:00；Sun & PH 12:00–19:00 |
| 送貨 | Hong Kong only；滿 HK$3,000 免運（政策頁寫清除外地區） |
| 主力品牌 | B&B Italia, Maxalto, Giorgetti, Paola Lenti, Gessi, Dornbracht, Fantini, Flos, Preciosa, Roca…（用固定名單，首頁、About、llms.txt、schema `knowsAbout` 一致） |

### 必做 schema（JSON-LD）

全站或 layout：

- `Organization` + `FurnitureStore` / `HomeGoodsStore`
- `PostalAddress`、`geo`、`openingHoursSpecification`
- `sameAs`：Instagram、Facebook、LinkedIn、YouTube、GBP 地圖 URL
- `hasOfferCatalog` 或至少 `knowsAbout` 品牌列表
- `areaServed`: Hong Kong

產品頁：

- `Product`：name, brand, sku, mpn, gtin（如有）, image, description, offers (price, priceCurrency: HKD, availability, url)
- `Offer` 要同頁面價格一致，否則 Merchant 同 Rich Result 會被拒

品牌頁：

- `Brand` 或 `CollectionPage` + 指向品牌官方
- 清楚寫 authorized retailer / official dealer（**只寫有合約依據的**）

FAQ 有獨特內容先加 `FAQPage`。而家全站共用訂單 FAQ，唔值得每頁標，會被當成 boilerplate。

用 [Google Rich Results Test](https://search.google.com/test/rich-results) 抽查首頁、一個品牌頁、一個產品頁。

---

## C. 技術 SEO（Shopify 實務）

### C1. 發現性

- 驗證 `https://colourliving.shop/sitemap.xml` 是否 200（2026-08-26 GET 已係 200）。GSC → Sitemaps 狀態應為成功。查法見 [09-faq-implementation.md](09-faq-implementation.md) 第 6 題。
- GSC → Sitemaps 提交：`sitemap.xml`（Shopify 會拆 products / collections / pages / blogs）
- 檢查 `robots.txt`：Shopify 預設已 Disallow filter/sort，應保留，避免千個組合頁。
- 確認重要頁 **無** `noindex`（密碼、草稿、search、cart 除外）

### C2. 國際化

- 每個 URL 輸出 `hreflang`：`en-HK`、`zh-HK`、`x-default`
- Canonical 指向自身語言版本，唔好所有語言 canonical 去英文（除非該頁未譯）
- 未譯產品：要麼完成 zh-HK，要麼 hreflang 唔指向空殼中文頁
- HTML `lang`：英文頁 `en-HK`，中文頁 `zh-HK`

### C3. 中文路徑健康

已知問題要開 ticket：

- `/zh` 或部份 collection 404
- 模板洩漏 `產品類型: {"bath"=>"Bath"...}`
- `LISS?` 一類字符損壞
- 產品 handle 全英文可以，但 `title` / `meta` 必須有中文品類詞

### C4. URL 衛生

- 把 `/collections/bath-1` 改成 `/collections/bath` 或 `/collections/bathroom`（改 handle 後做 301）
- 品牌 handle 用穩定拼音／官方名：`gessi`、`bb-italia`、`dornbracht`
- 避免同一產品出現在 10 個 collection 而產生重複 title；用 canonical 到產品 URL（Shopify 預設通常已經係產品 permalink）

### C5. 速度與渲染

- 首屏圖片用 Shopify CDN + 正確 `width/height`
- 產品規格、FAQ **必須在初始 HTML**，唔好等 click 先載入（AI 即時抓頁唔會開 accordion）
- 減少第三方 app 疊加（reviews、wishlist、popup）對 LCP 的傷害

### C6. Merchant Center

Luxury catalog 常見失敗：缺 GTIN、價格不符、缺貨仍標 InStock、舊 `.com` feed 同新 `.shop` 並行。

清單：

- 一個 feed，來源 Shopify
- `price` / `availability` 與 PDP 一致
- `brand` 用官方品牌名
- `mpn` = 廠方型號（A5A323AC00、LY153）
- `gtin` 有則填，無則喺 Merchant 設定正確
- `shipping` 設 Hong Kong，唔好留全球
- 定期看 Diagnostics：disapproved items 每週清一次

---

## D. Local SEO（灣仔旗艦）

頂級家居的本地搜尋，贏的是「想去睇實物」的客人。

### Google Business Profile

- 類別：`Furniture store` 主類別；可加 `Kitchen supply store` / `Bathroom remodeler` 需符合政策，唔好亂加
- 網站：只填 `https://colourliving.shop`
- 地址、電話、時間同網站完全一致
- 封面、陳列室、B&B Italia 樓層、浴室場景、停車／交通（灣仔站 A1 / 銅鑼灣 C）
- 每週 1 則帖：新系列、設計師工作坊、到店預約
- 回覆所有評論，中英按客人語言
- 產品可喺 GBP 選部分英雄 SKU（Gessi、Flos Arco、B&B 梳化）

### 其他地圖

Bing Places、Apple Business Connect、小紅書（若有品牌號）的 NAP 同一套。

### 網站上的本地頁

獨立頁 `/pages/wan-chai-showroom`（中英）：

- 地址、地圖 embed、營業時間
- 點樣預約、停車、邊層係浴室／傢俬／B&B Italia
- 「只限香港送貨」同「歡迎設計師帶客」
- 附近地標：Lockhart Road、Wan Chai

呢頁係 Local + GEO 雙料資產。AI 問「COLOURLIVING 喺邊」時會抄呢段。

---

## E. 完成定義（地基可宣布完成）

- [ ] `.com` 主力 URL 已 301，GSC 見到下降舊站、上升新站
- [ ] 全網 NAP 一致，Contact 不再連去舊站當官網
- [ ] Organization + Product schema 抽查通過
- [ ] Sitemap 200，GSC 已提交
- [ ] hreflang `en-HK` / `zh-HK` 正確
- [ ] 中文模板洩漏與亂碼已修
- [ ] GBP 官網為 `.shop`
- [ ] 品牌版 `llms.txt` 已上線（草稿見 playbooks）
