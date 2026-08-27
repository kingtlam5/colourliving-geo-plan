# Content 流程（鎖定：catalog 同寫文分開）

呢份係 **唯一** 跟住做的順序。前面文件若把「改 collection」寫入寫文步驟，以呢份為準。

兩段工、唔好撈：

| 段 | 步驟 | 做咩 | 用邊份 SOP | 唔做咩 |
| --- | --- | --- | --- | --- |
| **A. Catalog** | 1 → 2 | 揀 category，優化 **已有** collection／品牌頁／產品頁 | [collection-page-sop.md](collection-page-sop.md)、[product-page-sop.md](product-page-sop.md) | 唔開 Journal、唔砌 bucket |
| **B. 文章** | 3 → 4 → 5 | 由 query 做 bucket → cluster → **只寫 Journal** | [bucket-vs-many-pillars.md](bucket-vs-many-pillars.md)、[pillar-blog-format.md](pillar-blog-format.md) | 唔回頭改 collection 當「寫文」；文內只 **連去** 已優化的頁 |

文章裡出現 collection 連結 = 內連，**唔等於** 呢步再做 collection 優化。

---

## 五步（龍頭為例）

### 1. 揀最優先的 product category

生意：90 日最想要龍頭詢盤。  
輸出：一個 category，例如 **浴室龍頭**。  
停。未搜 keyword，未寫文。

### 2. Optimize 相關 collection、brand、product 頁

**呢步係 On-page catalog，完成先至進入內容策劃。**

- 品類：`/collections/bathroom-faucet`  
- 品牌：`/collections/gessi`、`dornbracht`、`fantini`  
- 英雄產品：例如 Rilievo 等 PDP  

做：H1、答案段、FAQ、內連、中英、title。跟 collection／product SOP。  
**做完就封存。** 之後寫文唔再夾雜「不如返去 fortify collection」。

### 3. 搜呢個 category 最常被問的 queries，歸納成 **bucket**

工具：GSC 查詢（篩 gessi／龍頭／faucet）、Google 自動完成、PAA、舖頭 WhatsApp、AI 試題。  
把問題 **歸類成 2–3 個主題桶**（文章用的範圍），例如：

- 桶：邊度睇／指定歐洲龍頭  
- 桶：香港浴室點樣指定（入牆、呎吋）  
- 桶：到店點睇龍頭  

Bucket = 之後 **文章主題範圍**，唔係 collection 名，亦唔係一篇文題。

### 4. 根據每個 bucket 製作 **keyword cluster**

每個桶拆成數個 cluster：主詞 1 + 輔詞 2 + 支援詞。  
Cluster 告訴你 **一篇文打邊堆近義搜尋**，同點同另一篇拆開。  
（Catalog 邊頁對應邊堆品牌詞，你喺第 2 步已經處理；第 4 步係為 **文章** 組詞。）

### 5. 用呢堆 keywords，就住 bucket theme 寫 **唔同角度** 的文章

只產出 Journal。每篇一個角度、一個主詞、連去第 2 步已優化的 collection／PDP。  
點避免文同文撞：[bucket-vs-many-pillars.md](bucket-vs-many-pillars.md)。  
字數／Q&A／內連：[pillar-blog-format.md](pillar-blog-format.md)。  
示範文：[pillar-gessi-hong-kong.md](pillar-gessi-hong-kong.md)。

呢步 **禁止**：再開品牌頁、改 collection H1、把「唔好寫文改 collection」當成寫作指導。第 2 步已做過 catalog。

---

## 對照：邊份文件屬邊段

| 文件 | 屬 |
| --- | --- |
| collection-page-sop / product-page-sop | **只限步驟 2** |
| 本檔 | 步驟 1–5 總流程 |
| bucket-vs-many-pillars、pillar-blog-format、pillar-gessi-hong-kong | **只限步驟 5**（同 3–4 的詞表） |
| measure-seo-geo | 量度；catalog 同 blog 分開睇 GSC 頁面 |
