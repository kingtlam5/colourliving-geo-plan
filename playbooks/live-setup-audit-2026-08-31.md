# Live setup audit — 2026-08-31（第二次，約 08:51 UTC）

公開 GET，未登入 Admin。對照：[homepage-positioning.md](homepage-positioning.md)、[schema-jsonld-shopify.md](schema-jsonld-shopify.md)、[agents-md-liquid.md](agents-md-liquid.md)、[nap-source-of-truth.md](nap-source-of-truth.md)。

同日早段比對：`Testing@` 已換成 `COLOURLIVINGShowroomBooking@`；`agents.md` 已加 `Agent Instructions —` 同 Store metadata。其餘地基無回退。

一句：**agents／llms／schema／H1／301／Roca／UCP 過關。預約掣已唔再係 Testing@。Hero 可見句仍未換採用定位段。**

---

## 總表

| 面 | 評 | Live |
| --- | --- | --- |
| `/agents.md` + `/llms.txt` + `/llms-full.txt` | **過關** | 三條字節相同。標題 `Agent Instructions — COLOURLIVING`；NAP、品牌、只送香港、中文、UCP、`### Store metadata` canonical。無 `## Platform`。 |
| Organization JSON-LD | **過關** | JSON parse 到。`FurnitureStore` + `HomeGoodsStore`。NAP、geo、時間、`knowsAbout`、陳列室 `image`、`priceRange: $$$$`。無假 `postalCode`。每頁一份 Organization。 |
| Product JSON-LD | **過關** | Alys：theme Product + 店 schema。B&B Italia、HKD 90000、`InStock`。唔好再開第二份 Product。 |
| Homepage H1 | **過關** | 1 個 `visually-hidden`：`COLOURLIVING — The House of Brands in Wan Chai, Hong Kong`。Logo 係 `div`。 |
| Homepage meta | **過關** | HK、Wan Chai、B&B／Giorgetti／Flos／Gessi、2000 sqm。 |
| Homepage **可見**定位段 | **未過採用稿** | Hero 仍係 H2「COLOURLIVING」+ *The House of Brands*。採用兩句只喺 meta。Footer 有 NAP，地點 lock 仍成立。 |
| 預約 CTA | **過關（相對 Testing@）** | `COLOURLIVINGShowroomBooking@bschk.onmicrosoft.com`。公開名已唔係 Testing。仍係 `onmicrosoft.com` 租戶域（可選再換公司域名）。 |
| `.com` / www → `.shop` | **過關** | 兩個 **301** → `https://colourliving.shop/`。 |
| `/pages/contact-us` | **過關** | **301** → `/pages/about-us`。 |
| Roca display | **過關** | `roca-display-1` 200 + `noindex, nofollow`。Gessi 無 noindex。 |
| UCP / robots / sitemap | **過關** | `/.well-known/ucp` 200，version `2026-08-25`。robots 指 agents.md + sitemap。 |
| `vendors?q=` | **低優先 backlog** | 產品圖／標題去 PDP（啱）。品牌細字仍 `url_for_vendor`。唔阻買嘢。 |

---

## 1. agents.md / llms.txt

三條相同。要核對的都有：洛克道、B.S.C. COLOURLIVING LIMITED、2,000 sqm、品牌、How to cite、`ucp.dev`、`/.well-known/ucp`、MCP、versions、Store metadata、policies。電話／電郵正確地唔寫入檔。

可選、唔阻：中文「是一間」vs 粵語「係…嘅」；Rules 付款同 Shop skill 分開兩條。

---

## 2. Schema

主頁 2 個 JSON-LD：Organization 複合類型 + WebSite SearchAction。About／Gessi 各 1 份店 schema。PDP + Product。

電話 schema 寫 `+85222956263`，footer 可見 `+852 2295 6263`——等價。`hasOfferCatalog` 仍無（可選）。

---

## 3. Homepage

| 項目 | Live |
| --- | --- |
| Title | `COLOURLIVING \| The House of Brands`（Hong Kong 喺 meta，未入 title） |
| Hero 可見 | *The House of Brands*。無 definitive address／2000 sqm 可見句 |
| 2000 sqm | meta + agents.md；Hero 無 |
| Footer NAP | 333 Lockhart Road, Wan Chai, Hong Kong；info@；+852 2295 6263；Mon–Sat 10–19；Sun & Holidays 12–19 |
| 預約 | `Reserve Your Visit` → `COLOURLIVINGShowroomBooking@bschk.onmicrosoft.com` |
| 漢字 | 0 |
| `og:image` | 仍一條 `http://`（另有 https secure_url） |
| 社交 icon 標籤 | href 啱；可見名 Tumblr／Vimeo |
| Special Offer | 仍有 |
| `/zh` | 404；hreflang 仍然唔好加 |

陳列室段文案仍無洛克道（footer 有）。

---

## 4. 預約（今次有變）

**之前：** `Testing@bschk.onmicrosoft.com`  
**而家：** `COLOURLIVINGShowroomBooking@bschk.onmicrosoft.com`

公開頁已唔再叫 Testing。確認信／URL 仍帶 `bschk.onmicrosoft.com`。功能可以公開用。若要再靚：IT 用 `visit@colourliving.com` 之類公司域名開新 Bookings，Share URL 貼返 Shopify。唔急過 Hero 可見句。

舊 `Testing@` 頁若仲 Publish，建議 Unpublish，避免書籤。

---

## 5. 仲可以做（按影響）

1. Hero **可見**副標題換成採用兩句（或你定稿；要睇得出唔淨係梳化）。而家好句只喺 meta。  
2. Title 可加 Hong Kong / Wan Chai。陳列室段可加一句可見洛克道。  
3. `og:image` 改 https；社交 icon 標籤；Special Offer 死掣。About 加 H1。  
4. 產品卡品牌細字改 `/collections/{{ vendor | handleize }}`——backlog。  
5. Bookings 可選轉公司域名。`hasOfferCatalog` 可選。

**唔使做：** 假 postalCode；複製 Product schema；unpublish Roca display；而家加 hreflang；抄 Shopify `## Platform`；為對齊預設把 UCP 搬去檔案第二節。
