# agents.md／llms.txt：我哋草稿 vs Shopify 預設

**2026-08-31 稍後：** 三條 URL 已上品牌稿（同字節）。對照 Shopify 預設仍然有用——你加 `agents.md.liquid` 就係用呢份換走預設。Live 細節：[live-setup-audit-2026-08-31.md](live-setup-audit-2026-08-31.md)。

**對照時的 live（上稿前）：** `/agents.md`、`/llms.txt`、`/llms-full.txt` 係 **Shopify 原廠同一套購物說明**。三條 URL 內容幾乎一樣，只係 Store Metadata 一句話跟住「你而家讀緊邊條」微調。

加 `templates/agents.md.liquid` 會 **整份取代** 預設，唔會合併。所以你見到「好多 heading 冇咗、UCP 唔喺最頂」係正常——我哋係用品牌百科 **換走** Shopify 開檔廣告，UCP 整節搬去下半，唔係平台 API 消失。

真正結帳通道 **唔喺呢份 Markdown**：`GET /.well-known/ucp` 同 `POST /api/ucp/mcp` 由 Shopify 平台提供，theme 刪幾多字都刪唔走。呢份檔只係 **教 agent 舖係邊間、協議去邊度搵**。

可貼稿：[agents-md-liquid.md](agents-md-liquid.md)。加檔方法：[how-to-edit-llms-txt.md](how-to-edit-llms-txt.md)。

---

## 檔案結構對照（heading 順序）

Shopify 預設（而家 live）大致係：

1. `# Agent Instructions — COLOURLIVING` + 「點同網店互動」一句
2. `## For Personal Shopping Assistants…`（整節推 Shop skill / Shop Pay）
3. `## Commerce Protocol (UCP)` → Discovery、MCP、6 步、versions、`### Important Rules`
4. `## Read-Only Browsing` → `### Product Data` → `### Store Metadata`
5. `## Store Policies`
6. `## Platform`（開舖、shopify.dev、ucp.dev、Shop skill 再推一次）

我哋草稿大致係：

1. `# Agent Instructions — {{ agents.store_name }}` + House of Brands 一句 + NAP／送貨／預約
2. `## What we are` / `## Brands` / `## How to cite us` / `## Chinese summary`
3. `## Commerce Protocol (UCP)` → 同樣 Discovery、MCP、6 步、versions、`### Rules`
4. `## Read-only browsing` → 同樣 products.json 等 → `### Store metadata`
5. `## Policies`
6. **冇** `## Platform`

所以你見到嘅「UCP 位置好唔同」＝ **順序改咗，唔係刪咗**。預設把結帳協議放第二節；我哋把灣仔／品牌放前面，UCP 跟住。

---

## 邊段唔同（對照表）

| 區塊 | Shopify 預設（而家 live） | 我哋草稿 `agents-md-liquid.md` | 對 AI 讀站／買嘢 |
| --- | --- | --- | --- |
| 標題 | `# Agent Instructions — COLOURLIVING` + 「點同網店互動」 | 同一句式 `# Agent Instructions — {{ agents.store_name }}`，改用 House of Brands 開場 | 細。Agent 認檔靠 URL（`/agents.md`、`/llms.txt`），唔靠呢個 H1 |
| **Shop skill 長文**（檔案最頂） | 成節 *For Personal Shopping Assistants…* 推 `shop.app/SKILL.md`、Shop Pay、跨店搜貨 | **刪長文**；`### Rules` 留一句：冇即時買家批准就 prefer Shop skill + Shop Pay | 購物 agent 可能少咗「第一眼裝 Shop skill」。Luxury 多數要到店指定，**刻意唔把 unattended checkout 放最頂** |
| 店係邊、賣咩、NAP、品牌、中文、只送香港 | **完全冇** | **有（草稿上半）** | **呢舊先係 GEO。** 預設令 ChatGPT 只知「又一間 Shopify 網店」，唔知灣仔／Gessi |
| **UCP 放邊** | 標題之後第二大節 | 品牌段之後先至 UCP | **內容仍在。** 只讀檔案頭幾千字嘅 crawler 會先食到品牌，後食到結帳。Checkout agent 多數另外打 `/.well-known/ucp`，唔靠 Markdown 排位 |
| Commerce Protocol 內容 | Discovery + MCP **寫死** 完整 URL | `agents.ucp_discovery_url`／`mcp_endpoint_url` 生成，內容等價 | **要留。** 草稿有。Liquid 較唔會過期 |
| Typical agent flow 6 步 | 有 | 有 | 無影響 |
| Supported UCP versions | 寫死 `2026-08-25` 等 | `{% for version in agents.ucp_versions %}` | **草稿更好**（平台升版會跟） |
| Important Rules | 付款要人批、429、address_country；冇批准就裝 Shop skill | 同樣三條 + 只送香港、陳列室、唔好話 exclusive、display stock | 預設三條仍在；我哋多咗舖頭規則。Heading 叫 `Rules` 唔叫 `Important Rules`，agent 認嘅係條文唔係 heading 名 |
| Read-only：products.json、search、collections | 有（包喺 Product Data 細節） | 有（同一組 URL，少咗「No Authentication Required」包裝句） | 無影響。JSON 端點係平台路由，唔係 Markdown 創造出嚟 |
| **Store Metadata** | Sitemap；`/agents.md` 係 canonical。`/llms.txt` 會加「You're reading `/llms.txt`, which mirrors…」；`/agents.md` 寫「this document is canonical」 | `### Store metadata`：sitemap + 「canonical 係 `/agents.md`，llms／llms-full mirror」 | **低。** 預設三條 URL 用三個微調句；我哋一個 template 餵三條，所以用一句講晒。URLs 本身唔變 |
| Store Policies | privacy／terms／refund | 有（heading 叫 `Policies`） | 無影響 |
| **## Platform** | Shopify 廣告：開舖、shopify.dev、ucp.dev、Shop skill 再推一次 | **整節刪** | **唔影響讀你哋貨盤。** Agent 唔使知點開一間 Shopify。`ucp.dev` 已喺 UCP 節；Shop skill 已喺 Rules |

