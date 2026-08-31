# Pillar blog：最穩的 SEO × GEO 格式（規格書）

適用所有 Journal 支柱，唔限 Gessi。示範文：[pillar-gessi-hong-kong.md](pillar-gessi-hong-kong.md)。

**適用時機：** 流程第 5 步（寫 Journal）。貨頁已喺第 2 步優化。  
**目標：** Google 有一頁可排「問題意圖」；ChatGPT／Perplexity 有一段可抄的事實。  
文內 **連去** collection；**唔好** 同 collection 用同一個 H1。呢份唔教改 collection。

中英 **分開兩篇** 最好（事實一致、唔機翻）。若同頁雙語，兩種語言都要有完整答案段，唔好英文 1,200 字、中文 80 字。

---

## 1. 字數

| | 理想 | 可接受 | 唔好 |
| --- | --- | --- | --- |
| **英文** | **1,000–1,300 words** | 800–1,500 | <600（答唔完）；>1,800（注水、重複 NAP） |
| **中文** | **1,400–1,800 字**（漢字為主，含標點大約 1,600–2,100 字元） | 1,100–2,200 字 | <800 字；或中文只係英文摘要三句 |

開頭 **答案段：** 英文 40–80 words；中文 **80–130 字**。必須一句完整答：邊間店、可睇咩、地址、預約、只送香港。

Meta title：英文 ≤60 字元；中文 ≤28 個漢字左右。  
Meta description：英文 140–160 字元；中文 70–90 個漢字。

---

## 2. Keyword cluster：每款出現幾多次、出現喺邊

Cluster 仍然係：主詞 1 + 輔詞 2 + 支援 4–10。Pillar **唔使** 把 15 個詞各出現 3 次。

以約 1,100 字英文（或 1,600 字中文）為準：

| 種類 | 次數（全文） | 必須出現的位置 | 可選位置 | 禁止 |
| --- | --- | --- | --- | --- |
| **主詞** | **3–5** | H1 一次（可改寫成問題句，含主詞核心）；答案段一次；meta title 一次 | 其中一個 H2；一張圖 alt | 同一段重複；每節開頭都貼 |
| **輔詞 1** | **1–2** | 一個 H2 **或** 一條 FAQ | 一句正文 | 同主詞疊加堆砌 |
| **輔詞 2** | **1–2** | 另一個 H2 或 FAQ（中文篇可放呢度） | 一句正文 | 硬譯塞入英文 |
| **每個支援詞** | **0–1** | 自然提到先寫 | FAQ | 為齊表而寫 |
| **型號／SKU** | **0** 當主詞 | 只放產品連結錨點或一句「例如 Rilievo」 | — | 放進 H1／meta |
| **COLOURLIVING** | **3–6** | 答案段、到店節、CTA | — | 每段都寫 |
| **完整地址** | **1**（可文末 CTA 再簡述一次） | 「去邊」那節寫晒 NAP | 答案段可寫街名 | 每 H2 重複洛克道 333 |

主詞可以係問題句變體：正規 cluster 主詞 `gessi hong kong`，H1 用 `Where to see Gessi taps in Hong Kong` 算 **用咗主詞**，唔使 H1 再寫一次 `gessi hong kong`。

**密度唔用 %。** 1,100 字裡主詞 8 次以上通常已經 stuffing。

URL handle：短、英文、含主詞核心，例如 `gessi-taps-hong-kong`。唔好 `gessi-hong-kong-gessi-龍頭-灣仔-陳列室-指定`。

---

## 3. 要唔要 Q&A？

**要。H2 用問題句係 pillar 預設格式。**

| 區塊 | 用唔用 Q&A | 點解 |
| --- | --- | --- |
| H2（4–6 個） | **要用問題句** | 對 Google People Also Ask、AI 提問、掃描閱讀 |
| 文末 FAQ（3–5 條） | **要** | 短答送貨、預約、獨家、中文詞；人同 AI 都會抄 |
| 整篇做成「Q: A: Q: A:」清單、冇段落 | **唔好** | 冇敘事、內連好醜、好似 FAQ 插件輸出 |
| `FAQPage` JSON-LD | **唔好加**（為博搜尋展開） | Google 2026-05 已取消 FAQ 豐富結果；全站訂單 FAQ 更唔好標 |

H2 例（揀 4–6 個，唔好 12 個）：

- Where can I see / buy [品牌] in Hong Kong?  
- What collections are on display?  
- How do I specify this for a Hong Kong apartment?  
- Where is the showroom and what are the hours?  
- How does this compare with [同店另一品牌]?（可選，1 節即停）

每節先 **2–5 句答完**，先至補充。唔好 H2 之後先寫 400 字背景。

