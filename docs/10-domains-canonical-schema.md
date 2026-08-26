# 10 — 雙域名策略、Canonical 逐步做、現有 Schema 審計

日期：2026-08-26。Schema 結論來自即時抓取 colourliving.shop 首頁、產品頁、分類頁、About／Contact。

---

## 1. `.com` 做 Branding、`.shop` 做 e-shop：而家應唔應該 301？日後分得返開嗎？

**而家應該把 `colourliving.com` 暫時 301 去 `colourliving.shop`。**  
長遠分拆仍然做得到，但要當「第二階段遷站」，唔好當而家已經係兩個站。

### 點解而家要 301（即使 management 想留 `.com` 做品牌）

品牌站未存在。空殼／亂轉址會傷害兩個域名：

| 而家 `.com` | 後果 |
| --- | --- |
| 根網址 **302** 去 `.shop` 首頁 | Google 當臨時搬家；品牌 SERP 可同時出 `.com` 同 `.shop` |
| 內頁 **404** | 舊 bookmark／殘餘外鏈撞牆；**而家多數已唔喺 Google 索引**（見 [colourliving-com-current-index.md](../playbooks/colourliving-com-current-index.md)） |
| Contact／名錄仍寫 `.com` | 官方自己分裂 entity |

未有品牌內容就「留住 `.com` 唔好指去 Shopify」，等於留一個死品牌網域。Luxury 雙站策略只在 **品牌站真係有獨立內容** 時先有意義。

### 暫時加去 Shopify 做 redirect，可唔可以日後 disconnect？

**可以。** Shopify：Settings → Domains → 移除／不再連接 `colourliving.com`，DNS 改指去未來品牌站（Webflow、另一 Shopify 店、自家 CMS 都得）。

但要同 management 講清楚三句：

1. **Disconnect 係技術上隨時做**（DNS + 去掉 Shopify 連接，通常數小時到 48 小時）。
2. **Google 記憶唔係隨時清零。** 301 做咗幾個月，品牌搜尋會習慣 `.shop`。日後 `.com` 再變 200，要重新建立品牌站內容同內部連結，先會搶返「COLOURLIVING」主結果。呢個係正常、可計劃，唔係鎖死。
3. **唔好用「兩個 Shopify 店、兩套產品目錄」。** 日後分拆時，`.com` 只放品牌／陳列室／媒體／設計師；產品同 checkout 永遠留 `.shop`。舊產品路徑繼續 301 去 `.shop`。

### 建議分三個階段（寫入公司計劃）

```
階段 A（而家，品牌站未開工）
  colourliving.com  /*  →  301  →  colourliving.shop（對應頁或首頁）
  對外 **身份網址** 仍然講 colourliving.com（vendor / 名片 / 建議 GBP）
  對外 **購物／廣告** 用 colourliving.shop
  唔好發動 vendor 改官網去 .shop

階段 B（management 真係開品牌站：至少有 About、Showroom、Press、For Designers）
  colourliving.com/                 → 品牌首頁 200
  colourliving.com/about            → 品牌頁 200
  colourliving.com/products/*       → 仍然 301 去 .shop
  colourliving.com/collections/*    → 仍然 301 去 .shop
  colourliving.shop/pages/about-us  → 301 去 .com/about（避免兩個 About）

階段 C（穩定）
  .com = 品牌 entity（Organization + FurnitureStore）
  .shop = 商務（Product + Offer）
  互相用同一套 NAP、sameAs 連對方
```

階段 A 加 Shopify redirect **唔會阻** 階段 B。階段 B 要預留工程：redirect map 由「全站去 `.shop`」改成「只有商務路徑去 `.shop`」。

### 階段 A 具體做法（Shopify）

1. Settings → Domains → **Connect existing domain** → `colourliving.com` 同 `www`
2. 依指示改 DNS（你有 domain login 就夠）
3. **Primary domain 必須係 `colourliving.shop`**
4. `.com` 選 **Redirect to primary domain**（Shopify 用 301）
5. 內部記一筆：*`colourliving.com` parked for future brand site; currently 301 to shop`*

驗證：`https://colourliving.com/` 應變 **301**（而家係 302）去 `.shop`。

