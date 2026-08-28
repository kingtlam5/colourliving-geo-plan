# 04 — 頁面、內容系統、中英雙語

地基之後，流量來自 **正確的頁面類型 × 正確的語言 × 正確的內部連結**。

---

## A. 目標資訊架構

```
/ (House of Brands 首頁)
├── /pages/about-us
├── /pages/wan-chai-showroom     ← 必加
├── /pages/for-designers         ← 設計師 / FF&E
├── /collections/furniture
│     ├── /collections/sofas
│     ├── /collections/beds
│     ├── /collections/dining-tables
│     └── /collections/outdoor-furniture
├── /collections/bathroom        ← 取代 bath-1
│     ├── /collections/bathroom-faucets
│     ├── /collections/bathtubs
│     ├── /collections/basins
│     └── /collections/toilets
├── /collections/lighting
│     ├── /collections/floor-lamps
│     └── /collections/table-lamps
├── /collections/kitchen
├── /collections/[brand]         ← gessi, bb-italia, maxalto...
├── /products/[handle]
├── /blogs/journal               ← 新內容樞紐（舊 trends 可 301 過來）
└── /zh-hk/...                   ← 對應全樹
```

**原則：** 客人同 Google 都要能「唔使篩選」就到達一個有獨特文案的 URL。Shopify filter 只服務頁內縮小範圍，唔再承擔 SEO。

子分類頁唔使一次建晒。90 日先建 **搜尋需求最大的 12–18 個**（見 keyword-clusters）。

---

## B. 首頁

**2026-08-28 live audit：** [homepage-audit.md](../playbooks/homepage-audit.md)。而家係視覺旗艦 + 電商目錄，未有可引用定位段。

首頁唔需要塞關鍵字，需要 **可被引用的定位段**（英文 + 中文各一）。**要客人睇到**，唔好 `visually-hidden`（隱藏 H1 得，隱藏整段 GEO 會失效）。點寫、schema 點加 `HomeGoodsStore`：[homepage-positioning.md](../playbooks/homepage-positioning.md)。

> COLOURLIVING is Hong Kong’s House of Brands for European furniture, lighting and bathroom. The 2,000sqm flagship at 333 Lockhart Road, Wan Chai presents B&B Italia, Maxalto, Giorgetti, Gessi, Dornbracht, Flos and other authorised collections. Delivery is available within Hong Kong. Book a showroom visit with a specialist.

而家 About 的「transcending borders and cultures」對搜尋同 AI 都無用。改成事實：面積、地址、品牌、服務（設計諮詢、FF&E、安裝）、送貨範圍。

---

## C. 品牌頁（最高 ROI 的非產品頁）

每個主力品牌一頁，結構固定：

1. **H1**：`Gessi Hong Kong | Authorised Retailer at COLOURLIVING`
   中文：`Gessi 香港｜COLOURLIVING 灣仔授權零售`
2. **40–80 字答案**：係咪授權、陳列喺邊、點預約、只送香港
3. **品牌是誰**（歷史、原產國、設計語言）— 可改寫官網，唔好整頁複製
4. **喺 COLOURLIVING 可睇／可訂邊啲系列**
5. **香港場景**：浴室工程、酒店項目、住宅呎吋
6. **產品 grid**
7. **CTA**：Book showroom / WhatsApp
8. **FAQ**（3–5 條獨特問題）：Is COLOURLIVING an official Gessi dealer? Can I see Gessi in Wan Chai? Do you install?

90 日品牌頁優先：

B&B Italia, Maxalto, Giorgetti, Paola Lenti, Gessi, Dornbracht, Fantini, Flos, Preciosa, Roca, Armani/Roca, Victoria + Albert

**授權用語要合法。** 合約係 exclusive / authorised / stockist，就照實寫。唔好自稱 exclusive 若唔係。

---

## D. 品類頁

每頁只打一個意圖。例：

| Handle | H1 EN | H1 ZH |
| --- | --- | --- |
| sofas | Designer sofas in Hong Kong | 香港設計師梳化 |
| bathroom-faucets | European bathroom faucets | 歐洲浴室龍頭 |
| bathtubs | Freestanding bathtubs | 獨立式浴缸 |
| floor-lamps | Designer floor lamps | 設計師地燈 |

頁面模組：

1. 獨特 150–300 字導購（中英各一，唔好全站複製 About）
2. 篩選（品牌、尺寸、有貨）
3. 點樣選（3 個 bullet：呎吋、面料、陳列室）
4. 連去相關品牌頁
5. 底部再放 100 字本地說明（送貨、預約）

而家 Furniture / Bath collection 底部 About 完全重複，對 SEO 係零。每頁必須有 **unique copy**。

---

## E. 產品頁 SOP

完整步驟見 [playbooks/product-page-sop.md](../playbooks/product-page-sop.md)。這裏只講策略。

### 標題公式

**英文：** `[Brand] [Collection] [Product type] [Key identifier]`  
例：`B&B Italia Alys LY153 Bed` 而唔只係 `Alys LY153 Bed`

