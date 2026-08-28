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
定位段的目的係俾 **人同 AI 引用**（灣仔、傢俬＋燈＋浴室、只送香港、預約）。藏起就做唔到 GEO。

JSON-LD 的 `description` 欄係另一條通道：畫面唔出一段字，但 Google 讀 schema。**唔代替**可見定位段。兩樣一齊：畫面一段短句 + schema 一句 description。

### 畫面點放（唔破壞旗艦店 look）

Customize → Homepage → Hero 已經有 H2「COLOURLIVING」同 *The House of Brands*。  
**唔好再加 Custom Liquid 隱藏段。** 把副標題／其下 Rich text **換成可見短句**（字可以細、同而家 Beige 風格）。

**建議可見英文（約 45 字，貼 Hero）：**

> Hong Kong’s House of Brands for European furniture, lighting and bathroom. The flagship at 333 Lockhart Road, Wan Chai presents collections including B&B Italia, Gessi, Dornbracht and Flos. Delivery within Hong Kong. Book a showroom visit.

中文等 ZH publish 再開一段，唔好而家用隱藏中文。全文版：[nap-source-of-truth.md](nap-source-of-truth.md)。

核對：無痕開主頁，**唔使 View Source 都睇到** 灣仔／bathroom／Hong Kong。原始碼入面呢段 **冇** `visually-hidden`。

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

可選：`"knowsAbout": ["furniture", "lighting", "bathroom fittings"]` — 三個詞即得，**唔好**把 Gessi／Roca 全名單塞入 schema。品牌靠 collection 頁。

**唔好用：** `DepartmentStore`、`HardwareStore`、`WholesaleStore`（類型錯）。**唔好**為浴室再開第二個 Organization。

改法：`header.liquid` 而家嗰份 FurnitureStore script，只改 `@type` 一行 + 喺 `name` 下面加 `description`。產品 Product schema **唔好動**。改完 View Source 應仍得 **一份** Organization。

完整稿：[schema-jsonld-shopify.md](schema-jsonld-shopify.md)。測：Rich Results Test 貼主頁。