高價值舊路徑（Gessi、Bath）若 Shopify 自動「保留路徑」後變成 `.shop` 404，再喺 **URL Redirects** 對去正確 collection。

### 唔好做嘅

- 而家就起一個空的 `.com` 品牌首頁（薄內容，兩個 About 互搶）
- 把 `.com` 設成 Shopify **第二個可瀏覽店**（同一目錄兩個網域，canonical 戰爭）
- 用 302 一直放住「等管理層決定」

**一句畀 management：** 品牌站未有內容前，`.com` 最有價值的用途係把歷史權重同死連結交俾 `.shop`。品牌站開工嗰日先分拆，產品 URL 永遠唔搬去 `.com`。Vendor／名錄的「官網」**繼續寫 colourliving.com**——見 [com-vs-shop-citations.md](../playbooks/com-vs-shop-citations.md)。

---

## 2. Canonical：你要逐步做嘅清單

Canonical 唔係每天改產品。Shopify 預設已經寫 tag。你要做的係 **設定正確 + 捉例外**。

### Canonical 做緊咩（10 秒版）

同一件貨可以有好多條 URL。Canonical 話俾 Google：**只此一條係正規。**

例：

- 正規：`https://colourliving.shop/products/alys-ly153-bed`
- 唔該當另一頁：`.../collections/furniture/products/alys-ly153-bed`、`http://`、`www.`、未來的 `colourliving.com/products/...`

Redirect 係「瀏覽器轉走」。Canonical 係「頁仍打開，但聲明正規」。`.com` 要用 redirect；店內重複路徑靠 canonical。

### 而家店已做對嘅

抽查結果：

| 頁 | Canonical |
| --- | --- |
| 首頁 | `https://colourliving.shop/` 正確 |
| 產品 Alys | `https://colourliving.shop/products/alys-ly153-bed` 正確 |
| `/collections/furniture` | 指向自己 正確 |
| `/collections/bath-1` | 指向 `/collections/bath` **正確**（handle 醜但已正規化） |

### 而家你見到、但其實已處理緊的

`https://colourliving.shop/pages/contact-us` **301** 去 About，canonical 亦係 About。若計劃入面 **永遠唔會有獨立 Contact 頁**（聯絡資訊一律放 About），呢個 301 **要留**，唔好刪、唔好再開 Contact。逐步核對見 [11-canonical-howto.md](11-canonical-howto.md)。

產品 `/collections/furniture/products/alys-ly153-bed` 同 `/products/alys-ly153-bed` 內容相同，但兩邊 canonical **已經**指向 `/products/alys-ly153-bed`。唔使喺 Admin 逐隻貨填 canonical。點樣自己核對同改產品卡連結，同樣見第 11 份。

---

### Step-by-step（Admin，唔使識 code）

**Step 1 — 鎖定主要網域（一次）**

1. Shopify Admin → **Settings → Domains**
2. 確認 **Primary** = `colourliving.shop`（有 Primary 徽章）
3. 若有 `www.colourliving.shop`，設為重新導向至非 www（或相反，只留一個）
4. 儲存後，無痕開首頁 → 右鍵「查看網頁原始碼」→ 搜 `canonical`  
   應只有一條，而且係 `https://colourliving.shop/`

唔好喺 theme.liquid 再手寫 `<link rel="canonical">`。Shopify 用 `{{ canonical_url }}` 已經出。寫多一條會衝突。

**Step 2 — 連接 `.com` 之後再查一次**

1. 無痕開 `https://colourliving.com/`
2. 應 **301** 到 `https://colourliving.shop/`（網址列變成 `.shop`）
3. 原始碼入面 canonical 仍然係 `.shop`，唔係 `.com`

若 `.com` 可以完整打開同一間店、canonical 卻寫 `.com`，即係你把 `.com` 設成可瀏覽而唔係 redirect。改返「Redirect to primary」。

**Step 3 — 修 Contact（只適用於你想有獨立 Contact 頁）**

若公司策略係 **唔要 Contact、一律用 About**：唔好刪 301、唔好新建 Contact。改跟 [11-canonical-howto.md](11-canonical-howto.md)。

若將來改策略要獨立 Contact：先刪 `contact-us` → `about-us` 的 redirect，再新建 Pages，handle 唔好同 About 撞。

