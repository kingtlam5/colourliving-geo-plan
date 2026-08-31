# Live setup audit — 2026-08-31

公開 GET（未登入 Admin）。對照：[homepage-positioning.md](homepage-positioning.md)、[schema-jsonld-shopify.md](schema-jsonld-shopify.md)、[agents-md-liquid.md](agents-md-liquid.md)、[nap-source-of-truth.md](nap-source-of-truth.md)、[roca-display-noindex.md](roca-display-noindex.md)。

一句：**品牌版 agents／llms 已上線；schema JSON 已通、Local 欄齊；homepage 隱藏 H1 同 meta 已有 GEO 事實；可見 Hero 仍未換採用定位段；預約鈕仍係 Testing@ 日曆。**

---

## 總表

| 面 | 評 | 而家 |
| --- | --- | --- |
| `/agents.md` + `/llms.txt` + `/llms-full.txt` | **過關（GEO）** | 三條 **完全相同**。品牌 NAP、2,000 sqm、品牌名單、只送香港、中文、UCP／MCP／6 步／policies 都有。已唔再係 Shopify 預設。 |
| Organization JSON-LD | **過關** | 有效 JSON。`FurnitureStore` + `HomeGoodsStore`。NAP、geo、時間、`knowsAbout`、`image`（陳列室圖）、`priceRange: $$$$`。**冇**假 `postalCode`。**冇**第二份 Organization。 |
| Product JSON-LD（PDP） | **過關（唔好再加）** | Alys 床：theme 預設 Product + 同一份店 schema。`B&B Italia`、HKD、`InStock`。 |
| Homepage H1 | **過關** | **1 個** `visually-hidden`：`COLOURLIVING — The House of Brands in Wan Chai, Hong Kong`。Logo 係 `div.header__logo`。 |
| Homepage meta | **過關** | Description／og／twitter 已有 Hong Kong、Wan Chai、B&B／Giorgetti／Flos／Gessi、2000 sqm。 |
| Homepage **可見**定位段 | **未過採用稿** | Hero 畫面仍係 H2「COLOURLIVING」+ *The House of Brands*。採用兩句（definitive address / 2000 sqm + 四品牌）**只喺 meta，唔喺 Hero。** Footer 有完整 NAP，所以地點 lock 仍然成立。 |
| `.com` → `.shop` | **過關** | `https://colourliving.com/` 同 `https://www.colourliving.com/` 都係 **301** 去 `https://colourliving.shop/`。 |
| `/pages/contact-us` | **過關** | **301** → `/pages/about-us`。 |
| Roca iPad collections | **過關** | `roca-display-1`… published（200）+ `noindex`。`/collections/gessi` 無 noindex。 |
| 預約 CTA | **未過** | 仍係 `Testing@bschk.onmicrosoft.com` Outlook booking。 |
| UCP 平台 | **過關（平台）** | `GET /.well-known/ucp` 200；robots 指向 agents.md、UCP、MCP、sitemap。 |

---

## 1. agents.md / llms.txt / llms-full.txt

三條 URL 字節級相同。開頭 `# COLOURLIVING`，有洛克道、B.S.C. COLOURLIVING LIMITED、只送香港、品牌、How to cite、中文、UCP discovery／MCP、versions `2026-08-25`（latest）、Rules、products.json、policies。**無** Shopify `## Platform`、無最頂 Shop Pay 長文。

同最新可貼稿 [agents-md-liquid.md](agents-md-liquid.md) 的差距（**唔阻 GEO**，可下次 theme 微調）：

| 最新稿 | Live |
| --- | --- |
| `# Agent Instructions — COLOURLIVING` | `# COLOURLIVING` |
| 中文用粵語「係…嘅」 | 書面「是一間」（一樣可引用） |
| `### Store metadata` canonical／mirror 一句 | 無；sitemap 寫成完整 URL |
| Rules 付款 + Shop skill 合成一條 | 分開兩條（意思仍在） |
| UCP 連 `ucp.dev` | 有協議、無該 markdown link |

電話／電郵正確地 **冇**寫入 agents.md（Shopify 對 cache 的建議）。Footer／schema／About 有。

---

## 2. Schema

主頁兩個 JSON-LD block，都 parse 到：

1. Organization + FurnitureStore + HomeGoodsStore（`@id` `https://colourliving.shop#organization`）
2. WebSite + SearchAction（Hyper 預設，留）