---

## 刪咗／搬位會唔會令 AI「讀唔到網站」？

**唔會封站、唔會令 Google 唔 index、唔會令 UCP API 消失。** `llms.txt` 改嘅係「agent 簡介」，唔係 robots、sitemap 或 PDP。

| 擔心 | 實際 |
| --- | --- |
| 冇咗 Agent Instructions／Platform，Google／ChatGPT 唔知有網店 | 唔會。頁面、sitemap、schema、collection 照 crawl。llms 改咗係 **簡介內容** 變 |
| UCP 唔喺第二節，購物 agent 搵唔到 | **只當你連 Discovery／MCP 兩行都刪。** 草稿有留，只係排後。真正能力仍喺 `/.well-known/ucp`（平台，同 Markdown 無關） |
| Shop skill 長文冇咗，買唔到 | Skill 網址仍喺 Rules。個人購物 agent 多數自己知 `shop.app/SKILL.md`。COLOURLIVING 高價貨本嚟唔應靠 unattended Shop Pay |
| Store Metadata 句式同預設唔一字不差 | 三個 URL 同一稿就夠。Agent 跟 `/sitemap.xml`、`/agents.md` 路徑，唔背誦 Shopify 廣告句 |
| Heading 名改咗（Important Rules → Rules；Store Policies → Policies） | 無影響。模型讀段落意思，唔係對 Shopify 預設 heading 做 checksum |
| 只讀檔案頭、截斷後面 | **預設反而更差：** 頭半截全係 Shop Pay 廣告，零洛克道。我哋把品牌放前，GEO 問「香港邊度睇 Gessi」先食到有用事實。Checkout 細節仍喺同一檔下半，兼有獨立 UCP discovery |

預設檔 **對 GEO 較差**：成份係「點用 Shopify 買嘢」，零洛克道、零品牌。ChatGPT 問「香港邊度睇 Gessi」時，預設 llms **幫唔到**，甚至令模型當你係普通可以 Shop Pay 即買嘅網店。

---

## 建議點處理（唔使抄返 Shopify 廣告）

1. **品牌上半一定要**（NAP、2,000 sqm、品牌、只送香港、中文、點引用）。  
2. **UCP 下半一定要**（discovery、MCP、6 步、versions Liquid、Rules、products.json、sitemap、policies）。排喺品牌後面冇問題。  
3. **已經加返、零成本：** 標題 `Agent Instructions —`；Store metadata 講 canonical `/agents.md`；Rules 講 Shop skill。  
4. **唔使加返：** `## Platform`、開舖連結、shopify.dev、檔案最頂成篇 Shop Pay 銷售文。唔使為咗「同 Shopify default 一模一樣」把 UCP 搬返第二節。

Shopify 官方注意：預設 `agents.md` **刻意唔放** 電郵／電話，因為檔案會被廣泛 cache。Liquid 草稿跟呢個：地址同營業時間留（GEO 要），電話／電郵放 About／GBP。法務稿 [llms-txt-draft.md](llms-txt-draft.md) 可以有電話，上 theme 前再決定。
