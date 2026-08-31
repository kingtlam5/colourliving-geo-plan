# 點樣 Benchmark 同 Measure（只用你已有的工具）

你手頭：**GSC、GA4、Google Merchant Center、Shopify**，加免費網頁工具。唔使 Ahrefs／Semrush。

原則：

1. **先影 Day 0**，否則 90 日後冇得比。  
2. 跟金字塔由下而上量：地基 → 技術 → On-page → Blog → GEO → 生意。上層好睇、下層先決定你有冇資格贏。  
3. Luxury：**WhatsApp／預約 > 訂單數**。Organic 帶來 3 個高單預約，仍然算贏。  
4. 一次只解讀一個層，唔好用總點擊升跌解釋 schema。

建議一個 Google Sheet，分頁：`Day0` `Weekly` `Monthly-GEO` `Queries` `Pages` `Leads`。數字抄入格，screenshot 另存 Drive 資料夾 `SEO-GEO-baselines/YYYY-MM-DD/`。

---

## 0. 今日做一次：全系統基準線（約 2–3 小時）

日期寫低。之後所有「有冇效」都對呢日。

### 0.1 GSC（Search Console）

Property：`colourliving.shop`。日期：**過去 28 日**（launch 兩個月用 28 日；之後可加 3 個月）。

1. **成效 → 總覽**  
   抄：總點擊、總曝光、平均 CTR、平均排名。Screenshot。  
2. **成效 → 查詢** → 匯出。另篩國家/地區 = **Hong Kong** 再匯出一份。  
3. **成效 → 頁面** → 匯出 Top 頁。  
4. 查詢搜尋框分別貼（抄點擊／曝光／排名，冇就寫 0）：  
   `colourliving` `gessi hong kong` `gessi 香港` `龍頭` `dornbracht` `b&b italia hong kong` `灣仔傢俬`  
5. **網頁索引 → 網頁**：抄「已編入索引」約數；開「未編入索引」睇最大原因（已發現尚未編入／404／重新導向）。Screenshot。  
6. **Sitemaps**：成功／失敗。  
7. URL 檢查（只記結果，唔使全 catalog）：  
   首頁、`/collections/gessi`、`/collections/bathroom-faucet`、一個產品、`/pages/about-us`、若已發 blog 就加該 URL。  
   抄：已索引 Y/N、最後爬取日、規範網址。  
8. 若有 `colourliving.com` property：同樣 28 日點擊（預期近 0 或全係首頁 redirect）。

### 0.2 GA4

1. **報告 → 獲客 → 流量獲客**：主要管道。抄 Organic Search 工作階段、使用者。  
2. **報告 → 參與 → 到達網頁**：Top landing。  
3. **探索** 或標準報告：有冇 `purchase`、表單、WhatsApp 點擊。**冇轉換就記「未設」**——呢個本身係 Day 0 發現，要先設先至能量生意。  
4. 日期範圍同 GSC 對齊 28 日。國家 Hong Kong（若有）。

Shopify Google channel 若已連 GSC／GA4，確認係同一個 GA4 property。

### 0.3 Merchant Center（GMC）

1. **產品 → 診斷**（或 Needs attention）：拒登數量、警告數量。Screenshot。  
2. 若有 **免費資訊主頁／Performance**：28 日曝光／點擊（有就抄；冇就寫 N/A）。  
3. Feed 最後成功同步時間。

**唔好** 把 Shopping 廣告點擊當成 SEO。

### 0.4 Shopify Admin

1. **Analytics → 報告**：網上銷售、工作階段（若有）。28 日總銷售、訂單。  
2. 有 **銷售渠道／推薦來源** 就抄 Direct vs Search（Shopify 分類粗，只作對照）。  
3. 記：WhatsApp app 有冇、預約用邊個表。

### 0.5 免費工具（技術＋GEO 原料）

| 測咩 | 工具 | Day 0 做 |
| --- | --- | --- |
| `.com` 轉址 | https://httpstatus.io/ 貼 `colourliving.com` | 記 302 定 301 |
| Schema | https://validator.schema.org/ 貼首頁 | 有冇 address／FurnitureStore |
| Rich results | https://search.google.com/test/rich-results 首頁 + 一個產品 | 首頁可能 0 items（正常）；產品應有 Product |
| 速度 | https://pagespeed.web.dev/ 首頁手機 | 只記 Performance 分數當參考，唔當 KPI |
| 公開索引 | Google：`site:colourliving.shop` 同 `site:colourliving.com` | 粗略頁數 |
| AI | [geo-monthly-prompts.md](geo-monthly-prompts.md) 最少浴室 4 題 + 品牌 2 題 | 見第 5 層 |

---

## 1. 地基（實體、域名、NAP）

