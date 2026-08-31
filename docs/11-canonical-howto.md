# 11 — Canonical 實作：關閉 Contact、產品雙 URL

呢份只教 **你喺 Shopify 要撳邊、睇邊、改邊**。先講結論，再逐步做。

---

## 先講清楚：Canonical 喺 Shopify 唔係「每個產品填一格」

Admin **沒有**「幫 Alys 床填 canonical URL」呢個欄。

Shopify 用 theme 裡一句 Liquid，**全站自動計**：

```liquid
<link rel="canonical" href="{{ canonical_url }}">
```

`canonical_url` 係 Shopify 內建變數。產品頁（包括 `/collections/furniture/products/...` 呢種）會自動計成：

`https://colourliving.shop/products/該產品-handle`

所以 Alys 呢題，**你唔使「寫」canonical——系統已經寫咗。** 你要做的係：核對、唔好改壞、同令內部連結盡量用正規 URL。

我 2026-08-26 抓過即時 HTML，兩條 Alys URL 的 canonical **已經一樣**：

| 你瀏覽器見到的網址 | HTTP | 原始碼裡的 canonical |
| --- | --- | --- |
| `/products/alys-ly153-bed` | 200 | `https://colourliving.shop/products/alys-ly153-bed` |
| `/collections/furniture/products/alys-ly153-bed` | 200 | **同一條** `/products/alys-ly153-bed` |
| `/collections/b-b-italia/products/alys-ly153-bed` | 200 | **同一條** `/products/alys-ly153-bed` |

Sitemap 亦只列出 `/products/alys-ly153-bed`，冇列出 collection 版。Google 主要食 sitemap + canonical，呢個已經係正確做法。

---

## 1. Contact Us → About Us：應該點 close？要唔要 GSC Removal？

**你而家嘅做法係啱的，唔使再開 Contact 頁，亦唔該交 Removals。**

即時狀態：

- `https://colourliving.shop/pages/contact-us` → **HTTP 301** → `/pages/about-us`
- 跳完之後 canonical = About
- Pages sitemap **沒有** contact-us

呢個正正係「關閉一頁、把訊號交俾 About」的標準方法。

### 點解唔好用 GSC「移除網址」

| | 301 去 About | GSC Removals |
| --- | --- | --- |
| 用途 | 永久合併頁面 | 緊急隱藏（洩密、錯價、法律） |
| 時效 | 永久，直到你刪 redirect | 大約半年，之後 Google 會再考慮收錄 |
| 權重 | 傳去 About | **唔傳**，只係暫時唔展示 |
| 客人打舊書籤 | 見到 About | 可能 404 或空白 |

你係 **有意把聯絡資訊併入 About**，要嘅係合併，唔係隱藏。Removals 會同 301 打架，亦唔幫 About 食到舊「contact」搜尋。

**例外先用 Removals：** 頁上有私人資料、錯價、你想搜尋結果即刻消失。Contact→About 唔屬呢類。

### 你要做嘅（確認 + 收口），逐步

**Step 1 — 確認 301 仍然存在（2 分鐘）**

1. 開無痕視窗
2. 去 https://httpstatus.io/ （或 Chrome 開發者工具 → Network，勾 Preserve log）
3. 輸入 `https://colourliving.shop/pages/contact-us`
4. 應見到 **301**，Location `/pages/about-us`（或完整 About URL）
5. 最終頁係 About，網址列變成 `/pages/about-us`

Shopify Admin 對應位置：

1. 左邊 **Content → Menus** → 右上 **URL redirects**  
   （舊后台：**Online Store → Navigation** 最底 **View URL redirects**；Admin 搜「redirect」都得）
3. 應有一行：

   | Redirect from | Redirect to |
   | --- | --- |
   | `/pages/contact-us` | `/pages/about-us` |

4. 若 **沒有** 呢行但網站仍會跳：可能係 Pages 裡 contact-us 的 handle 被改過，或舊頁刪除時 Shopify 自動建咗 redirect。**留住，唔好刪。**

**Step 2 — 確保沒有獨立 Contact 頁再被發佈**

1. **Online Store → Pages**
2. 搜 `contact`
3. 若仍有「Contact」草稿／已發佈頁：  
   - **Unpublish** 或 Delete  
   - 刪除時 Shopify 會問是否 redirect → 選 redirect 去 `/pages/about-us`
4. 唔好再新建 Contact 頁

