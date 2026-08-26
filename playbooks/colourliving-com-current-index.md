# colourliving.com 而家實際仲影響咩？（2026-08-26 覆核）

**短答：Google 而家幾乎冇索引任何 `.com` 內頁。** 你 GSC 空白、`site:colourliving.com` 只得首頁，同公開抓取一致。先前計劃把「舊站目錄互食」講得過重；而家真正仲喺搜尋出現嘅，主要係 **首頁 302**。

---

## 你見到嘅現象，係咪 GSC 遲咗？

**兩樣都有，但主因唔係「等數據」。**

| | `colourliving.shop`（你之前加） | `colourliving.com`（啱啱加） |
| --- | --- | --- |
| Google 認唔認呢個站 | 已爬咗約兩個月，索引裡已有大量 URL | 舊目錄多年前已消失；而家幾乎只得根網址轉址 |
| 加 GSC 之後 | 報告可以 **即日** 接到已有索引 | 新 property 通常 **1–3 日** 先有圖表；之後你都可能見到 **0 已編入索引** |
| Page indexing 合理結果 | 幾千個產品／分類 | 空白，或 1 條首頁列入「已排除：網頁有重新導向」 |

所以：

1. **新 property 的確要時間。** 圖表、搜尋字詞、覆蓋率唔係驗證完即刻同 `.shop` 一樣飽滿。等 48–72 小時係正常。
2. **等完都唔會突然出現幾百個舊產品頁。** `site:` 已經係 Google 公開索引的粗略鏡。只得 homepage，即係索引裡根本冇舊 catalog。GSC 唔會變魔術變出你 `site:` 搵唔到嘅頁。
3. `.shop` 即日有數據，係因為 Google **早就** 喺索引裡有呢個站；GSC 只係接駁你嘅帳號去睇。`.com` 冇同等存貨。

GSC 加完之後你應該睇：

- **網頁索引 → 網頁**：已編入索引 ≈ 0；「已排除」可能有 redirect／404
- **設定 → 使用者**：確認係 Domain property `colourliving.com`（包 www 同 http）
- 上面搜尋列貼 `https://colourliving.com/` → **URL 檢查**（即時，唔使等報告）：會話你 302、最終係 `.shop`

URL 檢查有結果、覆蓋率報告仍空：正常，報告滯後。

---

## 而家公開實際狀態（唔係估）

HTTP（2026-08-26）：

| URL | 狀態 |
| --- | --- |
| `https://colourliving.com/` | **302** → `https://colourliving.shop`（去**首頁**，唔帶路徑） |
| `https://www.colourliving.com/` | 同樣 **302** → `.shop` 首頁 |
| `/pages/about-us`、`/pages/contact-us`、`/collections/gessi`、`/products/alys-ly153-bed` | **404**，body 極短 |
| 舊檔 `about_colourliving.html`、`advertisements_Gessi.html`、`aboutus.htm` | **404** |
| `robots.txt` / `sitemap.xml` on `.com` | **404** |

Google 搜尋：品牌詞仍然可以同時出 `colourliving.com/` 同 `colourliving.shop/` 兩條「House of Brands」結果——因為 302 被當成 **臨時**搬家，Google 未把顯示網址完全合併去 `.shop`。

`site:colourliving.com` 只得 homepage：同上面一致。

---

## 我之前點「搵到」內頁？（同索引無關）

先前文件寫 `/pages/about-us` 404，**唔係**因為 Google 仲排緊呢啲頁，而係用三種方法：

1. **直接打 URL 問伺服器**（curl GET）。Shopify 風格路徑同舊 HTML 路徑而家都 404。呢個證明「有人若仲 bookmark 呢條會撞牆」，**唔證明**佢哋喺 Google 結果裡。
2. **Wayback Machine CDX**（internet archive 歷史快照）。例如 2003–2016 的 `aboutus.htm`、`advertisements_Gessi.html`；2020 前後 Magento 路徑如 `/collections/bath-and-wellness/...`。呢啲係 **十年前網站結構**，用來做將來 301 map 的原料，**唔係 2026 年 Google 索引清單**。
3. **普通網搜「COLOURLIVING」**。搜尋引擎結果有時仍顯示 `https://colourliving.com/` 做品牌結果（跟住 302 去店）。LinkedIn 公司檔「Homepage: colourliving.com」——呢類係 **citation／知識圖譜**，唔係一堆產品頁。

所以：冇一個隱藏工具顯示「Google 而家索引咗 500 個 `.com` 產品頁」。你自己用 GSC + `site:` 已經係最準。結論係 **舊目錄基本上已退出索引**。

---

## 咁 `.com` 仲影響 `.shop` 的 SEO／GEO 嗎？

**影響仲喺，但範圍細好多，而且集中喺首頁，唔係內頁互食。**

| 仲存在的影響 | 大唔大 | 點解 |
| --- | --- | --- |
| 首頁 **302**（臨時） | **中** | Google 可以繼續把品牌結果顯示成 `.com`，同 `.shop` **兩條首頁並列**。改 **301** 先會較穩把權重同顯示網址併去店 |
| 品牌 SERP 佔一格 `.com` | 中／細 | 客人撳入仍然去到店；問題係 302 合併慢、有時兩條結果搶 CTR |
| LinkedIn／舊稿寫官網 `.com` | 細，而且 **應留** | GEO／entity 用 `.com` 做公司官網；301 會帶人去店。見 [com-vs-shop-citations.md](com-vs-shop-citations.md) |
| 舊 Magento／HTML 深鏈 404 | **細**（而家） | 多數已唔喺索引。只有當 Google 再爬一條仲活嘅外鏈時先浪費一次。唔使為佢哋恐慌 |
| 舊產品頁同新產品頁互搶排名 | **而家基本上冇** | `site:` 同 GSC 都搵唔到呢批頁 |

GEO：AI 若 cite `colourliving.com`，跟 302／將來 301 都去到同一間店。呢個 **唔係傷害**。傷害只會係 302 令模型有時覺得「官網未穩定」。

---

## 你而家要做嘅（縮小版）

1. **把根網址 302 改 301**（`colourliving.com` 同 `www` → `colourliving.shop`）。呢步仍然值得做，但動機係「合併兩條品牌首頁」，唔係「拯救幾百個已索引內頁」。
2. 可選：Shopify 若支援 **保留路徑** 更好（`.com/products/x` → `.shop/products/x`）；而家內頁 404，只係防舊 bookmark／殘餘外鏈。
3. GSC `.com` property **留住** 觀察 1–2 週。預期：已索引 ≈ 0，首頁變「有重新導向」。唔好等佢變出舊 catalog。
4. **唔使** 為「搵晒所有舊頁」先做 301。Wayback 清單可以遲啲先做成 map。

**一句：** `.com` 而家唔係一個仲活喺 Google 裡的舊網店；佢係一條仲被搜尋引擎記住的品牌首頁 + 一個 302。你嘅 GSC 空白，大部分情況下係事實，唔係故障。
