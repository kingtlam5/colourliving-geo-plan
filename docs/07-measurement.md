# 07 — 衡量與治理

未登入你們帳號前，呢份係 **你要自己建立的儀表板規格**。工具已有：GSC、GA4、Merchant Center。缺的是定義同節奏。

**由地基做到 blog／GEO、逐層點撳工具：** [playbooks/measure-seo-geo.md](../playbooks/measure-seo-geo.md)。先做該檔第 0 節 Day 0。

---

## A. 只追 12 個數字

分四組。每週看操作型，每月看生意型。

### 1. 健康（每週）

| 指標 | 來源 | 健康樣子（launch 後 3–6 個月） |
| --- | --- | --- |
| 已編入索引的有效頁 | GSC 頁面索引 | 穩定上升，唔好爆大量「已發現 - 尚未編入索引」 |
| 404 / 伺服器錯誤 | GSC | `/zh`、sitemap 500、舊 handle 趨近 0 |
| Merchant 拒登產品 | GMC Diagnostics | 每週清，英雄品牌近 0 拒登 |

### 2. 可見（每週）

| 指標 | 來源 |
| --- | --- |
| 品牌詞：colourliving、colour living | GSC 查詢 |
| 品牌+產品：gessi hong kong、b&b italia hong kong | GSC |
| 中文品類：梳化、浴缸、龍頭 + 香港 | GSC，過濾國家 HK |
| 平均排名 / 點擊（分 `en` 與 `/zh` 路徑） | GSC 頁面 |

### 3. GEO（每月）

| 指標 | 來源 |
| --- | --- |
| Prompt mention rate | 人手跑 [geo-monthly-prompts.md](../playbooks/geo-monthly-prompts.md) |
| 事實正確率（地址電話） | 同上 |
| AI 來源是否 `.shop` | Perplexity 引用列表 |

### 4. 生意（每週）

GA4 必須先設轉換，否則 SEO 無法證明價值：

| 事件 | 建議名稱 |
| --- | --- |
| 點擊 WhatsApp | `generate_lead_whatsapp` |
| 提交預約陳列室 | `generate_lead_showroom` |
| 產品查詢表 | `generate_lead_pdp` |
| 購買 | `purchase` |
| 加購 | `add_to_cart`（輔助） |

再按 `sessionDefaultChannelGroup = Organic Search` 睇。

高端店：**預約數 > 訂單數** 仍然可以是 SEO 大勝。

---

## B. GSC 設定

1. Domain property：`colourliving.shop`（含 www 與非 www；統一 https 非 www 或 www，揀一個）
2. 若 `.com` 仍有流量，保留舊 property 觀察 301
3. 國際：篩選國家/地區 = Hong Kong；頁面篩選 `/zh` 或 `/zh-hk`
4. 提交 sitemap
5. 連結 Search Console 到 GA4
6. 核心查詢清單存成 Filter 或 Looker 報表（見 keyword-clusters 的 P0 詞）

Launch 兩個月：預期大量頁「已發現尚未索引」。優先用 URL Inspection 請求索引：**首頁、陳列室、10 個品牌頁、12 個品類、英雄產品**，唔好對全 catalog 狂按。

---

## C. GA4 設定

- 內部 IP 過濾
- 貨幣 HKD
- 增強型電子商務（Shopify 官方 pixel / Google & YouTube app）
- 標記 `page_location` 以便分語言
- 自訂管道或比較：Organic / Paid / Direct / Referral / WhatsApp in
- 若有 Shopify Inbox / WhatsApp 外連，用 outbound click 事件

---

## D. Merchant Center

每週一看：

- 產品遭拒原因（GTIN、價格、圖片、政策）
- Feed 最後成功時間
- 免費資訊主頁（Free listings）表現
- 若開 Performance Max，**分開睇**，唔好同 SEO 混為一談

SEO 計劃可以並行 Shopping 廣告，但本倉庫以自然為主。

---

## E. GEO 記錄表（Sheets 即可）

欄位：

`date | engine | prompt | mentioned Y/N | cited URL | facts correct Y/N | competitor mentioned | notes | action`

引擎最少：ChatGPT（有搜尋）、Perplexity、Gemini、Google（睇有冇 AI Overview）。

同一人、同一無個人化視窗（或無登入），減少個人化干擾。

---

## F. 治理：誰改 title、點樣上線

Shopify 最大風險係「人人改產品名」。定規則：

- 產品 Title 跟 SOP 公式，改動要有 SKU 負責人
- SEO title / description 用 Shopify Search & Discovery 或 theme metafield，唔好同顯示標題永久衝突時要有文件
- 中文翻譯 lock 詞表：梳化、浴缸、龍頭、面盆、陳列室、預約
- 每月抽 10 個 PDP 做品質審查（標題、schema、中英、價格）

---

## G. 基準線（本週做一次）

喺 GSC 匯出過去 28 日：

- 總點擊、總曝光
- Top 50 queries
- Top 50 pages
- 國家 = Hong Kong 的佔比

存成 `baselines/gsc-28d-YYYY-MM-DD.csv`（可放內部 Drive，唔一定放 git）。90 日後對比，先好講「SEO 有冇效」。
