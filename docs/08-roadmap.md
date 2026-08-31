# 08 — 90 日執行表

假設資源：1 個內部負責人（你）+ 翻譯支援 + 品牌經理可改 stockist + Shopify 開發少量工時。若只有你一個人，把「每週產品重寫」由 40 減到 15，但 **P0 不准刪**。

日曆由你讀完本計劃的下一週一開始。

---

## 總覽

| 階段 | 日子 | 主題 | 只准贏的結果 |
| --- | --- | --- | --- |
| 0 | 第 1–3 日 | 基準線 | GSC/GA4/GMC 截圖 + 本診斷對照 |
| 1 | 第 1–30 日 | 地基 | 域名、NAP、sitemap、中文修復、llms.txt、GBP |
| 2 | 第 31–60 日 | 錢貨頁（content 步驟 2） | 選定 category 的 collection／品牌／PDP |
| 3 | 第 61–90 日 | 文章（content 步驟 3–5） | 該 category 的 bucket→cluster→Journal；GEO |

---

## Phase 0 — 基準線（3 日）

- [ ] GSC 28 日匯出：queries、pages、國家 HK
- [ ] GA4：自然流量、而家有冇轉換事件
- [ ] Merchant：拒登數量
- [ ] 用 URL Inspection 抽：首頁、`/collections/furniture`、`/collections/bath-1`、一個 `/zh/products/...`、sitemap
- [ ] 跑一次 [geo-monthly-prompts.md](../playbooks/geo-monthly-prompts.md) 當 Day 0
- [ ] 列出 `.com` Top URL（GSC 或爬蟲）準備 redirect map

---

## Phase 1 — 日 1–30 地基

### 週 1

- [ ] 決定並文件化：購物正規網址 = `https://colourliving.shop`；品牌身份網址 = `https://colourliving.com`（301 去店）
- [ ] Footer／Shop CTA 連去 `.shop`；名片／vendor pack 官網保持 `.com`
- [ ] GBP：NAP 對齊；Website 建議 `.com`（301 會帶去店）
- [ ] **唔好** 群發品牌商改 Where to buy 去 `.shop`（見 [com-vs-shop-citations.md](../playbooks/com-vs-shop-citations.md)）
- [ ] 核對 sitemap 喺 GSC 顯示成功（瀏覽器打開 XML 為 200），GSC 提交
- [ ] 修中文模板洩漏、`LISS?` 類亂碼
- [ ] 上線品牌版 `llms.txt`（[草稿](../playbooks/llms-txt-draft.md)）
- [ ] Organization JSON-LD 上首頁

### 週 2

- [ ] Redirect map v1：舊站首頁、About、Contact、Bath、品牌
- [ ] 實施 `.com` 301（可先最大流量 50 條）
- [ ] 語言：確認 Markets = `zh-HK`，修 `/zh` 404
- [ ] hreflang 抽查 5 個 URL
- [ ] Showroom 獨立頁 outline + 上線英文

### 週 3

- [ ] Showroom 中文頁
- [ ] 10 個品牌頁骨架（H1、答案段、CTA），即使產品 grid 已有
- [ ] `/collections/bath-1` → `/collections/bathroom` + 301
- [ ] GA4 轉換：WhatsApp、預約表

### 週 4

- [ ] 其餘 301 批次
- [ ] Product schema 抽查 10 個 PDP
- [ ] 連結 Search Console ↔ GA4
- [ ] Phase 1 複盤：索引錯誤是否下降

**Phase 1 完成門檻：** 見 [03-foundation.md](03-foundation.md) 完成定義。

---

## Phase 2 — 日 31–60 錢貨頁（content 步驟 2）

呢 30 日 **只優化 catalog**，唔寫 Journal。跟 [content-workflow.md](../playbooks/content-workflow.md) 步驟 2。先做完 P0 category（龍頭）相關頁，先至擴其他品牌。

### 週 5–6 品牌與品類

- [ ] 完成 10–12 個品牌頁中英（公式見 04）
- [ ] 建立可索引品類：sofas, beds, dining, faucets, bathtubs, basins, toilets, floor-lamps, table-lamps, outdoor（按實際庫存裁剪）
- [ ] 每頁 unique 150 字 + 內連

### 週 5–8 產品（持續）

每週 20–40 個 SKU 跟 [product-page-sop.md](../playbooks/product-page-sop.md)：

優先順序：

1. 有貨 + 英雄品牌（Gessi, B&B, Flos, Dornbracht, Maxalto）
2. Merchant 已拒登但戰略需要
3. 標題現在只有型號數字的浴室 SKU

- [ ] Admin：vendor、product type、tags 清洗
- [ ] 中文 title / description 先做呢批
- [ ] 圖片改檔名只在新上傳時執行，舊圖唔使海量改

### 週 7–8

- [ ] Merchant 拒登清一輪
- [ ] For Designers 頁上線
- [ ] 內部連結：首頁 → 品牌 → 品類
- [ ] GSC 請求索引品牌頁與新品類

---

## Phase 3 — 日 61–90 被引用

### 內容

跟 [content-workflow.md](../playbooks/content-workflow.md)：該 category 的 collection／品牌／PDP **已喺步驟 2 做完**，呢 30 日只做步驟 3–5（bucket → cluster → Journal）。唔好邊寫文邊改 collection。

今季若 P0 係龍頭，先寫龍頭三篇（見 [faucet-season-content-plan.md](../playbooks/faucet-season-content-plan.md)），梳化／燈飾留下一個 category。每週最多 1 篇支柱（中英）：

1. Gessi：Where to see / specify in Hong Kong（龍頭桶 A）  
2. European faucets：指定香港浴室（龍頭桶 B）  
3. Wan Chai bathroom visit（龍頭桶 C）  
4. （下一 category 先至）B&B Italia / sofa / Flos  

其餘可延入下一季。

### GEO 與權威

- [ ] 聯絡 5 個品牌：**核對 NAP（地址／電話／營業）**；官網欄若已係 `colourliving.com` 就 **唔改**。只修 404 深鏈或錯地址
- [ ] 第二次、第三次 GEO prompt 監測（日 60、日 90）
- [ ] GBP 每週帖 + 邀請 10 個近期到店客人留評
- [ ] 1 則設計媒體投稿或新聞（新系列即可）

### 日 90 複盤

對比 Phase 0 基準線：

- 品牌詞點擊  
- 主力品牌詞曝光  
- 中文頁點擊  
- Organic → lead  
- GEO mention rate  
- `.com` vs `.shop` 誰主導品牌 SERP  

決定下一季：係繼續清 catalog 中文，定係加 video / 小紅書 SEO。**唔好同時開。**

---

## 90 日之後（故意不在本計劃展開）

- 全 catalog 中文
- YouTube：陳列室 walkthrough
- 繁簡（只有當要做大灣區）
- 大規模 PR
- 程式化頁面（每個尺寸 × 每個品牌）— 容易製造垃圾頁，需另案評估

---

## 風險同備案

| 風險 | 備案 |
| --- | --- |
| `.com` 301 要 IT／舊平台權限 | 先改所有新站自引同 GBP，舊站至少加 canonical + 首頁 301 |
| Shopify 覆蓋 `llms.txt` | 放喺可編輯的 Files + app，或 theme 額外 route |
| 翻譯人手不足 | 只做 Batch 1+2，其餘產品中文 title 用「品牌+品類+型號」模板 |
| 品牌唔肯改 stockist | **唔使堅持改網址。** 只跟錯地址／404；官網 `.com` 係正確終態 |
| 高價貨無 GTIN | Merchant 用 MPN + 正確設定，唔好填假 GTIN |
