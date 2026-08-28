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
定位段的目的係俾 **人同 AI 引用**（店名、灣仔地址、傢俬＋燈＋浴室）。藏起就做唔到 GEO。**只送香港**放 Customer Care／FAQ，唔寫入 Hero。

JSON-LD 的 `description` 欄係另一條通道：畫面唔出一段字，但 Google 讀 schema。**唔代替**可見定位段。兩樣一齊：畫面一段短句 + schema 一句 description。

### 畫面點放（唔破壞旗艦店 look）

Customize → Homepage → Hero 已經有 H2「COLOURLIVING」同 *The House of Brands*。  
**唔好再加 Custom Liquid 隱藏段。** 把副標題／其下 Rich text **換成可見短句**（字可以細、同而家 Beige 風格）。

**建議可見英文**可以係生活雜誌風，唔一定要「Hong Kong’s House of Brands…」咁直。事實清單同雜誌句見下面「語氣」。

中文等 ZH publish 再開一段，唔好而家用隱藏中文。NAP 鎖定仍係 [nap-source-of-truth.md](nap-source-of-truth.md)。

核對：無痕開主頁，**唔使 View Source 都睇到** 灣仔／bathroom／Hong Kong。原始碼入面呢段 **冇** `visually-hidden`。

### 語氣：唔使寫到好似說明書

SEO／GEO **唔要求**樸素英文。Google 同 AI 要嘅係 **拎得走的事實**，唔係「唔准有文采」。旗艦店用生活雜誌風，只要同一段入面仍包到下面，就友善：

| 要有 | 點解 |
| --- | --- |
| 店名 COLOURLIVING 一次 | AI 抄呢段時先至知係邊間，唔只抄 tagline |
| 333 Lockhart Road, Wan Chai | 同 NAP 逐字 |
| furniture、lighting、bathroom（或 bath） | 品類；單寫 wellness 搜「龍頭／bathroom」會弱 |
| 2–4 個品牌名 | 證明 House of Brands |
| Hong Kong | 寫入**地址**（Wan Chai, Hong Kong），唔寫 Delivery。送貨政策放 Customer Care／FAQ |

第一句可以係純氛圍，**第二句**先有店名＋完整地址。唔好整段都係形容詞。

**Homepage 唔寫 delivery。** 「只送香港／不接受國際運送」已有 FAQ，應留 Customer Care。地理用地址裡的 *Hong Kong* 已經夠 GEO。

**2026-08-28 採用稿（雜誌風，無運送句）：**

> The definitive address for refined European living.  
> COLOURLIVING, 333 Lockhart Road, Wan Chai, Hong Kong — furniture, lighting, and bath collections from B&B Italia, Flos, Gessi, and Dornbracht.

由你原稿收緊：段內加店名同 Hong Kong（地址，唔係送貨）；*Immerse / exceptional craftsmanship / curated masterworks* 疊咗太多形容，品牌同地址已經夠；Gessi／Dornbracht 帶浴室，仍留 *bath* 一個詞方便搜尋。

Schema `description` 可以繼續較直，畫面用上面語氣。運送細節唔使寫入 schema description。

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