**Step 4 — 抽查產品同分類（每季 10 條）**

開產品頁原始碼，搜 `canonical`：

- 必須係 `/products/該handle`，**唔好**帶 `?variant=` 當正規（Shopify 預設產品 canonical 通常已去乾淨 permalink，Offer 先帶 variant，呢個正常）
- 由 collection 點入產品，canonical 仍應係 `/products/...` 而唔係 `/collections/furniture/products/...`

分類頁：`/collections/gessi` 指向自己。若你有重複 collection（`bath` 同 `bath-1`），保持而家咁：**bath-1 canonical 去 bath**，長期把選單只連 `bath`，`bath-1` 做 301 更乾淨。

**Step 5 — 單頁 SEO 欄（只改內容，唔改網域）**

每個 Page／Product／Collection 下面 **Search engine listing → Edit website SEO**：

- Page title、Description：寫俾 Google 結果用
- URL handle：英文短、穩定
- **唔好** 把「URL and handle」改成另一個網域
- **唔好** 兩頁用同一個 handle

**Step 6 — 篩選頁（唔使做）**

Shopify 已禁止 Google 大爬 `sort_by`、多 filter。唔好為每個「Gessi + Chrome」filter URL 人手設 canonical。要打「Gessi 龍頭」就用品牌 collection 或獨立 collection。

**Step 7 — 中文 publish 之後**

每種語言自己指向自己：

- 英文產品 canonical = `https://colourliving.shop/products/alys-ly153-bed`
- 中文產品 canonical = `https://colourliving.shop/zh/products/alys-ly153-bed`（前綴以實際為準）

Shopify Markets 通常會咁做。你要抽查：中文頁 **唔好** canonical 全部指返英文（除非該 SKU 完全未譯、你寧願中文 noindex——現階段未 publish 就唔會有呢題）。

**Step 8 — 用 Google 確認**