---

## 4. Hyperlink：內連／外連幾多條

以 1,000–1,300 字英文為準（中文篇數字相同）：

| | 理想 | 可接受 | 備註 |
| --- | --- | --- | --- |
| **內連 total** | **5–8** | 4–10 | 少過 3：同貨盤斷開。多過 12：似目錄 |
| 其中 → 正規 collection | **1–2**（同一品牌頁可連兩次：中段 + 近結尾） | 1–3 | 錨點用品牌／品類名 |
| 其中 → 產品 PDP | **1–3** | 1–4 | 真實有售／有圖；唔連 10 隻 |
| 其中 → About／Showroom／政策 | **1–2** | 1–3 | 到店、送貨 |
| 其中 → 其他 Journal | 0–1 | 0–2 | 相關 pillar，唔好連環自插 |
| **外連** | **0–2** | 最多 3 | 見下面 |
| **全文連結總數** | **5–10** | 4–12 | 內+外 |

**外連只准高信任、非競品目錄：**

- 1 條 Google Maps（洛克道店）或 GBP  
- 可選 1 條品牌 **官方** 介紹頁（gessi.com 品牌故事，唔係其他香港 dealer 名單）

**唔好外連：** 競品網店、論壇、未核實媒體稿、Amazon。外連用 `rel` 預設 follow 官方／Maps 即可，唔使 nofollow 自己官方。

**錨點：** 3–8 個詞、可讀。`Gessi collections at COLOURLIVING`、`bathroom faucets`、`333 Lockhart Road on Google Maps`。禁止 `click here`、`this page`、裸貼全條 URL 當正文（側欄除外）。

**頻率：** 大約每 150–250 字一條內連，平均分佈；唔好全部堆在文末。

發布後文章側已完：文內連去貨頁即夠。Collection 要唔要加「Read this Journal」屬第 2 步 catalog 維護，**唔寫入呢份寫作規格**。

---

## 5. 最穩結構（由上到下，照此出 brief）

```
1. H1          問題句或「主題 + Hong Kong」
2. 答案段       40–80 words / 80–130 字  ← GEO 最重要
3. 要點盒       （可選）地址・時間・預約・只送香港・連 collection
4. H2 問題 ×4–6  每節先答後補充；內連織入段落
5. 短清單       1 個即可（2–5 點）：指定時帶咩去舖
6. FAQ          3–5 條，每答 2–4 句
7. CTA          預約 + 電話；地址可簡述
8. （後台）     作者、發布日、2–4 張圖、tags 2–3 個
```

**不要** 的結構：品牌百科 → 歷史 → 設計師傳記 → 最後先講香港；或純產品 gallery 冇句子。

### 要點盒（GEO 極友善，建議每篇都有）

四至六行，事實同 [nap-source-of-truth.md](nap-source-of-truth.md) 逐字：

- COLOURLIVING  
- 333 Lockhart Road, Wan Chai  
- Mon–Sat 10:00–19:00; Sun & PH 12:00–19:00  
- +852 2295 6263  
- Presented: [品牌]（授權詞依法務）  
- Shop: 該 collection 連結  

AI 好常抄盒，唔抄你第四段抒情。

### 圖

2–4 張：陳列室／該品牌牆／1 隻英雄 SKU。Alt 一句人話，主詞最多 1 張用一次。檔名英文 `gessi-wan-chai-showroom.jpg`。

### 作者

顯示名 + 一句「Wan Chai showroom team」。Shopify 開作者。有就加；唔好假借意大利總設計師。

### Article schema

Theme 若已輸出 `BlogPosting`／`Article`（headline、date、image）→ **唔好再加一份**。View Source 搜 `BlogPosting`。冇先至考慮。唔好加 FAQPage。

---

## 6. On-page 檢查清單（發布前）

- [ ] 答案段唔使滾已答到「邊度、可睇、預約、香港送貨」  
- [ ] H1 同 collection H1 **唔完全相同**  
- [ ] 主詞 3–5 次，位置啱；輔詞分佈 H2／FAQ  
- [ ] 內連 5–8，外連 0–2  
- [ ] 完整 NAP 只集中一節  
- [ ] 無 exclusive（除非合約）  
- [ ] 中英兩篇事實一致（時間、地址、只送香港）  
- [ ] Tags 2–3；作者、日期  
- [ ] Collection 頁已加返連呢篇  

---

## 7. 一句記

> 先答、再用 4–6 個問題當 H2、FAQ 收尾；1,000 字英文或 1,500 字中文；主詞四五次放對位；5–8 條內連去貨同陳列室；外連最多兩條去 Maps 或品牌官網。
