# 首頁加 H1 但畫面唔顯示

你而家 **已經有一個 H1**：header logo（`<h1 class="header__logo">`）。Hero「COLOURLIVING」只係 **H2**。  
所以 **喺主頁** 唔可以只「再加一句隱藏 H1」——會變成兩個 H1。要先處理 logo 嗰個。

Hyper **已經**寫死：

| 頁 | Logo 標籤 | 點解 |
| --- | --- | --- |
| 主頁 `/`（`request.page_type == 'index'`） | **`<h1 class="header__logo">`** | Theme 當首頁冇其他 H1，用 logo 頂 |
| 其他（`/pages/demo`、About、collection、PDP） | **`<div class="header__logo">`** | 預留 H1 俾頁面自己的標題 |

所以喺 **demo page 試 Custom Liquid H1，唔使改 header.liquid**——logo 本來就唔係 H1。  
主頁若加同一句隱藏 H1，**仍然要**先拆 logo 嗰個 H1，否則兩個 H1。

2026-08-28 覆核：homepage logo = `h1`；`/pages/demo` 同 `/pages/about-us` logo = `div`；`/collections/gessi` logo = `div`（collection 自己有 H1）。

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

### 1. 只喺 **主頁** 先要拆 logo 的 H1

Demo／About／collection **唔使做呢步**（theme 已用 div）。

**停：** Hyper 的 `header.liquid` **已經有** `request.page_type == 'index'` 包住 logo 的 `h1`／`div`。  
唔好再喺外面加多一層 `{% if template.name == 'index' %}`——兩個 if 套埋，開關標籤會錯配，header 會炒。

你 upload 嗰份（約第 81–140 行）係 **原裝正確版**。只要把「主頁用 h1」改成「所有頁都用 div」，改 **兩舊、共約 10 行**，其他 3000 行（包括最底 `{% schema %}`）**一個字都唔好郁**。

**第 81–85 行，整舊換成：**

```liquid
      <div class="header__logo flex justify-center items-center z-1">
```

即係刪走呢 5 行：

```liquid
    {%- if request.page_type == 'index' -%}
      <h1 class="header__logo flex justify-center items-center z-1">
    {%- else -%}
      <div class="header__logo flex justify-center items-center z-1">
    {%- endif -%}
```

**第 136–140 行，整舊換成：**

```liquid
    </div>
```

即係刪走：

```liquid
    {%- if request.page_type == 'index' -%}
      </h1>
    {%- else -%}
      </div>
    {%- endif -%}
```

改完 logo 區塊應變成：

```liquid
      <div class="header__logo flex justify-center items-center z-1">
    {%- if section.settings.header_layout == 'logo-left' or section.settings.header_layout == 'logo-left-search-center' and section.settings.enable_collapse_on_scroll -%}
      <button
        class="menu-drawer-button toggle-navigation-button btn btn--inherit flex-col items-center justify-center hidden lg:flex shrink-0"
        aria-label="{{ 'accessibility.menu_drawer' | t }}"
      >
        <span class="hamburger-line"></span>
      </button>
    {%- endif -%}
    <a href="{{ routes.root_url }}" ...>
      ...logo img...
    </a>
    </div>
```

Save 之後：header 外觀應同未改之前一樣。主頁原始碼 logo 變 `<div class="header__logo">`，Custom Liquid 嗰句先至係唯一 H1。

若而家 header 已炒：把 upload 嗰份原裝 `header.liquid` 貼返去還原，再只做上面兩舊替換。**唔好**改 `{% schema %}`。

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
