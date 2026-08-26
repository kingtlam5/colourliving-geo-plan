# 點樣搵 Canonical 有問題的頁（同而家最大問題清單）

Canonical 問題 **唔係** 喺 Shopify Admin 有一個「Canonical 報告」。你要用「打開網頁 → 睇原始碼／GSC」去對。

產品 `/collections/.../products/...` 兩條 URL **唔算壞**——只要原始碼 canonical 指向 `/products/...`（Alys 已經係）。

---

## 你自己點搵（由易到完整）

### 方法 1 — 單頁 30 秒（任何你懷疑的 URL）

1. 無痕打開該頁  
2. 右鍵 → **查看網頁原始碼**（View Page Source）  
3. 搜 `rel="canonical"`  
4. 對照：

| 見到 | 意思 |
| --- | --- |
| 只有一條，href = 你想 Google 算的正規網址 | 正常 |
| 兩條 `rel="canonical"` | 壞（theme + app 重複） |
| 冇 canonical | 壞 |
| href 指向另一頁，而你 **唔想** 合併 | 壞 |
| href 指向另一頁，而你 **有意** 合併（Contact→About） | 正常 |
| 網址列係 `/collections/furniture/products/xxx`，canonical 係 `/products/xxx` | **正常** |

### 方法 2 — Google Search Console（全站）

1. GSC → 你的 `colourliving.shop` property  
2. **網頁索引 → 網頁**  
   留意：「重複網頁，Google 已選擇與使用者不同的規範網址」「已排除：網頁有重新導向」  
3. **成效 → 頁面** 匯出：同一產品若同時出現  
   `/products/alys-ly153-bed` 同 `/collections/furniture/products/alys-ly153-bed`  
   只要後者點擊很少、前者係主，就係 canonical 生效  
4. 上面搜尋列貼一條 URL → **URL 檢查** → 展開「網頁是否可編入索引」  
   睇「使用者提供的規範網址」vs「Google 選用的規範網址」——兩條應一樣

GSC 數據要有爬取先準；launch 兩個月可能仲唔齊。

### 方法 3 — 免費狀態碼工具（域名／轉址）

https://httpstatus.io/ 貼：

- `https://colourliving.com/`  
- `https://colourliving.shop/pages/contact-us`  
- `https://colourliving.shop/collections/bath-1`

睇 301／302／404，同最終 Location。

**唔使** 一開始買 Screaming Frog。有 95 個 collection 之後先考慮。

---

## 而家我實際搵到的（2026-08-26）

### 要處理（真問題）

| 優先 | URL | 發生咩事 | 你要做 |
| --- | --- | --- | --- |
| P0 | `https://colourliving.com/` | **302** 去 `.shop` 首頁 | 改 **301**；見域名 FAQ |
| P0 | `https://colourliving.com/pages/about-us` 等內頁 | **404**，冇轉去 `.shop` | 301 去對應 `.shop` 頁或首頁 |
| P1 | `https://colourliving.shop/collections/roca-display-1` … `display-11` | 11 個陳列用 collection，各自 canonical 自己，好易變成薄／重複頁 | 若只係店內陳列：Shopify collection **不發布到線上商店**，或加 hidden + noindex；選單唔好連出去 |
| P2 | `/search?q=...`、`/cart` | 有自我 canonical，搜尋／購物車通常唔應上 Google | 多數 theme 已 noindex cart；GSC 若出現 search 再處理。唔好當產品頁咁優化 |

### 睇落似問題、但其實已正確（唔使改 canonical tag）

| URL | 行為 | 點解得 |
| --- | --- | --- |
| `/pages/contact-us` | **301** → `/pages/about-us`，canonical = About | 你有意冇 Contact 頁 |
| `/collections/bath-1` | 去 `/collections/bath`，canonical = bath | 舊 handle 已合併 |
| `www.colourliving.shop` | 去非 www `.shop` | 主域統一 |
| `/collections/furniture/products/alys-ly153-bed` | 200 打開，canonical = `/products/alys-ly153-bed` | Shopify 預設，**唔使逐隻填** |
| `/collections/b-b-italia/products/alys-ly153-bed` | 同上 | 同上 |
| Sitemap 裡的 About、Customer Care、Room Inspiration、Gessi、Sofa… | canonical 指向自己 | 正常 |

產品雙 URL **唔係**「最大 canonical 問題」。最大的係 **`.com` 302 + 內頁 404**，同（若公開）**roca-display-1～11** 呢類不應被索引的 collection。

### 選單／內部連結建議（減少 Google 發現第二條產品 URL）

分類頁產品卡用 `product.url`，唔用 `within: collection`。見 [11-canonical-howto.md](../docs/11-canonical-howto.md)。

---

## 定期抽查清單（每季 15 分鐘）

打開 View Source 核對 canonical：

1. 首頁  
2. About  
3. 一個品牌 collection（Gessi）  
4. 一個品類（sofa / bathroom-faucet）  
5. 一個產品 `/products/...`  
6. 同一個產品 `/collections/sofa/products/...`（應指返 `/products/`）  
7. httpstatus：`.com` 根網址應係 301  

唔使掃晒 2000 個 SKU。
