# 點樣改 Shopify 的 llms.txt

Shopify **沒有** Admin 開關叫「編輯 llms.txt」。  
`https://colourliving.shop/llms.txt` 而家係平台自動生成的購物 agent 說明（UCP／Shop skill），所以你喺 Files、Pages、SEO 欄都改唔到。

要改內容，係喺 **現行 theme** 加一個 Liquid 範本。2026 年 5 月起 Shopify 官方做法如下。

---

## 你要改邊個檔？（揀一個就夠）

| 網址 | Theme 檔案 | 用途 |
| --- | --- | --- |
| `/agents.md` | `templates/agents.md.liquid` | 官方「正本」。**加呢一個，三條網址一齊變。** |
| `/llms.txt` | `templates/llms.txt.liquid` | 只改 llms.txt；多數 **唔使** 另開 |
| `/llms-full.txt` | `templates/llms-full.txt.liquid` | 只改 llms-full.txt |

查找順序（以 `/llms.txt` 為例）：

1. 有 `llms.txt.liquid` → 用它  
2. 否則有 `agents.md.liquid` → 用它（**建議你做呢個**）  
3. 否則 → Shopify 預設（你而家見到嗰版）

**COLOURLIVING：只新增 `agents.md.liquid`。** 唔好淨改 `llms.txt.liquid`，否則 ChatGPT 讀 `/agents.md` 仲係預設、Perplexity 讀 `/llms.txt` 先係品牌版，會分裂。

加咗自訂範本會 **整份取代** 預設，唔會同系統合併。所以品牌介紹放上半，UCP 結帳說明要用 `agents` 物件自己寫返下半，唔好刪購物協議。同預設逐段對照：[agents-md-vs-shopify-default.md](agents-md-vs-shopify-default.md)。**唔使**抄返 Shopify 嘅 `## Platform` 開舖廣告。

---

## 逐步做（Admin）

**Step 1 — 複製 theme**

1. **Online Store → Themes**
2. 現行主題 → **⋯ → Duplicate**
3. 喺副本上改，Preview 滿意先 Publish

**Step 2 — 開 Edit code**

現行或副本 → **⋯ → Edit code**

**Step 3 — 新增檔案**

1. 左邊搵資料夾 **Templates**
2. 右鍵 Templates → **Add a new template** 或 **New file**
   - 若選單要你揀類型：揀一個普通 template 都得，重點係檔名
3. 檔名必須完全係：

   ```
   agents.md.liquid
   ```

   唔好寫 `agents.md`、`llms.txt`、`page.agents.md.liquid`

Online Store 的「Add template」有時只准 `page`／`product`。若加唔到：

- 用 **Add a new asset** 唔得（會放錯資料夾）
- 改用 Shopify GitHub 連接、或 theme 的「Add a new file」喺 Templates 底下直接命名
- 或用 Shopify CLI：`shopify theme push` 放入 `templates/agents.md.liquid`

**Step 4 — 貼內容**

檔案必須係 **Markdown + Liquid**，唔可以係 JSON template。

呢個範本 **唔能用** `shop`、`collections`、`pages`（會空白）。只可以用：

- `agents.store_name`、`agents.store_url`
- `agents.ucp_discovery_url`、`agents.mcp_endpoint_url`
- `agents.ucp_versions`、`agents.currency`、`agents.sitemap_url`
- `request`
- 你手寫死的品牌事實（地址、品牌名單）

完整可貼內容見 [agents-md-liquid.md](agents-md-liquid.md)。

**Step 5 — Save**  
未 Publish 副本前，用主題 Preview 開：

`https://colourliving.shop/llms.txt?preview_theme_id=你的theme編號`

或 Preview 網址列的 theme id。

**Step 6 — Publish 後核對（無痕、唔帶 preview）**

打開這三條，開頭應見到「Hong Kong flagship」而唔係一開始就 Shop skill：

- https://colourliving.shop/llms.txt
- https://colourliving.shop/agents.md
- https://colourliving.shop/llms-full.txt

`Ctrl+F` 搜 `333 Lockhart` 同 `ucp.dev`：兩樣都要有。

**Step 7 — 換 theme 要再加一次**

檔案跟住 **嗰份 theme**。將來換 Dawn／複製新主題，預設會返 Shopify 原廠文。Publish 新 theme 前把 `agents.md.liquid` 一齊搬過去。

---

## 唔得嘅方法（避免走錯）

| 做法 | 點解唔 work |
| --- | --- |
| Content → Files 上傳 `llms.txt` | 變成 `/cdn/shop/files/llms.txt`，**唔會**取代 `/llms.txt` |
| 開一個 Page handle=`llms-txt` | 路徑係 `/pages/...` |
| robots.txt 編輯器 | 改唔到 llms |
| App「SEO / llms.txt」亂插 | 可能同 theme 雙重、或改唔到呢個系統路徑 |
| 只改 `layout/theme.liquid` | 呢個 URL 唔行普通 layout |

---

## Shopify 官方注意

文件寫：預設 `agents.md` **刻意唔放** 電郵／電話，因為檔案會被廣泛 cache、任何 agent 都讀到。  
COLOURLIVING 作為旗艦零售，**地址、營業時間、只送香港** 對 GEO 好重要，建議保留。電話／電郵若法務想少暴露，可以刪，留 About 頁同 GBP。

品牌名單只寫而家有售；唔好寫 exclusive，除非合約係。

每季隨品牌進退改一次 `agents.md.liquid`。