| 欄 | Live | 評 |
| --- | --- | --- |
| description | House of Brands；furniture, lighting and bathroom；333 Lockhart Road；Delivery within Hong Kong | 啱 |
| telephone | `+85222956263` | 等價 NAP `+852 2295 6263`。Footer 可見寫法有空格 |
| address | 333 Lockhart Road / Wan Chai / Hong Kong / HK | 啱。**省略 postalCode**（香港正確） |
| geo | 22.27925, 114.17841 | 洛克道附近 |
| hours | Mon–Sat 10–19；Sunday 12–19 | 啱 |
| sameAs | FB、IG、小紅書、wa.me **四條，無 `""`** | 啱 |
| knowsAbout | furniture / lighting / bathroom fittings / B&B / Flos / Gessi / Dornbracht | 啱；JSON 逗號已修 |
| image | Fukasawa 陳列室 JPG + logo | 啱（Local 要店相，唔淨 logo） |
| priceRange | `$$$$` | 奢侈 **檔次**，唔係 HKD $4 |
| hasOfferCatalog | 無 | 可選；唔急 |
| 重複 Organization | 無 | 啱 |

About、Gessi collection：同一份店 schema，無第二份。PDP 加 Product，唔好再開一份 Product。

Rich Results：貼 **主頁** 測 Local business；貼 **PDP** 測 Product。`postalCode` 黃燈可忽略。

---

## 3. Homepage

| 項目 | Live |
| --- | --- |
| Title | `COLOURLIVING \| The House of Brands`（仍無 Hong Kong；meta description 已補） |
| Canonical | `https://colourliving.shop/` |
| Hreflang | 無（`/zh`、`/zh-hk` 404，維持唔加） |
| H1 | 1 個 hidden，採用句 **一字不差** |
| Hero 可見 | H2 COLOURLIVING + *The House of Brands*。**無** “The definitive address…”／“Immerse yourself…” |
| 2000 sqm | **只喺 meta**（同 schema description 無面積；面積喺 agents.md） |
| 品牌牆 | B&B、Dornbracht、Effe、Fantini、Gessi、Giorgetti、Maxalto、Paola Lenti、Preciosa |
| Slideshow | B&B / Giorgetti / Gessi |
| 產品卡 | Flos IC 燈等；品牌連仍有 **`/collections/vendors?q=`**（Flos collection 本身 200，應改直連） |
| 陳列室段 | 無寫洛克道；CTA Testing@ |
| Footer NAP | 333 Lockhart Road, Wan Chai, Hong Kong；info@；+852 2295 6263；Mon–Sat 10–19；Sun & Holidays 12–19 |
| 社交 icon 標籤 | href 啱；可見名 WhatsApp→Tumblr、小紅書→Vimeo（舊問題） |
| Special Offer | Shop Now 仍 disabled |
| 漢字 | 主頁 0 |
| `og:image` | 仍一條 `http://`（另有 https `secure_url`） |

GEO：模型而家可以由 **llms.txt + schema + meta + footer** 抄到灣仔／品牌。Hero 可見句仍然偏短，採用定位段上 Hero 仍然值得做——唔好再藏。

---

## 4. 其他 setup

| 項目 | Live |
| --- | --- |
| robots.txt | 指向 `/agents.md`、UCP、MCP；`Sitemap: /sitemap.xml`。無 llms.txt 行（Shopify 預設；三條 URL 已 mirror，唔急） |
| sitemap.xml | 200；含 products／pages／collections／agentic discovery |
| `/.well-known/ucp` | 200 |
| `/pages/demo` | 404（theme 404 仍輸出店 schema，正常） |
| `/pages/about-us` | 200；可見 Lockhart；**無 H1**（H2「COLOURLIVING」）。可之後加頁面 H1，唔阻而家 schema |
| `/collections/roca` | 200、可索引（正常品牌頁）。iPad 用 `roca-display-*` 已 noindex |
| Roca noindex 細節 | Live 係 `noindex, nofollow`；playbook 寫 `noindex, follow`。頁仍 published。Follow 與否對 iPad 無關；想內部連結被跟可改返 `follow` |

---

## 你喺 Admin 仲可以做（按影響）

1. **換預約連結**，拎走 `Testing@bschk`。步驟：[how-to-change-booking-link.md](how-to-change-booking-link.md)。陳列室段可加一句可見洛克道。  
2. **Hero 可見副標題**換成採用兩句（或你定稿、但要可見、要睇得出唔淨係梳化）。而家好句只喺 meta。  
3. 產品卡品牌細字連 `/collections/vendors?q=`：[how-to-fix-vendor-card-links.md](how-to-fix-vendor-card-links.md)。Special Offer 死掣：給 URL 或收埋。  
4. agents.md 可選標題／Store metadata：[how-to-edit-agents-md-title-and-store-metadata.md](how-to-edit-agents-md-title-and-store-metadata.md)。  
5. Title 可加 `Hong Kong`（例如 `COLOURLIVING | The House of Brands in Wan Chai`）。  
6. `hasOfferCatalog` 三條 collection：**可選**。  
7. About 加一個可見 H1。社交 icon 標籤 Tumblr／Vimeo。`og:image` 改 https。

**唔使做：** 假 postalCode；複製 Product JSON-LD；unpublish Roca display；而家加 hreflang；抄返 Shopify `## Platform`。
