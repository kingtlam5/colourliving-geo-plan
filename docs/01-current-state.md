# 01 — 現況診斷（Launch 約兩個月）

診斷日期：2026-08-25。基於公開網頁、robots、agents.md、搜尋結果與競品對照，**未登入** 你們的 GSC / GA4 / Merchant Center。內部數據要用 [07-measurement.md](07-measurement.md) 的清單自己跑一輪，把本文件的「假設」改成「事實」。

總評：網站視覺同品牌調性已經係旗艦店水平；**搜尋系統仍處於「新網域 + 舊網域互食 + 產品頁未為香港搜尋而寫」的階段。** 呢個階段做對 5 件事，效果會遠大於寫 50 篇 blog。

診斷未登入 GSC／GA4，部分技術觀察（例如舊 `.com` 內頁 404、中文未 publish）需用內部工具覆核。

---

## 發現 1 — 雙域名互食（最高優先）

| 域名 | 角色（而家） | 風險 |
| --- | --- | --- |
| `colourliving.com` | 舊站仍在線，Google 品牌搜尋仍常指向它；聯絡頁、部分經銷商名錄仍引此域 | 舊權重、舊產品 URL、舊內容同新站搶 |
| `colourliving.shop` | 新 Shopify，launch ~2 個月 | 新域權威低，未繼承 `.com` 的歷史連結 |

公開頁面已見到衝突：

- Contact 頁寫 `https://www.colourliving.com`
- Herman Miller「Where to buy」仍指向 `colourliving.com`
- `colourliving.com/` 而家係 **302** 去 `.shop` **首頁**（唔保留路徑）；內頁例如 `/pages/about-us` 回 **404**。應改 **301** 並映射舊路徑，做法見 [09-faq-implementation.md](09-faq-implementation.md)

**含義：** 未處理 301 同 citation 之前，所有 SEO 投入都會漏去舊站。呢個唔係「優化題」，係「架構題」。處理方法見 [03-foundation.md](03-foundation.md)。

---

## 發現 2 — 產品頁係目錄卡，唔係購買／預約頁

以 `Alys LY153 Bed` 為例，優點同漏洞並存：

**已有（要保留）**

- SKU、品牌、產地、系列、設計師、設計年份、呎吋、面料
- 陳列室 4 步流程
- 香港送貨政策

**未有（會輸俾競品同 AI）**

- Title 以型號為主（`Alys LY153 Bed`），缺少「B&B Italia / 香港 / 雙人床」等檢索詞
- Design Story 係品牌原文，無香港場景（呎吋是否適合本地單位、床褥尺寸、陳列室可睇）
- FAQ 全站共用（訂單、退貨），**沒有產品 FAQ**
- 無「誰適合買 / 相關單品 / 對比 / 設計師預約 CTA」的獨立內容區塊
- 部分浴室產品中文頁 Description 只係把規格串成一行英文

浴室分類產品名更嚴重，例如 `Rilievo 59001299`、`Cono 45503031`：人睇唔明係龍頭定配件，Google 同 AI 都難理解。

---

## 發現 3 — 中文版未真正「可被香港搜尋」

已確認：

- 產品 URL 存在 `/zh/products/...`
- 介面按鈕已譯（添加到購物車、願望清單）
- **產品標題、描述、規格標籤多數仍係英文**
- 中文頁出現模板洩漏：`產品類型: {"bath"=>"Bath", "furniture"=>"家具"...}`
- 編碼損壞：`LISS? Concealed thermostat`（應為 LISSÉ）
- `/zh` 首頁、部分 collection 路徑回 404（至少喺公開抓取時）
- 未見到穩定的 `zh-HK` 語言標示；用 `/zh/` 容易被當成通用中文而非香港繁體

香港客人會搜：「意大利梳化 香港」「Gessi 龍頭」「獨立浴缸 香港」「灣仔傢俬店」。而家中文需求幾乎冇對應頁面語言。

---

## 發現 4 — 資訊架構（IA）對搜尋不友善

| 觀察 | 問題 |
| --- | --- |
| Bath collection handle 係 `/collections/bath-1` | URL 帶 `-1`，唔像正規分類 |
| Furniture 198、Bath 232，靠 Shopify filter 分「2 Seater Sofa / Wall-Hung Toilet」 | Filter URL 已被 `robots.txt` Disallow（正確，避免無限組合），但 **獨立可索引子分類頁不足** |
| 品牌 collection 已有（如 B&B Italia） | 品牌頁文案短，未寫「香港授權零售 / 陳列室哪層 / 可預約」 |
| Popular Search 只有 Sofa、Bed、Faucet 等英文詞 | 未接住中文搜尋詞 |
| 舊 blog `/blogs/trends` 多為 2022 hospitality 稿 | 過時、無更新、對零售客人搜尋意圖弱 |