1. [Rich Results Test](https://search.google.com/test/rich-results) 貼產品 URL
2. GSC → URL 檢查 → 睇 Google 選用的 canonical（「使用者提供」應等於「Google 選用」）

若「Google 選用」同你寫嘅唔同，先查係咪 duplicate title、薄內容、或 contact 類錯誤轉址。

---

## 3. 你而家 Shopify 預設 Schema 有咩問題？漏咗邊？

**你以為 default 已經寫得好好，呢個判斷對咗一半。**

Shopify／theme 預設嘅目標係：**產品頁有一個合法嘅 Product + Offer，令 Google 識價錢同庫存。**  
佢 **唔係** 為香港實體旗艦店、GEO、或完整 Merchant 政策而設計。所以「唔使改」只限「想避免 rich result 完全無效」。Luxury + 灣仔陳列室，要補的係 **公司／地址／店舖類型**，而唔係重寫成套 Product。

### 而家實際有咩（抓到的）

**每頁都有 Organization（theme 出）：**

```json
{
  "@type": "Organization",
  "name": "COLOURLIVING",
  "url": "https://colourliving.shop",
  "logo": "https://colourliving.shop/cdn/shop/files/COLOURLIVING_LOGO2.png?...",
  "sameAs": [
    "",
    "https://www.facebook.com/colourliving.hk",
    "",
    "https://www.instagram.com/colourliving.hk/",
    "",
    "https://wa.me/85259217909",
    "",
    "",
    "https://www.xiaohongshu.com/user/profile/..."
  ]
}
```

**首頁另有 WebSite + SearchAction**（站內搜尋）— 呢舊係加分，留住。

**產品頁另有 Product**（以 Alys 床為例）：

| 欄位 | 狀態 |
| --- | --- |
| name, url, image, description | 有 |
| brand = B&B Italia | 有（來自 Vendor，好重要，留住） |
| sku | 有 |
| category | 有（英語分類名） |
| offers.price / priceCurrency=HKD / InStock / url | 有 |
| mpn / gtin | **無** |
| shippingDetails / hasMerchantReturnPolicy | **無**（幾乎所有 Shopify 預設都無） |
| aggregateRating | **無**（冇評價就正確，唔好假造） |

Dornbracht 龍頭頁同樣：brand、sku、價、HKD 有；型號未進 `mpn`。

**分類頁／品牌頁：** 只有 Organization，**沒有** CollectionPage／ItemList。對旗艦店可接受，唔急。

**沒有：** `FurnitureStore` / `LocalBusiness`、地址、電話、營業時間、`areaServed: Hong Kong`。Google 同 AI 單靠呢份 schema **唔知你喺灣仔**。

### 問題分三級

**P0 — 會誤導機械（先修，多數喺 Admin 唔使改 schema 結構）**

1. **`sameAs` 一串空字串**  
   Theme 把未填的社交欄位輸出成 `""`。空 URL 係無效 citation。  
   **做法：** Theme settings／Social media 只填真實連結；空白的刪掉。Facebook、Instagram、小紅書、WhatsApp 已有就留。唔好留空欄。

2. **Contact 頁變成 About**  
   若策略係合併到 About：保持 301 即可（見第 11 份）。若曾想獨立 Contact 先要拆開。Organization.url 應永遠係 shop root `https://colourliving.shop`。

3. **冇實體店類型同 NAP**  
   Default Organization 只有名、logo、部分社交。對 COLOURLIVING 呢個係最大缺口。補 `FurnitureStore` + address + telephone + openingHours。可以用一份 JSON-LD 加喺 `theme.liquid`（見 `playbooks/schema-jsonld-shopify.md`），**或者** 用 theme 的 Store location 功能如果有。  
   **唔好** 再加第二個完整 Product schema。

**P1 — Default 故意冇，唔使為咗 GSC 黃燈改 theme**

GSC 好常報：缺 `shippingDetails`、`hasMerchantReturnPolicy`。呢個係 **Google 建議欄**，幾乎所有原生 Shopify 都會缺。

正確做法：**Merchant Center 填香港運費同退貨政策**（你已有 GMC）。Google 會用 feed 對產品，而唔係逼你手寫 2000 個 Offer。手寫錯（例如寫全球免運）害處大過黃燈。

**P2 — 可增強、排喺產品資料品質之後**

| 缺口 | 點補 | 優先 |
| --- | --- | --- |
| `mpn`（廠方型號 LY153、3502097090） | 變體 Barcode／SKU 欄位或 metafield → 先把型號放進 Admin，先唔急改 Liquid | 中 |
| `gtin` | 有條碼先填；冇就唔好造假 | 低 |
| BreadcrumbList | 可選，theme 有時已有；而家首頁冇 | 低 |
| FAQPage | 只加喺真係獨特 FAQ 的品牌／指南頁；全站共用訂單 FAQ **唔好**標。Google **2026-05 起已唔再顯示 FAQ 豐富結果**，加咗都唔會喺搜尋展開 | 低（對測試工具） |
| CollectionPage | 品牌頁可後加 | 低 |

### 你應該點改（務實順序）

**本週（Admin + 小量 theme）**

1. 清社交空欄，修 `sameAs`
2. 拆開 Contact／About
3. Store details 填 333 Lockhart Road、+852 2295 6263
4. 加一份 **FurnitureStore JSON-LD**（地址、時間、電話）。若同現有 Organization 重複 `@type: Organization`，改成 **一個** `@type: ["Organization","FurnitureStore"]`，唔好兩個 Organization 互搶  
   實施前 View Source 計有幾個 Organization——而家全站已有 1 個，應 **擴充或替換呢個**，唔好再貼多一個 app

**唔好做**

- 安裝「JSON-LD for SEO」之類 app 再輸出第二份 Product（重複 = GSC 錯誤）
- 造 `aggregateRating`
- 為消滅 GSC `shippingDetails` 警告而抄美國免運範例

**點驗證**

1. https://search.google.com/test/rich-results  
   - 首頁：Organization 有地址  
   - 產品：Product 有效（已有效）
2. GSC → 購物／非結構化資料：Product 有效數量應穩定；shipping 警告可忽略直至 GMC 政策填好

### 一句總結 Schema

Default **夠格做電商價錢標記**；**不夠格做香港旗艦店 entity**。你要改的唔係「Shopify schema 寫得差」，而係補 **店舖身份**，同修好 Contact／空 sameAs 呢兩個會令機械讀錯的 bug。產品 schema 暫時留 theme 預設即可。
