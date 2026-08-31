# `colourliving.com` 已經係 301：httpstatus.io 點解顯示 Error

**Redirect 本身冇壞。** 2026-08-31 09:31 UTC 公開 GET：

| 你貼嘅網址 | 真正狀態 | Location |
| --- | --- | --- |
| `https://colourliving.com/` | **301** | `https://colourliving.shop/` |
| `https://www.colourliving.com/` | **301** | `https://colourliving.shop/` |
| `http://colourliving.com/` | **301** | 先去 `https://colourliving.com/`（Cloudflare HTTPS），下一跳先至 `.shop` |
| `https://colourliving.com/pages/about-us` | **301** | `https://colourliving.shop/pages/about-us`（路徑保留） |

Header 有 `x-redirect-reason: primary_domain_redirection` → 呢個係 Shopify **Domains → Redirect to primary**，唔係 Content → URL redirects 嗰層。DNS A 已係 Shopify `23.227.38.65`。TLS 證書 `CN=colourliving.com`（Let’s Encrypt，2026-08-31 簽、11-29 到期）。

Google／瀏覽器跟 301。**唔使因為 httpstatus.io 顯示 Error 再改 Shopify。**

---

## 點解個工具會 Error

httpstatus.io 唔係 Google。常見係工具自己失敗，狀態碼欄變紅／Error：

1. **新連入 Shopify 的 SSL 未 ready。** 證書今日先簽。連 domain 之後幾分鐘到幾小時，檢查器會報 SSL error，唔報 301。而家證書已有效；工具可能仲 cache 舊失敗。
2. **佢哋伺服器 IP 被 Cloudflare 擋。** 你瀏覽器開到，檢查器開唔到 → Error。
3. **Shopify 嘅 301 係空 body + 好長 `Set-Cookie`。** 有啲 checker 等 body／preview iframe（`.shop` 有 `X-Frame-Options: DENY`）就當 Error。
4. **貼咗 `colourliving.com` 冇 `https://`。** 工具先打 HTTP，兩跳 301。有時第一跳顯示得唔清，當失敗。

呢個 **唔等如** 客人同 Google 見唔到 301。

---

## 點核對（唔使 httpstatus.io）

**Chrome（最準）：**

1. 無痕開  
2. F12 → Network → 勾 **Preserve log**  
3. 貼 `https://colourliving.com/`  
4. 第一條 document：Status **301**，Response Headers `location: https://colourliving.shop/`  
5. 下一條 `.shop`：**200**

網址列最後變成 `.shop` 就啱。

或終端：

```bash
curl -sI https://colourliving.com/
```

應見到 `HTTP/2 301` 同 `location: https://colourliving.shop/`。

httpstatus.io 若再用：貼 **完整** `https://colourliving.com/`（連 `https://` 同結尾 `/`），清工具 cache／換 redirect-checker 類服務。仍然 Error 就當工具問題。

---

## 唔好為咗個 Error 去做嘅嘢

| 唔好 | 點解 |
| --- | --- |
| 喺 URL redirects 加 `/` → `https://colourliving.shop/` | 域名層已經 301；加規則有機會亂 |
| 改 primary 做 `.com` | 購物站應係 `.shop` |
| 再開 GoDaddy Domain Forwarding | 會同 Shopify 打架，以前就係 302 |
| 因為工具 Error 拆咗再連一次 domain | SSL 會再 pending 一陣 |

Settings → Domains：`colourliving.com` / `www` = **Redirect to primary**，primary 保持 `colourliving.shop`。咁就夠。