頂級店應該有一層「可索引的語義目錄」：

`品牌頁 → 品類頁 → 場景頁 → 產品頁`

而唔係只有一個大 collection + 一堆 filter。

---

## 發現 5 — GEO 入口存在，但內容係 Shopify 預設

好消息：Shopify 已提供

- `https://colourliving.shop/agents.md`
- `https://colourliving.shop/llms.txt`
- UCP / MCP 商務協議
- 產品 `.json` 可供 agent 讀

壞消息：**`llms.txt` 同 `agents.md` 幾乎全係 Shopify 通用結帳說明**，沒有講：

- COLOURLIVING 係邊間公司
- 灣仔旗艦店地址
- 代理哪些歐洲品牌
- 只送香港
- 陳列室預約點運作
- 中英雙語
- 官方聯絡

AI 助手若只讀 `llms.txt`，會把你們當成「又一間 Shopify 店」，而唔係「香港頂級歐洲家居旗艦」。呢個係 GEO 最便宜、槓桿最高的修復點。

Sitemap：部分抓取工具對 `https://colourliving.shop/sitemap.xml` 曾回 500；2026-08-26 用 GET 覆核為 **200**，子 sitemap（products／pages）亦 200。以瀏覽器打開同 GSC → Sitemaps 為準，見 [09-faq-implementation.md](09-faq-implementation.md) 第 6 題。

---

## 發現 6 — 本地實體訊號分散

旗艦店事實很強：333 Lockhart Road、三層、B&B Italia 獨立 showroom 曾獲設計獎、Time Out / BODW 有歷史報道。但網站 About 用「全球視野、超越國界」這類空句，**沒有把「香港唯一／授權／2,000sqm／洛克道」寫成可引用事實**。

Contact 仍指去舊域。NAP（Name, Address, Phone）喺舊站、新站、LinkedIn、經銷商名錄可能唔一致。AI 同 Google 都靠一致性建立 entity。

---

## 發現 7 — 內容同競品的差距

香港同級店（Andante / Minotti、Atelier A+ / Cassina、Louvre Gallery、MyConcept）已經開始做：

- 「How to buy [品牌] in Hong Kong」指南
- 品牌授權敘事
- 陳列室體驗內容

COLOURLIVING 有更好的品牌組合（B&B Italia + Maxalto + Giorgetti + Gessi + Dornbracht + Flos），但 **網上幾乎沒有把「授權零售商 + 香港陳列」寫成可被引用的百科式頁面**。舊 blog 停喺 2022。

---

## 發現 8 — 衡量堆疊已在，未變成營運系統

GSC、GA4、Merchant Center 已裝，代表技術門檻已過。Launch 兩個月最常見的空白係：

- GSC 未分 `en` / `zh` 屬性或過濾
- 未提交 sitemap / 未處理 404、重複、軟 404
- GA4 未標示「預約陳列室 / WhatsApp / 產品查詢」為轉換
- Merchant Center 未對齊 Shopify 價格、缺貨、GTIN/MPN
- 完全沒有 AI 搜尋監測（問 ChatGPT 十條題，記錄有冇被點名）

工具在，系統不在。

---

## 優先級總表（先做邊樣）

| 優先 | 項目 | 點解先做 |
| --- | --- | --- |
| P0 | 域名策略：`.com` → `.shop` 301，統一 citation | 否則所有優化被舊站稀釋 |
| P0 | 修復 sitemap、中文 404、模板洩漏、亂碼 | 爬蟲同客人同時受傷 |
| P0 | 品牌版 `llms.txt` + Organization schema + NAP | SEO + GEO 共同地基 |
| P1 | 產品標題／描述模板 + 主力 SKU 重寫（中英） | 最大頁面數量、最大長尾 |
| P1 | 可索引品牌頁 + 品類頁（唔只 filter） | 接住「Gessi 香港」「意大利梳化」 |
| P1 | Google Business Profile 同所有名錄改指向 `.shop` | Local + 品牌 |
| P2 | 12 篇「香港邊度買 / 點樣選」權威頁 | GEO 引用原料 |
| P2 | 產品 FAQ、內部連結、Merchant 資料品質 | 轉換 + 購物結果 |
| P3 | PR、設計師內容、持續 blog | 有地基先有複利 |

詳細做法唔寫喺呢度，分別喺 03–08 同 playbooks。
