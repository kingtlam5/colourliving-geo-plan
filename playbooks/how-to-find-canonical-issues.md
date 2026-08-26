# 點樣搵 Canonical 有問題的頁（同而家最大問題清單）

Canonical 問題 **唔係** 喺 Shopify Admin 有一個「Canonical 報告」。你要用「打開網頁 → 睇原始碼／GSC」去對。

產品 `/collections/.../products/...` 兩條 URL **唔算壞**——只要原始碼 canonical 指向 `/products/...`（Alys 已經係）。

## 總結：而家 Canonical 仲有幾大問題？

**除了 `colourliving.com` 之外，`.shop` 上面冇第二個「好大」的 canonical 災難。** 抽查過：

| 項目 | 狀態 |
| --- | --- |
| `www` → 非 www `.shop` | 已轉址，正常 |
| 產品 collection URL vs `/products/` | 已有正確 canonical，**唔使** 301 晒 |
| `/pages/contact-us` → About | 你有意 301，**留住** |
| `/collections/bath-1` → `bath` | 已 301，正常 |
| 中文 `/zh` | 未 publish，暫時 404，唔算 live canonical 問題 |
| **`colourliving.com` 302 + 內頁 404** | **唯一要優先修的大問題** |

Roca display **唔係 canonical 問題**，係「唔想 Google 索引、但鋪頭 iPad 要開到」。做法係 **繼續 published + noindex**，見 [roca-display-noindex.md](roca-display-noindex.md)。**唔好 unpublish。**

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
| P1 | `https://colourliving.shop/collections/roca-display-1` … `display-11` | 店內 iPad 要用，所以 **必須繼續發布**。對 Google 嚟講係薄／工具頁 | **唔好 Unpublish**（iPad 會 404）。加 `noindex`，見下面 |

除 `.com` 之外，店內產品／品牌／品類頁的 canonical **冇第二個同等大的 tag 錯誤**。Contact→About、bath-1→bath、collection 產品 URL 指向 `/products/` 都屬正確行為。

### Roca display：繼續 published + noindex（iPad 仍然打得開）

Unpublish = 網上 404 = 舖頭 iPad 條 link 死。  
Noindex = 客人／iPad 仍然開到頁，Google 結果盡量唔出。

**唔好** 用 robots.txt Disallow 呢批 URL（Google 可能反而睇唔到 noindex）。

Edit code → `layout/theme.liquid`，喺 `<head>` 內、`</head>` 前加：

```liquid
{% if collection and collection.handle contains 'roca-display' %}
  <meta name="robots" content="noindex, follow">
{% endif %}
```

Save → 無痕開 `/collections/roca-display-1` → View Source 搜 `noindex`。  
選單／SEO 頁唔好推呢 11 條；iPad 書籤照用原 link。

有其他 in-store only collection（handle 唔係 `roca-display`）就加多個 `or collection.handle == 'vea'` 這類條件。


### 睇落似問題、但其實已正確（唔使改 canonical tag）

| URL | 行為 | 點解得 |
| --- | --- | --- |
| `/pages/contact-us` | **301** → `/pages/about-us`，canonical = About | 你有意冇 Contact 頁 |
| `/collections/bath-1` | 去 `/collections/bath`，canonical = bath | 舊 handle 已合併 |
| `www.colourliving.shop` | 去非 www `.shop` | 主域統一 |
| `/collections/furniture/products/alys-ly153-bed` | 200 打開，canonical = `/products/alys-ly153-bed` | Shopify 預設，**唔使逐隻填** |
| `/collections/b-b-italia/products/alys-ly153-bed` | 同上 | 同上 |
| Sitemap 裡的 About、Customer Care、Room Inspiration、Gessi、Sofa… | canonical 指向自己 | 正常 |

產品雙 URL **唔係**「最大 canonical 問題」。最大的係 **`.com` 302 + 內頁 404**。Roca 用 **noindex、保持 published**（[roca-display-noindex.md](roca-display-noindex.md)），唔好當成要 301／unpublish。

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
