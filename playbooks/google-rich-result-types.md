# 想 Rich Results Test 出現類型：邊種做得到

畫面有 FAQ、麵包屑、地址 **唔等於** Google 有對應「結果類型」。Rich Results Test 只認 **JSON-LD 裡指定的 @type**，而且該類型仲要係 Google **而家仍支援** 的搜尋外觀。

COLOURLIVING 而家實際（2026-08-26）：

| 你見到（畫面） | JSON-LD 有冇 | Rich Results Test |
| --- | --- | --- |
| 首頁 FAQ 手風琴 | **冇** `FAQPage` | 唔出 FAQ。而且 Google **2026-05-07 起已取消 FAQ 豐富結果**，加咗都唔會喺搜尋展開 |
| Collection／產品麵包屑（Home → Gessi） | **冇** `BreadcrumbList`，只有 HTML | 唔出 Breadcrumb |
| Footer／About 地址 | 只有瘦 `Organization`，**冇** 地址欄 | 唔出 Local business |
| 產品價錢 | 產品頁 **已有** `Product` + `Offer` | 測 **產品 URL** 先會出 Product；測首頁唔會 |

首頁測出「No items detected」= 呢頁冇合格類型，唔係 Google 睇唔到整站。

---

## 1. Local business（你最應該做、同 header schema 同一件事）

Google 要的係 `LocalBusiness` 或其子類，**而且要有 `address`**。`FurnitureStore` 就係子類。

而家只有 `Organization` + logo + 社交 → **唔合格**做 Local business 結果類型。

做法：用已寫好嗰段取代 `header.liquid` 的 Organization script（`@type": ["Organization", "FurnitureStore"]` + 洛克道 + 電話 + 營業時間）。  
Publish 後再測 `https://colourliving.shop/`，先有機會出現 **Local business**。

驗證：https://search.google.com/test/rich-results  

地圖知識卡仲要 GBP 地址一致；schema 只係網頁呢邊。

---

## 2. Product（已經有，你測錯頁）

Rich Results Test 貼首頁 → 唔會出 Product。  
貼例如：`https://colourliving.shop/products/alys-ly153-bed` → 應見到 **Product**（價錢 HKD）。

**唔好**再加第二份 Product JSON-LD。

---

## 3. Breadcrumb（畫面有、機械冇）

Gessi 頁 HTML 已有：Home → Collection → Gessi。產品頁：Home → B&B Italia → Alys LY153 Bed。  
Google 要另加 `BreadcrumbList` JSON-LD，路徑同畫面一致。

Duplicate theme。Edit code 打開 breadcrumb 嗰個 section（Customize 見到 Breadcrumbs 區塊；code 裡檔名常係 `sections/breadcrumbs.liquid` 或類似）。喺 `</nav>` **後面**、`</div>` 前貼：

```liquid
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": {{ shop.url | json }}
    }
    {%- if template.name == 'collection' and collection -%}
    ,{
      "@type": "ListItem",
      "position": 2,
      "name": {{ collection.title | json }},
      "item": {{ shop.url | append: collection.url | json }}
    }
    {%- endif -%}
    {%- if template.name == 'product' and product -%}
      {%- if collection -%}
    ,{
      "@type": "ListItem",
      "position": 2,
      "name": {{ collection.title | json }},
      "item": {{ shop.url | append: collection.url | json }}
    }
    ,{
      "@type": "ListItem",
      "position": 3,
      "name": {{ product.title | json }},
      "item": {{ shop.url | append: product.url | json }}
    }
      {%- else -%}
    ,{
      "@type": "ListItem",
      "position": 2,
      "name": {{ product.title | json }},
      "item": {{ shop.url | append: product.url | json }}
    }
      {%- endif -%}
    {%- endif -%}
  ]
}
</script>
```

若 Hyper 該 section 已有「Enable schema」類勾選，打開即可，唔使重複貼。

測：`https://colourliving.shop/collections/gessi` 同產品頁。Breadcrumb 豐富結果主要喺 **電腦版** 搜尋出現，手機常唔出。

首頁通常唔使 breadcrumb schema。

---

## 4. FAQ：唔好為 Rich Results Test 去做

Google 已於 **2026 年 5 月 7 日** 停止喺搜尋顯示 FAQ 展開結果（政府／醫療都一併取消）。Rich Results Test 唔出 FAQ，**唔代表你網站 FAQ 區塊壞**；代表呢個「結果類型」已經冇咗。

首頁那堆訂單／送貨 FAQ 係全站共用 boilerplate，就算標 `FAQPage` 以前都容易被當垃圾，而家更加 **零搜尋外觀回報**。

**留住畫面 FAQ**（人讀、ChatGPT 仍可抄）。**唔好**為咗個測試工具加全站 FAQPage。

若之後有「點樣揀 Gessi 龍頭」這類 **該頁獨有** 問答，內容本身對 GEO 有用；都唔好預期 Google 藍字下面會展開。

---

## 5. 測邊條 URL（對老細用）

| 想見到 | 貼去 Rich Results Test |
| --- | --- |
| Local business | 首頁（**改完 FurnitureStore 之後**） |
| Product | 任何產品 permalink |
| Breadcrumb | `/collections/gessi` 或產品頁（加完 BreadcrumbList 之後） |
| FAQ | **而家唔會出**，唔使測 |

schema.org validator（https://validator.schema.org/）仍然會顯示 Organization／WebSite；用嚟證明名片存在。Rich Results Test 用嚟證明「有機會變成搜尋外觀」的那幾種。

## 優先序

1. Header 換成 FurnitureStore + 地址（Local business）  
2. 用產品 URL 測 Product（已有就 screenshot 俾老細）  
3. 麵包屑 JSON-LD（可選，desktop 路徑）  
4. 唔做 FAQ schema 去追測試工具
