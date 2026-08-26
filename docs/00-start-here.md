# 00 — 點樣開始：計劃總覽

## 你而家處於邊個階段

網站已經用 Shopify 砌好、launch 約兩個月，Google Search Console、Google Merchant Center、Google Analytics 已安裝。英文版完成，中文版翻譯約七成，產品頁部分產品資料仍係英文。

呢個階段最容易犯兩個錯：

1. **亂加內容**：未搞清楚 entity、域名、hreflang，就開始寫 blog。
2. **當自己係快消電商**：用「流量 → 加購物車」去衡量頂級傢俬。COLOURLIVING 的真正轉換多數係 WhatsApp、預約陳列室、設計師報價，而唔只係線上 checkout。

正確順序係：**先把搜尋系統的地基打穩，再擴內容，再進 AI 引用。**

---

## 兩個詞要分清楚

| 詞 | 全寫 | 贏嘅場 |
| --- | --- | --- |
| **SEO** | Search Engine Optimization | Google / Google.hk 傳統結果、購物結果、地圖 |
| **GEO** | Generative Engine Optimization | ChatGPT、Perplexity、Gemini、Google AI Overviews / AI Mode 的回答入面被點名、被引用 |
| **Local SEO** | 本地搜尋（SEO 的一層） | 「灣仔傢俬」「Lockhart Road furniture」「Gessi 香港門市」 |

本計劃三場一齊打。香港頂級家居零售，三場缺一都會輸：客人會 Google 品牌、會問 ChatGPT「香港邊度有 B&B Italia」、亦會喺地圖搵灣仔陳列室。

GEO **唔係** Geographic SEO 的縮寫。Geographic / Local 會喺地基文件單獨處理。

---

## 呢盤生意嘅搜尋本質

COLOURLIVING 係「House of Brands」：灣仔洛克道 333 號約 2,000 平方米旗艦店，代理歐洲高級傢俬、燈飾、浴室用具（龍頭、浴缸、智能廁所等）。送貨只限香港，不接受海外運送。

搜尋意圖分四類，權重唔同：

| 意圖 | 例子 | 網站任務 | 真正轉換 |
| --- | --- | --- | --- |
| **品牌** | colourliving、colour living 灣仔 | 保護品牌、唔好俾舊站 `.com` 食晒 | 到店 / WhatsApp |
| **品牌 + 產品** | Gessi 香港、B&B Italia Hong Kong、Flos Arco 香港 | 成為官方授權零售商答案 | 產品頁 → 預約 |
| **品類 + 香港** | 意大利傢俬香港、高級浴缸香港、設計師燈飾 | 分類頁 + 指南贏中長尾 | 瀏覽 → 詢盤 |
| **項目 / 場景** | 豪宅浴室翻新、開放式廚房龍頭、2,000 呎單位梳化 | 內容頁 + 陳列室服務頁 | 設計諮詢 |

頂級傢俬的 SEO 勝利條件 **唔係**「每月十萬流量」，而係：

- 搜「Gessi Hong Kong」時，Google 同 AI 都話 COLOURLIVING 係授權門市
- 搜「灣仔 高級傢俬」時，地圖同網站一齊出現
- 客人未到店之前，已經喺網站睇到呎吋、設計師、陳列狀態、預約入口

---

## 成功標準（12 個月）

用生意結果，而唔只用排名。

**品牌與實體**

- `colourliving.shop` 成為 Google 品牌搜尋的主結果；`colourliving.com` 不再搶產品頁
- Knowledge 層清晰：地址、電話、營業時間、同一組品牌名
- ChatGPT / Perplexity 問「Where to buy Gessi in Hong Kong」時，穩定點名 COLOURLIVING

**需求捕捉**

- 品牌 + 主力品牌詞（B&B Italia、Maxalto、Giorgetti、Gessi、Dornbracht、Flos）香港意圖進入首頁或前三
- 10–15 個品類頁（梳化、浴缸、龍頭、地燈）喺 zh-HK 同 EN 都有獨立可索引頁
- 有機流量中，中文（繁體）佔比明顯上升（而家產品資料仍偏英文，中文需求幾乎未被接住）

**生意**

- GA4 入面「自然搜尋 → 預約陳列室 / WhatsApp / 產品查詢」成為主要 SEO KPI
- Merchant Center 產品批准率高、價格與庫存一致，Shopping 同免費 listing 穩定
- 設計師 / 項目客戶能用品牌頁同 FF&E 內容找到你們

---

## 工作原則（頂級操盤手會守）

1. **一個正規網址（canonical domain）**。兩個網店同時活著，等於把 50 年品牌權重劈開。
2. **品牌名永遠用 COLOURLIVING**，地址永遠用 `333 Lockhart Road, Wan Chai, Hong Kong`，電話永遠用 `+852 2295 6263`。所有平台同一套 NAP。
3. **歐洲品牌名唔翻譯**。Gessi 就係 Gessi，唔好寫成「傑西」。中文補品類詞：龍頭、浴缸、梳化。
4. **產品頁先於 Blog**。launch 兩個月，最大漏洞係產品標題、描述、結構化資料同中文，而唔係沒有文章。
5. **寫俾人，同時寫俾模型**。每頁開頭 40–80 字要能直接回答一個真實問題。
6. **香港繁體 `zh-HK`**，唔好當自己係台灣站或簡體站。
7. **每週量，每月調，每季先開新內容線**。唔好同步開十條戰線。

執行層（點樣 301、canonical、schema、hreflang）：[09-faq-implementation.md](09-faq-implementation.md)。

下一步：讀 [01-current-state.md](01-current-state.md)。