**Step 3 — 全站連結改去 About（避免自己製造新索引）**

逐個檢查，全部改連 About：

1. **Online Store → Navigation** → 每個選單（Main、Footer）  
   若有 Contact 項 → 改指向 About 頁，或刪除該項
2. Theme **Customize → Footer** 文字連結
3. 首頁／產品頁 WhatsApp、Book visit 可以留；「Contact us」字眼連去 About 的聯絡區塊
4. 用網站搜尋 `contact-us` 或瀏覽器全站搵（Chrome：網站內唔得，用 theme 預覽或 GSC 稍後睇）

**Step 4 — GSC 做監察，唔做 Removal**

1. 開 Google Search Console（`.shop` property）
2. 上面搜尋欄貼：`https://colourliving.shop/pages/contact-us`
3. **URL 檢查** → 過幾日／幾週應變成「網頁未編入索引」或「有重新導向」
4. **網頁索引** 裡若 contact-us 出現「網頁有重新導向」，即係成功，**唔使** 去「移除網址」

若三個月後 `site:colourliving.shop/pages/contact-us` 仍出結果，先再查 redirect 有冇斷。仍然 **優先修 301**，唔好第一日就 Removal。

**Step 5 — About 頁要接得住「聯絡」意圖**

既然策略係 About = 聯絡，About 必須有（人眼可見，唔單止 footer）：

- 地址 333 Lockhart Road
- 電話、WhatsApp、電郵
- 營業時間
- 地圖或「點去灣仔」
- 預約表單（如有）

否則 Google 合併咗 URL，但 About 答唔到「contact」搜尋。

---

## 2. 產品雙 URL：點樣令兩條都指向同一條？（逐步）

以 Alys 為例，Shopify **允許兩條都打開**（所以你睇到一樣內容），但 **只聲明一條正規**。呢個係平台設計，唔係你漏設。

```
客人／連結可能用：
/collections/furniture/products/alys-ly153-bed   ← 仍然 200，方便「喺傢俬分類裡睇呢張床」

Google 應計算權重去：
/products/alys-ly153-bed                         ← 正規
```

### A. 先核對（你自己做一次，建立信心）

**Step A1**

無痕開：  
https://colourliving.shop/collections/furniture/products/alys-ly153-bed

**Step A2**

頁面空白處右鍵 → **查看網頁原始碼**（View Page Source），唔好用「檢查元素」估。

**Step A3**

`Ctrl+F`（Mac：`Cmd+F`）搜：

```
rel="canonical"
```

**Step A4**

你應該見到 **只有一條**：

```html
<link rel="canonical" href="https://colourliving.shop/products/alys-ly153-bed">
```

注意：網址列仍然係 `/collections/furniture/products/...`，**呢個正常**。Canonical 唔會改網址列；只有 301 先會改。

**Step A5**

再開正規頁 https://colourliving.shop/products/alys-ly153-bed  
同樣搜 `canonical`，應係 **同一條** href。

兩個都係同一條 = **已經完成「兩個 URL 指向同一 link」。** 唔使再喺 Admin 填一次。

若你見到兩條 `rel="canonical"`，或者 collection 版指向自己（`.../collections/furniture/products/alys-ly153-bed`），先去下面 **C. 修好 theme**。

---

### B. 你唔使喺每個產品寫 canonical（Admin 冇呢格）

產品後台 **Search engine listing** 只有：

- Page title
- Meta description  
- URL handle（例如 `alys-ly153-bed`）

Handle 決定正規路徑係 `/products/alys-ly153-bed`。  
**沒有**「Canonical URL」輸入盒。唔好把 handle 改到連 collection。

---

### C. 去 theme 睇（同萬一寫壞時點改）— 逐步

**Step C1**

Shopify Admin → **Online Store → Themes**  
現行主題 → **⋯ → Edit code**  
（建議先 **Duplicate** 一份 theme 先改）

**Step C2**

左邊開 `layout/theme.liquid`

**Step C3**

喺檔案搜 `canonical`（編輯器有搜尋）。

標準、正確嘅寫法係 **一句、用 Shopify 變數**：

```liquid
<link rel="canonical" href="{{ canonical_url }}">
```

`{{ canonical_url }}` 在 collection 產品 URL 上，Shopify 會輸出 `/products/handle`。**唔好改成** `{{ request.path }}` 或而家呢頁的網址，否則兩條 URL 會各自 canonical 自己，變成重複內容。

