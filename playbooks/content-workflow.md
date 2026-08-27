# Content 流程（鎖定：catalog 同寫文分開）

呢份係 **唯一** 步驟編號。其他 playbook 若同呢份打架，以呢份為準。

```
1. 揀一個最優先想優化 SEO 及 GEO 的 product category
2. Optimize 相關的 collection page、brand page、product page
3. 之後搜尋呢個 product category 最常被問的 queries，歸納成 bucket
4. 根據 bucket 再製作 keyword cluster
5. 用呢堆 keywords，就住 bucket theme 寫唔同文章
```

兩段工、唔好撈：

| 段 | 步驟 | 做咩 | 用邊份 | 呢段禁止 |
| --- | --- | --- | --- | --- |
| **A. Catalog** | 1 → 2 | 揀 category，優化 **已有** collection／品牌頁／產品頁 | [collection-page-sop.md](collection-page-sop.md)、[product-page-sop.md](product-page-sop.md) | 唔開 Journal、唔砌 bucket、唔寫文 |
| **B. 文章** | 3 → 4 → 5 | query → bucket → cluster → **只寫 Journal** | [bucket-vs-many-pillars.md](bucket-vs-many-pillars.md)、[pillar-blog-format.md](pillar-blog-format.md) | 唔回頭改 collection H1／答案段；文內只 **連去** 第 2 步已優化的頁 |

文章裡出現 collection 連結 = 內連，**唔等於** 呢步再做 collection 優化。  
講緊點寫文時，**唔好** 突然轉去講 collection SOP。

---

## 五步（龍頭為例）

### 1. 揀最優先的 product category

生意：90 日最想要龍頭詢盤。  
輸出：一個 category，例如 **浴室龍頭**。  
停。未搜 keyword，未寫文，未改 collection。

### 2. Optimize 相關 collection、brand、product 頁

**呢步係 On-page catalog。完成先至進入內容策劃。**

- 品類：`/collections/bathroom-faucet`  
- 品牌：`/collections/gessi`、`dornbracht`、`fantini`  
- 英雄產品：例如 Rilievo 等 PDP  

做：H1、答案段、FAQ、內連、中英、title。跟 collection／product SOP。  
**做完就封存。** 之後寫文唔再夾雜「不如返去改 collection」。

第 2 步用的品牌／品類詞（例如 collection H1 打 `Gessi Hong Kong`）屬 **貨頁**，唔屬第 4 步的文章 cluster。

### 3. 搜呢個 category 最常被問的 queries，歸納成 **bucket**

工具：GSC 查詢（篩 gessi／龍頭／faucet）、Google 自動完成、PAA、舖頭 WhatsApp、AI 試題。  
把問題 **歸類成 2–3 個主題桶**（之後文章用的範圍），例如：

- 桶：邊度睇／指定歐洲龍頭  
- 桶：香港浴室點樣指定（入牆、呎吋）  
- 桶：到店點睇龍頭  

Bucket = 之後 **文章主題範圍**，唔係 collection 名，亦唔係一篇文題。

### 4. 根據每個 bucket 製作 **keyword cluster**

每個桶拆成數個 cluster，每個 cluster 服務 **一篇文**：主詞 1 + 輔詞 2 + 支援詞 4–10（約 7–15 個詞）。  
Cluster 告訴你 **一篇文打邊堆近義搜尋**，同點同另一篇拆開。

第 4 步 **唔係**「把詞分配去邊個 collection」。Collection 喺第 2 步已經優化。  
第 4 步只為 **文章** 組詞。

### 5. 用呢堆 keywords，就住 bucket theme 寫 **唔同角度** 的文章

只產出 Journal。每篇一個角度、一個主詞、連去第 2 步已優化的 collection／PDP。  
點避免文同文撞：[bucket-vs-many-pillars.md](bucket-vs-many-pillars.md)。  
字數／Q&A／內連：[pillar-blog-format.md](pillar-blog-format.md)。  
示範文：[pillar-gessi-hong-kong.md](pillar-gessi-hong-kong.md)。

呢步 **禁止**：再開品牌頁、改 collection H1、把「唔好寫文改 collection」當成寫作指導。第 2 步已做過 catalog。

---

## 混淆示例（以後唔好再咁講）

| 錯（撈埋） | 對 |
| --- | --- |
| 講緊點寫 Gessi 文，突然加「同時 fortify `/collections/gessi`」 | 寫文只講 brief、H2、內連、發布 |
| 把 cluster 畫成「Gessi 詞 → 正規頁 = collection」 | 文章 cluster 指向 **一篇 Journal**；collection 已喺第 2 步處理 |
| 90 日表把「改 collection」同「發布文章」交錯當同一條寫作流程 | Catalog 工單只出現在第 2 步；文章日曆只出現在第 5 步 |
| 「呢篇唔好寫，返去改 collection」寫入寫作 SOP | 角度撞就 **換文章角度**；唔好喺寫作文件重開 catalog |

---

## 對照：邊份文件屬邊段

| 文件 | 屬 |
| --- | --- |
| collection-page-sop / product-page-sop | **只限步驟 2** |
| keyword-clusters.md | **步驟 2** 貨頁詞表（邊個 collection 打邊堆品牌／品類詞） |
| 本檔 | 步驟 1–5 總流程 |
| faucet-season-content-plan | 龍頭示範：跟同一五步，唔另開編號 |
| content-plan-layers | 名詞（category／bucket／cluster／pillar），流程仍以本檔為準 |
| bucket-vs-many-pillars、pillar-blog-format、pillar-gessi-hong-kong、blog-content-sop | **只限步驟 5**（詞表來自 3–4） |
| measure-seo-geo | 量度；catalog 同 blog 分開睇 GSC 頁面 |
