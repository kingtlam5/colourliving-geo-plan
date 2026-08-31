# Schema audit（live，2026-08-28）

公開抓取。唔寫 theme code。對照 NAP：[nap-source-of-truth.md](nap-source-of-truth.md)。點改：[how-to-edit-schema.md](how-to-edit-schema.md)。

**對比 8 月 26 日：** 舊嘅瘦 `Organization`（無地址、`sameAs` 夾 `""`）**已經換成** `Organization` + `FurnitureStore`。呢個 P0 做完。

---

## 而家全站有咩 JSON-LD

每頁 header 一份（同一 `@id`，正確，唔算重複公司）：

```json
"@type": ["Organization", "FurnitureStore"]
"@id": "https://colourliving.shop#organization"
```

| 頁 | HTTP | JSON-LD |
| --- | --- | --- |
| `/` 主頁 | 200 | FurnitureStore + **WebSite / SearchAction** |
| `/pages/about-us` | 200 | FurnitureStore only |
| `/collections/gessi`、`/bathroom-faucet` | 200 | FurnitureStore only |
| `/products/alys-ly153-bed` | 200 | FurnitureStore + **Product** |
| Gessi 龍頭 PDP（Rilievo 恆溫） | 200 | FurnitureStore + **Product**（`OutOfStock`） |
| `/pages/demo` | **404** | 仍輸出 FurnitureStore（Shopify 404 正常） |

無 `itemscope` microdata。無 `FAQPage`。無 `BreadcrumbList`。無第二份 `Organization`。

---

## 1. FurnitureStore（合格，留住）

已有、同 NAP 大致對齊：

| 欄 | 現況 | 評 |
| --- | --- | --- |
| name / legalName | COLOURLIVING / B.S.C. COLOURLIVING LIMITED | 啱 |
| url | `https://colourliving.shop`（每頁都係店根，唔係 About URL） | 啱 |
| telephone | `+852-2295-6263` | 同 `+852 2295 6263` 等價 |
| email | info@colourliving.com | 啱 |
| address | 333 Lockhart Road, Wan Chai, HK | 啱 |
| geo | 22.27925, 114.17841 | 洛克道附近，合理 |
| 營業 | Mon–Sat 10–19；Sunday 12–19 | 公眾假期 schema 無獨立欄，周日已 12–19 |
| areaServed | Hong Kong | 啱 |
| sameAs | Facebook、IG、小紅書、WhatsApp **四條實 URL，冇 `""`** | 啱 |
| logo | 絕對 https URL | 夠用 |

Rich Results Test 而家應貼 **主頁** 再測一次：有機會出 **Local business**（之前「No items detected」係因為舊 Organization 無地址）。地圖知識卡仍靠 GBP 一致。

`FurnitureStore` 包傢俬陳列；浴室／燈用同一份 JSON 加 `HomeGoodsStore` + `description`，唔好刪 FurnitureStore。見 [homepage-positioning.md](homepage-positioning.md)。

---

## 2. WebSite + SearchAction（主頁，留住）

`https://colourliving.shop/search?q={search_term_string}` — Hyper 預設，加分。只喺主頁出現係正常。

---

## 3. Product（theme 預設，唔好再開第二份）

Alys 床：brand **B&B Italia**、sku、HKD `90000.00`、`InStock`、圖、描述 — 合格方向。  
Rilievo 龍頭：brand **Gessi**、價 HKD、`OutOfStock` 正確；**`category` 空字串**。

| 有 | 無（多數 Shopify 預設；唔急改 Liquid） |
| --- | --- |
| name, url, image, brand, sku, offers.price / HKD | mpn、gtin |
| availability | shippingDetails、hasMerchantReturnPolicy（去 **Merchant Center** 填） |
| | aggregateRating（冇評價就唔好假造） |
| | seller / FurnitureStore 連去 Product（可選） |

Product `@id` 係相對路徑 `/products/...?` — Google 多數接受。**唔好**為呢個複製成第二份 Product。

Rich Results Test 要貼 **產品 URL**，唔好貼主頁。

GSC 黃燈缺運費／退貨 → 忽略 schema，改 GMC。

---

## 4. 仍然冇（優先低過貨頁文案）

| 類型 | 畫面 | JSON-LD | 要唔要做 |
| --- | --- | --- | --- |
| BreadcrumbList | Collection／PDP 有 HTML 麵包屑 | **無** | 可選；見 [google-rich-result-types.md](google-rich-result-types.md) |
| CollectionPage / ItemList | 品牌／品類頁 | **無** | 旗艦店可接受，唔急 |
| FAQPage | 主頁有訂單 FAQ | **無** | **唔好加**（Google 2026-05 已取消 FAQ 豐富結果） |
| BlogPosting | `/blogs/news` 200，listing 好似無新支柱 | 未抽到文章 | 有 Journal 先至睇 theme 有冇自動出；有就唔好重複加 |

---

## 建議順序（而家）

1. **測：** https://search.google.com/test/rich-results 貼主頁（Local business）+ 貼 Alys（Product 仍 Valid）。  
   https://validator.schema.org/ 貼主頁原始碼。  
2. **唔做：** 改 Product JSON-LD、加 FAQPage、加第二份 Organization。  
3. **之後（可選）：** BreadcrumbList 同畫面路徑一致。  
4. **貨頁 `category: ""`：** 喺 Admin 填 Product type，唔使改 schema 檔。

Schema 唔代替首頁可見定位段、亦唔代替 content 流程第 2 步改 collection。