**中文：** `[品牌] [系列] [中文品類] [型號]`  
例：`B&B Italia Alys 床架 LY153`

浴室最差的 `Rilievo 59001299` 應變成：  
`Gessi Rilievo basin mixer 59001299` / `Gessi Rilievo 面盆龍頭 59001299`

### 描述分兩層

1. **40–80 字摘要**（人同 AI 都會抄）：品牌、產地、功能、香港陳列／訂貨
2. **規格表**（已有，保持結構化欄位）
3. **香港補充**：送貨、陳列品可能是 display unit、預購價或不同、建議預約量度

### Meta

- Title ≤ 60 字元：品牌 + 品類 + Hong Kong 或 香港（唔好每頁都塞 COLOURLIVING 太長）
- Description ≤ 155：一句利益 + 灣仔可睇 + CTA

### 唔好翻譯的

品牌名、設計師名、系列官方名、型號。

### 必須翻譯的

品類（龍頭、浴缸、梳化）、利益句、送貨、預約、保養、FAQ。

---

## F. 中文（zh-HK）執行順序

唔好等「全 catalog 譯完」先上線 SEO。分批：

**Batch 1 — 模板與 UX（1 週）**

- 修洩漏 JSON、亂碼
- 統一 `zh-HK`
- 導航、篩選、按鈕、政策

**Batch 2 — 錢貨（2–4 週）**

- 所有品牌頁中英
- Top 100 SKU（按庫存、毛利、品牌戰略：Gessi、Roca、B&B、Flos）
- 12 個品類頁

**Batch 3 — 長尾**

- 其餘產品用「標題公式 + 規格欄位中文化」的半自動模板
- 人工只 polish 英雄產品

翻譯品質：請人用 **香港繁體**（浴缸、梳化、陳列室、預約），避免台灣用語（沙發、門市）或大陸用語（馬桶、衛浴潔具）除非該詞本地都通用（洗手盆／面盆可並存，揀一個做 H1）。

產品資料可以中英並列：

```
品牌 Brand：Gessi
產地 Origin：Italy
型號 Model：59001299
```

---

## G. 內容系統（指南頁，唔係「為寫而寫」）

**Content 五步（唔好撈 catalog 同寫文）：** [content-workflow.md](../playbooks/content-workflow.md)  
1 揀 category → 2 優化 collection／品牌／產品 → 3 query 歸 bucket → 4 文章 keyword cluster → 5 先至寫 Journal。

舊 `/blogs/trends` 2022 hospitality 稿可以留作 archive，但 **新內容要用新樞紐**，每篇對應一條可贏的問題。

90 日只寫 **12 篇支柱**（中英可同頁雙語，或兩個 URL 用 hreflang）：

1. Where to buy B&B Italia in Hong Kong
2. Gessi taps Hong Kong: authorised retailer guide
3. Dornbracht vs Gessi vs Fantini（中立對比，導向陳列室）
4. How to choose a designer sofa for a Hong Kong apartment
5. Freestanding bathtub buying guide (HK bathrooms)
6. Flos lighting in Hong Kong
7. Maxalto vs B&B Italia: which collection
8. Visiting COLOURLIVING Wan Chai showroom
9. Bathroom renovation: specifying European faucets in HK
10. Outdoor furniture for HK rooftops / terraces (Paola Lenti, Kettal)
11. For interior designers: FF&E and trade at COLOURLIVING
12. Delivery, lead times and display stock explained

每篇結構（GEO 友好）：

- 開頭直接答
- H2 用問題句
- 事實表（地址、品牌、時間）
- 內連到品牌頁／品類／3 個產品
- 作者真名 + 職位（E-E-A-T）
- 更新日期

產量目標：**每週最多 1 篇支柱**（步驟 5），而唔係每日一篇空文。產品標題改寫屬步驟 2 catalog，唔同寫文週撈埋做。

---

## H. 內部連結

| 從 | 到 |
| --- | --- |
| 首頁 | 8–10 個品牌、3 個品類、陳列室 |
| 品牌頁 | 該品牌英雄產品、相關品類、陳列室 |
| 品類頁 | 2–3 個品牌、1 篇指南 |
| 產品頁 | 品牌頁、同系列 3 個、陳列室 CTA |
| 指南 | 品牌 + 品類 + 預約 |

錨文字用自然短語：`Gessi in Hong Kong`，唔好全部 `click here`。

---

## I. 圖片 SEO

- 檔名：`gessi-rilievo-basin-mixer-chrome.jpg` 而唔係 `IMG_3829.jpg`
- Alt：品牌 + 產品 + 顏色／場景，唔堆關鍵字
- 陳列室實拍（灣仔場景）比純白底更有 Local 同 GEO 訊號
- 平面圖、呎吋圖保留，AI 摘要經常引用尺寸

完成後用 [08-roadmap.md](08-roadmap.md) 排工；寫頁時打開對應 playbook。
