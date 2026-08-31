# Shopify hreflang：英文冇 `/en/`、中文係 `zh` 應該點處理

## 而家公開網站實際係點（2026-08-26）

| 訊號 | colourliving.shop |
| --- | --- |
| 英文 URL | `https://colourliving.shop/...` **冇** `/en/` 前綴 |
| `<html lang>` | `lang="en"` |
| HTML 裡 `hreflang` | **0 條** |
| `/zh`、`/zh-hk` | **404**（中文未 publish，正常） |

你喺 Admin 見到「中文 = zh、英文冇寫 en」，多數係 **Languages 列表／URL 前綴**，唔係 Google 而家讀緊的 hreflang。兩樣要分開睇。

---

## 英文「冇寫 en」係正常，唔好加 `/en/`

Shopify 規定：**主要語言用根網址，不加語言前綴。**

- 英文（Primary）→ `colourliving.shop/products/alys-ly153-bed`
- 中文（第二語言）→ `colourliving.shop/zh/products/alys-ly153-bed`

Google 靠呢啲知英文係英文：

1. `<html lang="en">`（你而家已有）
2. 頁面內容係英文
3. 中文 publish 之後，自動 hreflang 會有一條指向 **冇前綴** 的英文 URL，值可能係 `en` 或 `en-HK`

**唔好** 再做一個 `/en/` 市場把英文再複製一次。會變成兩個英文首頁互搶。

「寫到明係 en」嘅正確位置係 **`lang` 同將來的 hreflang**，唔係 URL。

---

## 中文叫 `zh` 而唔係 `zh-HK` 點處理

`zh` = 語言「中文」，冇地區。  
`zh-HK` = 香港繁體，對 Google／用戶更準。

Shopify 若只開一種中文，URL 前綴好常見係 **`/zh/`**，hreflang 亦可能只出 `zh`。  
呢個 **唔會令香港 SEO 失敗**，因為你只賣香港、Market 係 HK、內容係繁體、GBP 喺灣仔。

優先順序：

1. **Market = Hong Kong**（地區）
2. 語言用 **繁體／香港**，唔好用簡體或台灣（用字）
3. 譯文品質
4. 先至輪到 hreflang 係 `zh` 定 `zh-HK`

---

## 中文未 publish：而家唔好手寫 hreflang

只有一種已發布語言時，**冇 hreflang 係啱的**。  
而家若手寫 `hreflang="zh"` 指去 `/zh/...`，Google 會跟去 **404**。

等中文 Publish 之後，Shopify 經 `content_for_header` 自動加 tag。`theme.liquid` 必須保留：

```liquid
{{ content_for_header }}
```

刪咗就永遠冇系統 hreflang。

---

## Publish 前要設嘅（Admin）

**1. Settings → Markets**

- 主要市場：**Hong Kong**
- 網店 URL：主域 `colourliving.shop`（唔好用另一個網域做中文）
- 語言：English 為預設；中文作 extra language（publish 先開）

市場國家會影響 tag 會唔會變成 `en-HK` / `zh-HK`。官方說明：針對單一國家的 market 較常出 `en-us` 這類 **語言-地區**；闊市場可能得 `en`。

**2. Settings → Languages**

- Primary：English（URL 前綴空白 = 根網址）
- 第二語言：清單若有 **Chinese (Hong Kong)／中文（香港）** 或 locale `zh-HK` → **揀呢個**
- 若只有 **Chinese (Traditional)**：用它，接受前綴 `/zh/` 或 `/zh-hant/`
- **唔好** 開 Chinese (Simplified)，除非真係要做內地
- 保持 Unpublished 直至譯完

**3. 唔好開「英文第二個 locale」** 例如再加 English (Hong Kong) 做 `/en-hk/`。根網址英文已經服務香港。

---

## Publish 之後點核對

無痕開同一個產品的 **英文頁同中文頁**，View Source，搜 `hreflang`。

理想：

```html
<link rel="alternate" hreflang="en-HK" href="https://colourliving.shop/products/alys-ly153-bed">
<link rel="alternate" hreflang="zh-HK" href="https://colourliving.shop/zh/products/alys-ly153-bed">
<link rel="alternate" hreflang="x-default" href="https://colourliving.shop/products/alys-ly153-bed">
```

可接受（香港單一市場仍然 OK）：

```html
<link rel="alternate" hreflang="en" href="https://colourliving.shop/products/alys-ly153-bed">
<link rel="alternate" hreflang="zh" href="https://colourliving.shop/zh/products/alys-ly153-bed">
```

每種語言要 **互相指對方**（英文頁都列出中文 alternate）。Canonical：英文指英文自己，中文指中文自己。

---

## 想「英文寫到明 en-HK」：改 `html lang`（可選、低風險）

唔改 URL。Edit code → `layout/theme.liquid` 搵：

```liquid
<html ... lang="en">
```

或 `lang="{{ request.locale.iso_code }}"`

可改成（中文 publish 後 `zh` 都會變成 zh-HK）：

```liquid
<html
  class="no-js"
  lang="{% if request.locale.iso_code == 'zh' or request.locale.iso_code contains 'zh' %}zh-HK{% else %}en-HK{% endif %}"
>
```

Save 後英文頁 View Source 應係 `lang="en-HK"`。

**唔好** 再手寫一套完整 hreflang，會同 `content_for_header` 重複。只有系統完全冇 tag、你又願意長期維護，先考慮自己寫。

---

## 一句

英文冇 `/en/` = 主要語言設計，用 `lang="en"`／將來 `hreflang="en"` 已經標明。  
中文 `zh` = Shopify 前綴限制；Market 設香港 + 繁體內容先緊要。  
未 publish 中文就 **唔好** 造 hreflang。Publish 後先 View Source 核對，唔好為咗 `zh-HK` 四個字去開第二個英文 URL。