**Step C4 — 三種常見錯，對住改**

| 你見到 | 問題 | 改法 |
| --- | --- | --- |
| 完全冇 `rel="canonical"` | Theme 刪咗 | 喺 `</head>` 前加返上面一句 |
| 有兩句 canonical | SEO app + theme 重複 | 停一個；只留 `{{ canonical_url }}` |
| 寫死 `href="{{ shop.url }}{{ collection.url }}/products/{{ product.handle }}"` | collection 版會指自己 | 改返 `{{ canonical_url }}` |

**Step C5**

Save → 重複 **A1–A4** 核對 Alys collection URL。

**唔好** 手寫死 Alys 的 URL。一句 Liquid 服務全部產品。

---

### D. 減少「第二條 URL」被大量發現（建議做，仍然唔使 301 全 catalog）

Canonical 已夠 Google 合併。你再做呢步，係避免自己主題不停把 Google 帶去 collection 版。

Shopify 產品卡有兩種連結：

```liquid
{{ product.url }}
{% comment %} → /products/alys-ly153-bed   ← 要用呢個 {% endcomment %}

{{ product.url | within: collection }}
{% comment %} → /collections/furniture/products/alys-ly153-bed   ← 會製造第二條 URL {% endcomment %}
```

**Step D1**

Edit code → 搜尋整個 theme：

```
within: collection
```

或

```
within:collection
```

**Step D2**

出現嘅 `href="{{ product.url | within: collection }}"`  
改成：

```liquid
href="{{ product.url }}"
```

常見檔案：`snippets/product-card.liquid`、`snippets/card-product.liquid`、`sections/main-collection.liquid`。

**Step D3**

Save → 去 Furniture collection → 右鍵一張床 **Copy link address**  
應係 `/products/...` 而唔係 `/collections/furniture/products/...`。

客人從分類點入後，網址列就係正規 URL。Collection 版 URL 仍然存在（有人舊連結、Google 舊索引），但靠 canonical 合併——**呢個可以接受。**

---

### E. 要唔要做 301？（通常唔使）

有人想網址列都統一，把

`/collections/furniture/products/alys-ly153-bed` → 301 → `/products/alys-ly153-bed`

- **優點：** 瀏覽器網址都乾淨  
- **缺點：** 要為每個「分類 × 產品」做 redirect；Shopify **沒有**「一鍵 301 所有 collection 產品 URL」；手做幾千條唔實際  
- **Google 官方立場：** 200 + 正確 canonical 已經可以合併重複

**所以 COLOURLIVING 唔建議為 Alys 人手加 URL Redirect。** 核對 canonical + 改 `within: collection` 就夠。

若你仍然想 301 **單一測試**：

1. Online Store → **URL Redirects → Create URL redirect**
2. Redirect from：`/collections/furniture/products/alys-ly153-bed`
3. Redirect to：`/products/alys-ly153-bed`
4. Save  
呢個只影響呢一條路徑，**唔會**自動套用全部產品。唔好當全站方案。

---

### F. 用 GSC 確認 Google 聽咗（一週後）

1. GSC → 網址檢查  
2. 貼 `https://colourliving.shop/collections/furniture/products/alys-ly153-bed`
3. 睇「Google 選用的規範網址」應係  
   `https://colourliving.shop/products/alys-ly153-bed`
4. 若仍顯示 collection 版：等索引、確認只有一條 canonical、內部連結已改；**唔好** 對 collection 版提交 Removal

Sitemap 已只有正規產品 URL，呢邊你唔使改。

---

## 一張對照表

| 情況 | 正確 close／合併方法 | 唔好做 |
| --- | --- | --- |
| 有意唔要 Contact 頁 | **永久 301** → About；選單改連 About | GSC Removals；刪頁變 404 又唔 redirect |
| 產品 `/collections/.../products/...` | Theme `{{ canonical_url }}`（你已生效）；連結用 `product.url` | 每個 SKU 人手填 canonical；Removal 掉 collection URL |
| 真係洩密／錯頁要即刻從搜尋消失 | 先 301 或 noindex，急先先 Removals | 只用 Removals 當長期 SEO |

**一句：** Contact 用 301 收口；產品雙 URL 用 Shopify 已有的 canonical，你去原始碼核對同改產品卡連結，而唔係喺 Admin 逐隻貨「寫 canonical」。
