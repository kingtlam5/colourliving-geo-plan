# 首頁加 H1 但畫面唔顯示

你而家 **已經有一個 H1**：header logo（`<h1 class="header__logo">`）。Hero「COLOURLIVING」只係 **H2**。  
所以唔可以只「再加一句隱藏 H1」——會變成兩個 H1。要先處理 logo 嗰個。

---

## 建議先考慮：唔使隱藏

客人 **已經見到** Hero 的「COLOURLIVING」同 *The House of Brands*。  
最乾淨做法：把呢句 **升級做 H1**（畫面完全唔變），logo 改用 `<div>`。Google 同客人睇同一句，無「隱藏關鍵字」風險。

Hyper：Homepage 那個 image-with-text overlay 區塊，睇下 Heading 有冇 **Heading size / HTML tag** 可以揀 `H1`。冇呢個掣，就要改 theme（下面 C）。

若你堅持 **畫面完全唔出嗰句較長的 SEO 句**（例如加 Wan Chai / Hong Kong），用 **做法 B**。一句要短、同舖頭事實一致，唔好塞品牌名單。

---

## 唔好用嘅隱藏法

| 做法 | 點解唔好 |
| --- | --- |
| `display: none` / `visibility: hidden` | Google 可能當呢句唔存在 |
| 字色同背景一樣、`font-size: 0`、`text-indent: -9999px` | 舊式隱藏文字，似 stuffing |
| 兩個 H1（logo + 隱藏句） | 結構亂，logo 嗰個仲係「第一個 H1」 |

正確隱藏 = **視覺隱藏、仍佔可讀位置**（screen reader 同 Google 都讀得到）：Shopify 多數 theme 已有 class `visually-hidden`。

---

## 做法 B：畫面睇唔到，原始碼有一個 H1

**先 Duplicate theme。** 只改副本。

### 1. 主頁拆走 logo 的 H1

Online Store → Themes → ⋯ → **Edit code** → `sections/header.liquid`  
搜：`header__logo` 或 `<h1`。

而家類似：

```liquid
<h1 class="header__logo ...">
  <a href="/">…logo…</a>
</h1>
```

改成：**只有首頁用 div，其他頁可繼續用 h1**（內頁 logo 當 H1 都普通）。

```liquid
{% if template.name == 'index' %}
  <div class="header__logo flex justify-center items-center z-1">
{% else %}
  <h1 class="header__logo flex justify-center items-center z-1">
{% endif %}
```

對應的 `</h1>` 都要改成：

```liquid
{% if template.name == 'index' %}
  </div>
{% else %}
  </h1>
{% endif %}
```

只改呢對標籤，**唔好**動 `{% schema %}` 設定 JSON。Save。

### 2. 主頁加一句隱藏 H1

Customize → Homepage → **Add section** → **Custom Liquid**（或 Custom HTML）→ 拖去 Hero **下面第一個**（唔好放 footer）。

貼：

```html
<h1 class="visually-hidden">COLOURLIVING — The House of Brands in Wan Chai, Hong Kong</h1>
```

Save → 無痕開主頁：

- 畫面應 **睇唔到** 呢句（logo 同 Hero 照舊）  
- 右鍵「查看網頁原始碼」搜 `<h1`：應 **只有呢一個** H1  
- 若字仍然出現：theme 冇 `visually-hidden`，去 Theme settings → **Custom CSS** 加：

```css
.visually-hidden {
  position: absolute !important;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

### 3. 句子點寫

用一句品牌定位即可，例如：

`COLOURLIVING — The House of Brands in Wan Chai, Hong Kong`

**唔好** 寫成長關鍵字袋（Gessi Dornbracht Fantini sofa faucet…）。隱藏 + 堆詞，Google 當作弊。真正想講灣仔／只送香港，應放 **客人見到** 的短定位段（見 [homepage-audit.md](homepage-audit.md)），唔單靠隱藏 H1。

---

## 核對

1. 主頁原始碼只有 **一個** `<h1>`  
2. 畫面無多出一行字  
3. Logo 連返 `/` 仍然正常  
4. 內頁（About、collection）header 未爛  

Rich Results／schema **唔靠** 呢個 H1。Local business 仍要改 Organization JSON-LD。