**成功定義：** 品牌搜尋同地圖認同一間灣仔店；`.com` 唔再用 302 漏權重。

| 你想證明 | 工具 | 點取數 | 頻率 | 健康樣子 |
| --- | --- | --- | --- | --- |
| `.com` 已 301 | httpstatus.io | 根網址狀態碼 | 改 DNS 當日 + 一週後 | **301** → colourliving.shop |
| Google 認 `.com` 轉址 | GSC `.com` → URL 檢查首頁 | 「網頁有重新導向」 | 改完 1–2 週 | 已索引 ≈ 0；排除=redirect |
| 品牌詞點擊 | GSC 查詢 `colourliving` | 點擊、CTR、排名 | 每週 | 28 日後點擊唔跌；排名趨向 1–3 |
| NAP 一致 | 人手：網站 footer、GBP、schema.org validator | 地址電話逐字 | 改 schema／footer 當日 | 同 [nap-source-of-truth.md](nap-source-of-truth.md) |
| GBP 網站掣 | 手機開 Maps 店頁 | 撳網站去邊 | 改 GBP 後 | 去到店（經 301 都得） |

**解讀：** 品牌詞點擊升、但 Organic 轉換未設 → 只證明「搵到舖」，未證明「預約」。唔好用呢層解釋 blog。

---

## 2. 技術（索引、sitemap、schema、Merchant、hreflang）

**成功定義：** 戰略頁可被抓、產品標記冇壞、Merchant 英雄貨上架。

| 你想證明 | 工具 | 點取數 | 頻率 | 健康樣子 |
| --- | --- | --- | --- | --- |
| 索引規模 | GSC 網頁索引 | 已編入索引 | 每週 | 穩升或持平；唔好突然少一半 |
| 404／錯誤 | GSC 未編入索引 → 未找到、伺服器錯誤 | 數量同例子 URL | 每週 | `/zh` 亂 404、bath-1 趨降 |
| Sitemap | GSC Sitemaps；瀏覽器開 `/sitemap.xml` | 成功、發現網址數 | 每週 | 200、無失敗 |
| 戰略頁已收 | GSC URL 檢查 | Gessi、bathroom-faucet、英雄 PDP | 改完請求索引後 3–14 日 | 已編入索引 |
| Organization → FurnitureStore | validator.schema.org | 有 streetAddress | Publish schema 當日 | 有 333 Lockhart Road |
| 產品 Rich result **合格** | Rich Results Test 貼 PDP | 偵測到 Product | 改 theme 後抽 2 隻 | Valid；唔好首頁當 Product 測 |
| 購物 feed | GMC 診斷 | 拒登數 | 每週 | 英雄品牌拒登 → 0 |
| 中文頁（publish 後） | GSC 頁面篩 `/zh`；URL 檢查 hreflang | 點擊、索引 | 每月 | 有曝光先至有點擊 |
| 速度 | PageSpeed Insights | 僅參考 | 改 theme 後 | 唔作 90 日成敗標準 |

請求索引：**只** 對戰略 URL 按，唔好對 2000 SKU 狂按。

---

## 3. On-page（品牌頁、品類頁、產品頁）

**成功定義：** 目標詞有曝光／點擊；人由搜尋落到正確頁；有詢盤。

### 3.1 用 GSC 對 **一個 cluster 一條正規頁**

例：Gessi。

1. 成效 → 頁面 → 篩 `https://colourliving.shop/collections/gessi`  
2. 再撳「查詢」：呢頁帶來邊啲詞。  
3. 成效 → 查詢 → 篩 `gessi`：邊啲詞有曝光、落地係咪真係 Gessi 頁（對照「頁面」）。

**Benchmark（改答案段前再抄一次）：** 該頁 28 日點擊、曝光、平均排名；查詢 `gessi hong kong` 的排名（冇就寫「無曝光」）。

**改完 4–8 週再比**（Luxury 詞搜尋量細，唔好一週就判死刑）。

品類頁同樣：頁面 = `/collections/bathroom-faucet`；查詢含 `faucet` `龍頭` `mixer`。

產品頁：GSC 頁面貼該 PDP URL。型號詞（`59003.706`）應落 PDP，唔應落 blog。

### 3.2 GA4：落地同行為

1. 到達網頁含 `/collections/gessi`：工作階段、參與時間。  
2. 若已設轉換：呢條 landing 的 `generate_lead_whatsapp` / 預約。  
3. 管道 = Organic Search 對比 All traffic（自然來的人會唔會問嘢）。

### 3.3 Shopify

該 collection／產品的瀏覽（若有報告）。訂單 tagged 來源不可靠時，以 GA4 事件為準。

### 3.4 免費抽查

無痕打開該頁：H1、答案段、內連。呢個係品質，唔係數字。每改一頁就 screenshot 答案段當「內容基準」。

