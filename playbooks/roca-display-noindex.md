# Roca 陳列 collection：要 published，用 noindex

鋪頭 iPad 要撳得開 `https://colourliving.shop/collections/roca-display-1` 呢類連結。  
**可以 noindex。唔可以 unpublish。**

## 點解

| 做法 | iPad 條 link | Google |
| --- | --- | --- |
| Unpublish / 草稿 | **404**，鋪頭撳唔入 | 亦唔索引 |
| `robots.txt` Disallow | 仍然開到（視乎瀏覽器） | Google **可能仍然索引**（見到 link 但讀唔到 noindex） |
| **保持 Published + `noindex, follow`** | **開到** | 唔放搜尋結果 |

所以：**保持 published，加 noindex。** 唔好 Disallow 呢啲 URL。

## 喺 theme 加（Duplicate theme 先）

Edit code → `layout/theme.liquid` → 搵 `<head>` 入面、最好靠近其他 `<meta>` 的位置，貼：

```liquid
{%- if collection and collection.handle contains 'roca-display' -%}
  <meta name="robots" content="noindex, follow">
{%- endif -%}
```

呢段會覆蓋 `roca-display-1` 到 `roca-display-11`（handle 含 `roca-display` 就中）。  
Save → Preview → 開一條 Roca 頁 → View Source 搜 `noindex`，應見到上面嗰行。  
再抽查一條正常 collection（例如 `/collections/gessi`）**唔好**有呢行。

## 之後喺 Admin（可選）

- Collection 設 **唔放入主選單、唔放入 sitemap**（Shopify collection 有「在搜尋結果中隱藏」類選項時可勾；仍要 **published**）
- 唔好喺 SEO 描述寫「Roca display 1」當公開品類

Google 清走舊快取可能要幾日到幾週。iPad **即日**仍然開到。
