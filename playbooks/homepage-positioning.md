# 首頁定位段：要可見；schema 類型唔止 FurnitureStore

答兩條：（1）定位段可唔可以好似 H1 咁隱藏；（2）舖頭唔止傢俬，FurnitureStore 夠唔夠。

---

## 1. 定位段唔好 `visually-hidden`

| | 隱藏 H1（你而家做緊） | 隱藏定位段（唔好） |
| --- | --- | --- |
| 係咩 | 一個**標題** | 一段 **40–80 字事實** |
| SEO | Google 當頁面 H1，短句、同畫面品牌一致 | 長文隱藏，似同畫面唔同的「第二套內容」 |
| GEO | 幫好少；ChatGPT／Perplexity **好少抄 hidden** | **幾乎失效**。AI 抄首屏睇到的句子、About、footer，唔抄 `visually-hidden` 段落 |

隱藏 H1 得，因為客人已經見到「COLOURLIVING / The House of Brands」，機械只係有一個正確標題。  
定位段要 **可見**。地點可以只出現喺 footer（可見）+ 隱藏 H1 + schema，唔強制寫入 Hero。

JSON-LD 的 `description` 欄係另一條通道：畫面唔出一段字，但 Google 讀 schema。**唔代替**可見定位段。兩樣一齊：畫面一段短句 + schema 一句 description。

### 畫面點放（唔破壞旗艦店 look）

Customize → Homepage → Hero 已經有 H2「COLOURLIVING」同 *The House of Brands*。  
**唔好再加 Custom Liquid 隱藏段。** 把副標題／其下 Rich text **換成可見短句**（字可以細、同而家 Beige 風格）。

**建議可見英文**可以係生活雜誌風，唔一定要「Hong Kong’s House of Brands…」咁直。事實清單同雜誌句見下面「語氣」。

中文等 ZH publish 再開一段，唔好而家用隱藏中文。NAP 鎖定仍係 [nap-source-of-truth.md](nap-source-of-truth.md)。

### 定位段：必定要有／唔使有（鎖定）

整段（tagline + 後面一句、兩句都計）**可見**。句子點寫由你定；我唔再改第二句。

**必定要有：**

定位段本身只強制一樣：

1. **舖頭賣咩，要睇得出唔淨係梳化：** 品類詞至少一個（`furniture` / `lighting`／`light` / `bath`／`bathroom`），**或者** 至少兩個唔同場品牌（B&B Italia、Flos、Gessi／Dornbracht）。

**地點唔使再寫入定位段**，若全頁其他**可見**位置已有（footer「333 Lockhart Road, Wan Chai」算）。隱藏 H1 的 Wan Chai **唔算**定位段嘅可見地點——AI 少抄 hidden——但 footer + schema 已經夠。Hero 可以改用其他可見事實（例如 2,000 sqm）。

**唔使寫入定位段：**

| 元素 | 已經喺邊 |
| --- | --- |
| COLOURLIVING | Logo、H1、title |
| Wan Chai / Hong Kong | 隱藏 H1；footer；schema |
| 333 Lockhart Road | Footer、schema、About |
| 電話、營業時間 | Footer、schema |
| Delivery / 只送香港 | Customer Care、FAQ |

**第一句**可以全係氛圍。

**採用稿：**

> The definitive address for refined European living.  
> Immerse yourself in exceptional craftsmanship at our 2000 sqm flagship—featuring curated masterworks from B&B Italia, Flos, Gessi, and Dornbracht.

過關：品牌覆蓋三場；面積係 Hero 獨有可見事實；Wan Chai 留 H1 + footer。

---

## 2. Schema：FurnitureStore 要留，但唔夠代表全舖

`FurnitureStore` 係 Google 認的 Local business **子類**，對傢俬／陳列室仍然啱，**唔使刪**。  
Schema.org 無「浴室店」類型。較近、又包龍頭／浴缸／燈／生活用品的係 **`HomeGoodsStore`**（家居用品店）。

一份 JSON-LD 可以有**多個類型**（而家已經係陣列）：

```json
"@type": ["Organization", "FurnitureStore", "HomeGoodsStore"]
```

再加一句 `description`（同可見定位段事實一致，唔好變成品牌百科）：

```json
"description": "COLOURLIVING is Hong Kong’s House of Brands for European furniture, lighting and bathroom, including faucets, baths and sanitary ware. Flagship at 333 Lockhart Road, Wan Chai. Delivery within Hong Kong."
```

可選：`knowsAbout` 品類 + 幾個品牌；薄 `hasOfferCatalog` 連三個 collection。點解第一稿冇、而家點加：[schema-jsonld-shopify.md](schema-jsonld-shopify.md)。**唔好**把全品牌／全 SKU 塞進 Organization。

**唔好用：** `DepartmentStore`、`HardwareStore`、`WholesaleStore`（類型錯）。**唔好**為浴室再開第二個 Organization。

改法：`header.liquid` 而家嗰份 FurnitureStore script，只改 `@type` 一行 + 喺 `name` 下面加 `description`。產品 Product schema **唔好動**。改完 View Source 應仍得 **一份** Organization。

完整稿：[schema-jsonld-shopify.md](schema-jsonld-shopify.md)。測：Rich Results Test 貼主頁。
