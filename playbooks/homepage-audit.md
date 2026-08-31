# 首頁 audit（colourliving.shop）

**2026-08-31 覆核**見 [live-setup-audit-2026-08-31.md](live-setup-audit-2026-08-31.md)：隱藏 H1 同 meta 已過；可見 Hero 仍未換採用定位段；預約仍係 Testing@。

日期：**2026-08-28**（同日第二次覆核 H1）。公開 GET `https://colourliving.shop/`（HTTP 200）。

**H1 已修好：** 主頁而家 **只有 1 個** `<h1 class="visually-hidden">COLOURLIVING — The House of Brands in Wan Chai, Hong Kong</h1>`。Logo 係 `<div class="header__logo">`。Header 結構正常（logo 圖、menu drawer 仍在）。

一句：主頁仍然係 **視覺旗艦店 + 電商目錄**，未係 Google／AI 可抄的 **品牌實體頁**（隱藏 H1 唔等於有可見定位段）。

對照：[docs/04-pages-and-content.md](../docs/04-pages-and-content.md) B 節、[nap-source-of-truth.md](nap-source-of-truth.md)、[homepage-hidden-h1.md](homepage-hidden-h1.md)。

---

## 客人由上到下見到咩

Theme：Hyper preset **Pillar Beige v1.4.0**（`Shopify.theme`）。語言：`html lang="en"`，`Content-Language: en-HK`。**零漢字。**

| 區 | 而家係咩 |
| --- | --- |
| Header | Logo 係 `<div class="header__logo">`（唔再係 H1）。Mega menu 同前。 |
| Hero | Overlay 圖 + **H2**「COLOURLIVING」+ 一句 *The House of Brands*。冇地址、冇品牌名單、冇香港送貨。 |
| 四格 banner | Home Essentials → `/pages/home-essentials`；Featured Brands → `/pages/featured-brands`；Get Inspired → living-room inspiration；**Special Offer「Shop Now」按鈕 disabled**（死 CTA）。 |
| Haute Living Brands | 一句 *A curated selection of renowned brands…* + logo 連去品牌 collection：B&B Italia、Dornbracht、Effe、Fantini、Gessi、Giorgetti、Maxalto、Paola Lenti、Preciosa。 |
| Slideshow | 三張：B&B ITALIA／GIORGETTI／GESSI，連去正確品牌 collection。文案極短（例如 *Icon of timeless contemporaneity.*）。 |
| Lookbook「Style Define Space」 | Italian Luxury／Minimalist／Modern，hotspot 去 Husk、Apollo、Allure O' Dot 等 PDP。 |
| 「Where Every Room Tells a Story」 | 三隻產品卡（含 Flos IC 燈、Metropolitan、Alys 床）。 |
| 「Discover Design In Person」 | *Our showroom offers a personalised journey…* **無寫灣仔／洛克道。** CTA **Reserve Your Visit** 去 Outlook：`Testing@bschk.onmicrosoft.com`（測試日曆）。 |
| Instagram 牆 | 外連 colourliving.hk 帖。 |
| FAQ | 13 條 **網店訂單／送貨／退貨**（Mastercard、7 日換貨、滿 $3,000 免運、一年保、不退款）。有「只送香港、不接受國際運送」。**無**預約、授權、可睇邊啲品牌。 |
| Popular Search | 全英文：Sofa、Bed、Chair、Table、Table Lamp、Bathroom Faucet、Toilet、Washbasin、Bathtub。 |
| Footer | NAP **齊**：333 Lockhart Road, Wan Chai；info@colourliving.com；+852 2295 6263；Mon–Sat 10:00–19:00；Sun & Holidays 12:00–19:00。社交：Facebook、IG、WhatsApp `wa.me/85259217909`、小紅書。 |

---

## 技術 SEO（主頁本身）

| 項目 | 現況 | 評 |
| --- | --- | --- |
| Title | `COLOURLIVING \| The House of Brands` | 品牌對，但無 Hong Kong／Wan Chai |
| Meta description | *A one-stop lifestyle destination, with everything you need to furnish and accessorise your home from kitchen and bath…* | 通用電商句；**無香港、無地址、無品牌名** |
| Canonical | `https://colourliving.shop/` | 正確 |
| hreflang | 無 | 中文未 publish 時可接受 |
| robots | 無 noindex | 可索引 |
| H1 | **1 個：** `visually-hidden`「COLOURLIVING — The House of Brands in Wan Chai, Hong Kong」 | 結構正確。畫面仍係 Hero H2「COLOURLIVING」 |
| JSON-LD | `Organization` + `FurnitureStore`（有地址）+ WebSite/SearchAction | 見 [schema-audit.md](schema-audit.md)。`sameAs` 已無空字串 |
| og:image | 一條用 **`http://`**（另有 secure_url https） | 應全部 https |
| 分析 | GA4 `G-3L3SMEW6C7`；Microsoft Clarity | 已裝 |
| 中文 | 主頁 0 個漢字；無 `/zh` 切換 | 香港搜尋接唔住 |

Rich Results Test 貼首頁出「No items detected」仍然 **預期**：呢頁未有 Local business schema。測 Product 要用 PDP。見 [google-rich-result-types.md](google-rich-result-types.md)。

---

## GEO／可引用性

AI／Google 想抄的事實（店名、灣仔、2,000sqm、品牌、只送香港、預約）**冇集中在首屏一段**。

- 地址、電話、時間：**只在 footer**（人睇得到；模型較少抄 footer）。  
- 陳列室段無 NAP。  
- 預約按鈕指向 **Testing@** 日曆，公開頁唔應出現。  
- 社交 icon 的可見名稱錯：WhatsApp 標成 Tumblr、小紅書標成 Vimeo（href 本身正確）。

---

## 內連（主頁自己的問題）

- 品牌 logo 牆連得啱（`/collections/gessi` 等）。Slideshow 三品牌都啱。  
- 產品卡有外連去 **`/collections/vendors?q=Flos`**、`?q=B%26B%20Italia`，而唔係 `/collections/flos`、`/collections/b-b-italia`。Vendors 搜尋頁弱過品牌 collection。  
- Popular Search 有 `/collections/bathroom-faucet`（單數，live 正確）。  
- **無** 連 Journal（未寫文都唔急）。**無** `/pages/wan-chai-showroom`、`/pages/for-designers`（頁本身可能未建）。

呢步係 **首頁內連**，唔係 content 流程第 5 步寫文，亦唔係第 2 步改 collection 文案。

---

## 優先（只限主頁，Admin 改文案／連結即可）

1. **換測試預約連結**；陳列室段補一句 NAP（灣仔洛克道 333、預約、只送香港）。  
2. **Title + meta** 加 Hong Kong / Wan Chai；首屏加 40–80 字定位段（英文；中文等 ZH publish）。唔好堆 keyword。  
3. **Organization schema**：地址、電話、時間、清走 empty `sameAs`（theme，見 [how-to-edit-schema.md](how-to-edit-schema.md)）。  
4. 產品卡品牌連去 **品牌 collection**，唔好 `vendors?q=`。Special Offer 要嘛給真 URL，要嘛唔顯示死掣。  
5. FAQ 可留網店政策；**唔好** 當 Homepages 的 GEO 答案（陳列／授權放定位段同 About）。

唔需要為首頁開 Journal，亦唔好把主頁改成一篇長 blog。