**水龍頭今季最少 lock 呢幾條 query 做計分板（GSC 每週抄）：**

`gessi hong kong` | `gessi 香港` | `gessi 龍頭` | `bathroom faucet hong kong` | `浴室龍頭` | `dornbracht hong kong`

每格：曝光、點擊、平均排名、Top 落地 URL。

---

## 4. Blog / Pillar

**成功定義：** 文章被收錄；帶來問題型 query；幫 collection 而唔互搶。

| 你想證明 | 工具 | 點取數 | 幾時開始有意義 |
| --- | --- | --- | --- |
| 已索引 | GSC URL 檢查該 `/blogs/...` URL | 已編入 Y/N | 發布後 3–14 日 |
| 文章自己有冇曝光 | GSC 頁面 = 該篇 URL | 點擊／曝光／query | 4–8 週 |
| 有冇搶 collection | 同一 query（如 gessi hong kong）開「頁面」 | 點擊應 **主要** 仍在 `/collections/gessi` | 8 週 |
| 讀完去貨 | GA4：landing = blog，下一頁或連出 collection | 若有「路徑」探索；冇就睇該 session 有冇去 `/collections/gessi` | 有流量之後 |
| 轉換 | GA4 Organic + 該 landing | 預約／WhatsApp | 有事件之後 |

**解讀：** Blog 點擊 5、collection 點擊 40 而且 query 係 gessi hong kong → **正常**（cluster 設計如此）。  
Blog 同 collection 對同一主詞對半分、排名一齊跌 → 互搶，改 H1 或合併。

發布當日記：URL、H1、主詞。90 日後先同 Day 0 比「問題型 query 有冇新曝光」。

---

## 5. GEO（llms.txt、AI 答案）

**成功定義：** 指定 prompt 被點名、地址啱、有時有連結。

工具：ChatGPT（開搜尋）、Perplexity、Gemini、google.com.hk（睇 AI Overview）。**免費、人手。** GSC／GA **量唔到** ChatGPT。

表格每題一行（每月一次；龍頭季加 Day 0 / 30 / 60 / 90）：

`date | engine | prompt | Mentioned 0/1 | Cited URL | Facts OK 0/1 | Competitors | Notes`

計分（一個引擎一題）：Mentioned + Facts OK + Cited（有 `.shop` 或 `.com` 都算 cited）= 0–3。  
浴室 4 題 × 3 引擎 = 最高 36。**Day 0 分數寫低。** 90 日升 分先算 GEO 有移動。

另：瀏覽器開 https://colourliving.shop/llms.txt ——改完即日可 screenshot（原料），**唔等於** ChatGPT 已改口。

GBP 帖文／相片：Local 輔助，每月記「有冇更新」，唔當 SEO 點擊。

---

## 6. 生意（先設事件，否則永遠講故事）

GA4 建議事件（Shopify 用 Google & YouTube app 或自訂）：

- `generate_lead_whatsapp`（撳 WhatsApp）  
- `generate_lead_showroom`（預約提交）  
- `purchase`

**報告：** 獲客 → Organic Search → 轉換。  
Shopify 訂單數作對照，但 **有機流量嘅預約** 先係呢個 project 的北極星。

每週抄：Organic 工作階段、Organic 導致的 WhatsApp／預約、Organic 訂單（可 0）。

未設事件前：GSC 點擊只證明「被搵到」，你要同老細講明差一層。

---

## 節奏（同金字塔一致）

| 何時 | 量邊層 | 用時 |
| --- | --- | --- |
| **Day 0**（本週） | 第 0 節全做 | 2–3 小時 |
| **每週 30–45 分** | 技術索引 + GSC 品牌／Gessi 六條 query + GMC 拒登 + Organic 工作階段 | 週一 |
| **每月 90 分** | GEO 題庫 + 戰略頁 28 日對比 + 若有新 blog 就查該 URL | 月尾 |
| **日 90** | 對 Day 0：GSC 總點擊、六條 query、索引、GEO 分數、Organic 預約 | 半日 |

**唔好每週問「SEO 有冇效」。** 技術層一週可見；Gessi 詞 4–8 週；GEO 30–90 日；預約要事件 + 夠工作階段。

---

## 老細一頁（由邊層講）

- 地基／技術：301、索引、schema 測試圖、Merchant 拒登 ↓  
- On-page：Gessi 頁同 `gessi hong kong` 表（曝光／排名）  
- Blog：該篇已索引；主詞仍以 collection 為主  
- GEO：36 分制前後 screenshot  
- 生意：Organic 預約（有事件先）

缺少 Day 0 表 = 唔好宣稱成功。Sheet 欄位夠用：日期、層、指標、工具、數值、備註。
