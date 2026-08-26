# Wayback Machine：點睇舊 colourliving.com＋apex vs www

## 1. 直接開呢幾條（Internet Archive）

呢啲係公開檔案，唔使 login。載入可能慢。

**日曆（按年睇有幾密）：**

- 根網址（冇 www）：https://web.archive.org/web/*/colourliving.com
- www 首頁：https://web.archive.org/web/*/www.colourliving.com

**呢個域下面曾經抓過嘅所有路徑（你問「有幾多條 link」主要睇呢度）：**

- 冇 www：https://web.archive.org/web/*/colourliving.com/*
- 有 www：https://web.archive.org/web/*/www.colourliving.com/*

**下載清單（純文字，每行一條舊 URL）：**

- https://web.archive.org/cdx/search/cdx?url=colourliving.com/*&output=txt&fl=original,timestamp,statuscode&collapse=urlkey
- https://web.archive.org/cdx/search/cdx?url=www.colourliving.com/*&output=txt&fl=original,timestamp,statuscode&collapse=urlkey

2026-08-26 抽過：`colourliving.com/*` 用 `collapse=urlkey` 大約 **2000 條不重複 URL**。當中好大份係圖片、舊購物車、404、重複參數。**唔等於** Google 而家索引咗 2000 頁，亦唔使 2000 條都做 301。

---

## 2. 點用（5 分鐘版）

1. 先開 **日曆** 條：https://web.archive.org/web/*/colourliving.com  
   上面有年份 bar chart。有柱嘅年份 = 當年有人／機械存過快照。點年份 → 日曆上藍色圈 = 嗰日有存檔。
2. 想知「舊站有過咩頁」，開 **星號路徑** 條：https://web.archive.org/web/*/colourliving.com/*  
   會列出路徑。你只關心類似：
   - `/aboutus.htm`、`/about_colourliving.html`
   - `/advertisements_Gessi.html`、品牌名
   - `/collections/...`（2020 前後 Magento）
3. **忽略**：`/checkout`、`/admin`、`.gif` / `.jpg`、`form_key=`、亂碼。
4. 撳一條路徑 → 再揀一個 **較新、狀態 200** 的日期，就見到當時頁面。用來決定「呢條舊 URL 而家應對去 `.shop` 邊個 collection」。
5. 夠用就停。目標係抽 **幾十條高價值**（About、Gessi、Bath、Furniture），唔係還原成個站。

`www` 同冇 `www` 嘅清單會好大程度重複（同一頁兩種寫法）。睇完一個再掃另一個有冇獨有路徑即可。

---

## 3. `colourliving.com` 同 `www.colourliving.com` 係咪兩個 domain？

**唔係兩個註冊域名。** 你買嘅係一個域：`colourliving.com`。

| 寫法 | 技術上係咩 | Google 點睇 |
| --- | --- | --- |
| `colourliving.com` | **apex／裸域**（根主機名） | 一條獨立 URL |
| `www.colourliving.com` | 同一個域下面的 **`www` 子網域** | **另一條** URL，直到你轉址合併 |

所以：註冊商只得 **一個** domain；瀏覽器／Google 見到 **兩個** hostname。兩個都要去到同一個目的地，否則有人打有 www、有人打冇 www，行為可以唔同。

而家兩個都係 **302** 去 `https://colourliving.shop`（只去首頁）。DNS A 記錄指向 `15.197.225.128` / `3.33.251.168`，呢對 IP 係註冊商（常見 GoDaddy）**Domain Forwarding**，**仲未係** Shopify 官方 IP（`23.227.38.65`）。所以而家條 302 好大機會喺 GoDaddy Forwarding，唔係 Shopify「Redirect to primary」。

---

## 4. Shopify 要唔要兩個都加？

**兩個 hostname 都要轉去 `.shop`。** 操作上唔係「買兩個 domain」，而係連一次 `colourliving.com` 時，**apex 同 www 一齊接**。

Shopify：

1. **Settings → Domains → Connect existing domain**
2. 輸入 **`colourliving.com`**（通常唔使分開再買／再 connect 多一次 `www`；系統會要你加 `www` 的 DNS）
3. 註冊商 DNS 改成 Shopify 指定（同時關 GoDaddy Forwarding，否則 A 記錄會鎖住舊 IP）：
   - A `@` → `23.227.38.65`
   - CNAME `www` → `shops.myshopify.com`
4. **Primary domain 保持 `colourliving.shop`**
5. 列表裡 `colourliving.com` 同 `www.colourliving.com` 都設 **Redirect to primary domain**  
   Shopify 呢步用 **301**，而且多數 **保留路徑**（而家 Forwarding 做唔到）

清單裡應該見到 **三個** hostname 一齊：

- `colourliving.shop`（Primary，店）
- `colourliving.com`（redirect）
- `www.colourliving.com`（redirect）

只加咗 `www`、冇加裸域：客人打 `colourliving.com` 可能仍停喺舊 302／404。兩個都要。

**GSC：** 你加 Domain property `colourliving.com` 已經包咗 www 同非 www，**唔使**為 www 再開一個 property。

電郵 `@colourliving.com`：改 A / CNAME 時 **唔好刪 MX**。Shopify 連 domain 唔會取代你電郵，除非你自己改 MX。
