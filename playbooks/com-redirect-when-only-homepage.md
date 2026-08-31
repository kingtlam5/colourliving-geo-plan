# `.com` 301：只做首頁夠唔夠？搵到內頁又點？

## 短答

等幾日之後，GSC 同 `site:colourliving.com` **仍然只得 homepage**：

- **唔使**為 Wayback 那 2000 條舊路徑逐條做 URL Redirect。
- **仍然要把整個 `colourliving.com`（連 www）連入 Shopify，Redirect to primary `colourliving.shop`。**  
  呢步唔係「只轉首頁」——Shopify 會把呢個域名 **所有請求** 做 301。對 SEO 嚟講，你真正在意的係首頁；其餘內頁跟住轉走係免費附送，唔使逐條加規則。

若之後真係搵到其他仲有人用／Google 仲記得嘅內頁：  
**先**連 domain 做 301，**再**只為「路徑喺新店唔存在」的那幾條加 URL Redirect。你講嘅後台位置啱：而家 Shopify 多數係 **Content → Menus → URL redirects**。

---

## 兩層 redirect（唔好當成同一掣）

| 層 | 喺邊度設 | 做咩 | 你而家要唔要 |
| --- | --- | --- | --- |
| **A. 域名** | Settings → **Domains** → 連接 `colourliving.com` → Redirect to primary | `colourliving.com/任何路徑` → `colourliving.shop/同一路徑`（**301**） | **要。** 呢個先解決首頁 302 |
| **B. 路徑** | **Content → Menus → URL redirects** | 只改 **路徑**：`/aboutus.htm` → `/pages/about-us` | **得你搵到、而且連完之後喺 `.shop` 會 404 的頁先加** |

連完 A 之後，有人打 `colourliving.com/collections/gessi`：

1. 301 去 `colourliving.shop/collections/gessi`
2. 若新店 **有** 呢個 collection → 完成，**唔使**再加規則
3. 若新店 **冇**（舊 Magento 路徑例如 `/aboutus.htm`）→ `.shop` 上 404 → 先用層 B

層 B 的「Redirect from」只填路徑，例如 `/aboutus.htm`，**唔好**填 `https://colourliving.com/aboutus.htm`。因為客人到達時已經喺 `.shop` 上。

Homepage **唔使**喺 URL Redirects 加 `/` → `/`。層 A 已經轉晒根網址。

---

## 等幾日仍然只得 homepage，可唔可以「只做首頁」？

**SEO 優先級：可以當內頁規則係 0。** Google 唔索引嘅頁，唔會搶 `.shop` 排名。

但 Shopify **冇**「只 301 首頁、其他路徑繼續 404 喺 `.com`」呢個獨立掣（除非你繼續用 GoDaddy Forwarding 只轉根網址——而家就係咁，而且係 302、唔帶路徑）。

建議仍然做層 A（連入 Shopify），原因：

- 把 302 改成 **301**
- `www` 同裸域一齊處理
- 將來偶然有人撳舊 bookmark，至少會去到 `.shop` 同一路徑，有就開到、冇就 404（你可以遲啲先補層 B）

**唔建議**為咗「只轉首頁」而停留喺 GoDaddy 302。

內頁 URL Redirect：**唔做都得**，直到 GSC `.com` 或 `.shop` 出現「未找到」而且係你認得嘅舊品牌／About 路徑。

---

## 若搵到其他 page：步驟（你估嘅順序係啱）

**Step 1 — 域名 301（一次）**

1. 註冊商 **關掉** Domain Forwarding（否則 DNS 改唔到 Shopify）
2. Shopify → **Settings → Domains → Connect existing domain** → `colourliving.com`
3. DNS：A `@` = `23.227.38.65`；CNAME `www` = `shops.myshopify.com`（**唔好刪 MX**）
4. Primary 保持 **`colourliving.shop`**
5. `colourliving.com` 同 `www.colourliving.com` 都設 **Redirect to primary domain**
6. https://httpstatus.io/ 核：`https://colourliving.com/` 應 **301**（唔再 302）去 `.shop`

   若 httpstatus.io 顯示 **Error** 而瀏覽器已經跳去 `.shop`：多數係工具／SSL 檢查問題，唔係 Shopify 冇 301。改用無痕 + Network 睇第一跳，或見 [why-httpstatus-io-errors-on-com-301.md](why-httpstatus-io-errors-on-com-301.md)。

**Step 2 — 只為對唔上路徑加規則**

1. 打開嗰條舊 URL（或 `colourliving.com/舊路徑`）
2. 睇最終係咪 `.shop` 上 **404**
3. 係先至：**Content → Menus**（右上）**URL redirects** → **Create URL redirect**
   - Redirect from：`/aboutus.htm`（舊路徑）
   - Redirect to：`/pages/about-us` 或 `/collections/gessi`；去首頁就填 `/`
4. Save。舊后台若仍係 **Online Store → Navigation → View URL redirects** 都係同一個功能。

Admin 搜「redirect」搵唔到就搜「URL」。

**唔好**為 Wayback 全表匯入。只加：About、幾個品牌、Bath／Furniture 這類你確認有人連過、或 GSC 列出 404 的。

---

## 點先算「搵到其他 page」而值得加規則

值得：

- GSC `colourliving.com` 幾週後「未找到／404」裡出現具體路徑
- `site:colourliving.com` 多咗非首頁
- 品牌商／PDF／電郵仲連住一條具體舊 URL，你自己打開係 404

唔值得：

- Wayback 有過、而家 404、Google 同 GSC 都冇嘅路徑
- `/checkout`、圖檔、`admin`

驗證層 A 用首頁即可。驗證層 B：無痕開 `https://colourliving.com/那條舊路徑`，應 301 兩次或一次之後落到正確 `.shop` 頁，唔好停喺 404。
