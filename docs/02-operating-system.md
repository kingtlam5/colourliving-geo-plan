# 02 — 系統化操盤：SEO & GEO Operating System

頂級計劃唔係一份「要做事項清單」，而係一個 **每月重複的作業系統**。COLOURLIVING 團隊即使只有 1 個人兼職 SEO，都可以用呢個系統唔迷路。

---

## 五層金字塔（永遠由下而上）

```
        [5] 權威擴散     PR、經銷商名錄、設計師、媒體、評論
       [4] GEO 引用      llms.txt、問答型內容、第三方一致事實
      [3] 頁面與內容      產品 / 品牌 / 品類 / 指南 / 中英
     [2] 技術可被發現     Sitemap、hreflang、schema、速度、Merchant
    [1] 實體與域名        一個官網、一套 NAP、一個 Knowledge 實體
```

Launch 兩個月，80% 時間應留喺第 1–3 層。第 4–5 層好誘人，但地基未穩就寫文章，等於喺沙上建旗艦店。

每層對應文件：

1. [03-foundation.md](03-foundation.md)
2. 同上（技術）+ [07-measurement.md](07-measurement.md)
3. [04-pages-and-content.md](04-pages-and-content.md)
4. [05-geo.md](05-geo.md)
5. [06-authority.md](06-authority.md)

---

## 三個市場、三種語言策略

| 市場 | 語言 | 搜尋習慣 | 頁面策略 |
| --- | --- | --- | --- |
| 香港本地客人 | `zh-HK` 繁體 | 品類中文 + 品牌英文（Gessi 龍頭、意大利梳化） | 中文標題、中文導購、英文品牌名 |
| 香港專業／外籍 | `en-HK` | 品牌 + Hong Kong + authorized dealer | 英文權威頁、規格、設計師名 |
| AI 助手 | 中英都會被問 | 「Where can I buy… in Hong Kong」 | 短事實段落 + schema + 一致 NAP |

Shopify Markets 應設：

- Primary: English (`en` 或 `en-HK`)，x-default 指向英文
- Secondary: 繁體中文香港 (`zh-HK`)，URL 建議 `/zh-hk/` 或 Shopify 的 `/zh-hk`，**避免含糊的 `/zh/`**

---

## 四類頁面，各有一個工作

唔好每頁都想「排名 + 賣貨 + 講品牌故事」。每類頁一個主工作：

| 頁類 | 主關鍵字類型 | 主工作 | 成功睇邊樣 |
| --- | --- | --- | --- |
| 首頁 | 品牌 | 實體聲明：House of Brands、灣仔、代理名單 | 品牌搜尋 CTR、AI 品牌描述正確 |
| 品牌頁 | `[Brand] Hong Kong` / `[品牌] 香港` | 證明授權 + 陳列 + 預約 | 該品牌詞排名與詢盤 |
| 品類頁 | `[品類] 香港` / 意大利梳化 | 幫客人縮小範圍 | 品類印象與點擊入產品 |
| 產品頁 | 型號 / SKU / 系列 | 規格真實、可引用、可預約 | 加入購物車 **或** WhatsApp |
| 指南頁 | 問題型 | 俾 Google 同 AI 抄一段正確答案 | 引用、品牌搜尋增長 |
| 陳列室頁 | 灣仔傢俬 / Lockhart Road | 地圖 + 預約 | 來電、路線、預約表 |

---

## ICE 決策法（每週只挑 3 件事）

每個待辦打三個分數（1–5），乘起來排序：

- **I — Impact**：對品牌詞、主力品牌詞、預約轉換影響有幾大
- **C — Confidence**：有冇數據／明確技術路徑
- **E — Ease**：一個星期內做唔做得完

例子：

| 任務 | I | C | E | ICE |
| --- | --- | --- | --- | --- |
| 修 `.com` 302→301、提交／核對 GSC sitemap | 5 | 5 | 5 | 125 |
| 重寫 `llms.txt` 品牌版 | 5 | 4 | 5 | 100 |
| `.com` 301 規劃 | 5 | 4 | 3 | 60 |
| 重寫 30 個 Gessi / B&B 產品標題 | 4 | 4 | 3 | 48 |
| 寫一篇家居潮流 blog | 2 | 2 | 4 | 16 |

每週只執行 ICE 最高的 3 項。blog 通常排後面，直到 P0 完成。

---

## 兩個漏斗，唔好只用電商漏斗

**漏斗 A — 線上成交（細件、有庫存、生活方式）**

搜尋 → 產品頁 → 加購 → 送貨香港

**漏斗 B — 旗艦體驗（傢俬、浴室工程、項目）**

搜尋 / AI 推薦 → 品牌或指南頁 → 產品規格 → WhatsApp 或預約 → 灣仔陳列室 → 報價

GA4 要把漏斗 B 當成一等轉換。否則 SEO 會被誤判為「冇用」，因為梳化 HK$90,000 很少人直接網上買。

---

## 角色分工（即使只有你一個人）

把工作分成帽子，每週戴一頂主帽：

| 帽子 | 工作 | 建議時段 |
| --- | --- | --- |
| 技術 | GSC 覆蓋、sitemap、hreflang、schema | 週一 90 分鐘 |
| 目錄 | 產品標題、描述、標籤、缺貨 | 週二、四 90 分鐘 |
| 內容 | 跟 [content-workflow.md](../playbooks/content-workflow.md)：步驟 2 改貨頁；步驟 5 先至寫指南 | 週三 120 分鐘（只做其中一段） |
| GEO | 跑 prompt 集、改 `llms.txt`、FAQ | 週五 45 分鐘 |
| 本地 | GBP 帖文、相片、評論回覆 | 週五 30 分鐘 |

完整節奏見 [playbooks/weekly-rhythm.md](../playbooks/weekly-rhythm.md)。

---

## 90 日只打五場仗

詳細日曆喺 [08-roadmap.md](08-roadmap.md)。戰略上只准五場：

1. **統一 entity**：域名、NAP、schema、GBP
2. **令爬蟲同 AI 讀得懂店**：sitemap、中文 URL、品牌 `llms.txt`
3. **重寫錢貨頁**：Top 品牌 × Top 品類的產品與 collection
4. **接住香港中文搜尋**：zh-HK 標題、描述、品類詞
5. **成為可引用答案**：10–12 頁「香港邊度買／點樣選」

90 日後先考慮大規模內容工廠、YouTube SEO、繁簡轉換、海外市場。

下一步：[03-foundation.md](03-foundation.md)。
