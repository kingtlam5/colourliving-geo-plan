# 用一句講俾管理層：llms.txt、agents.md、schema 有咩分別

三樣都係 **寫俾機械睇、唔係寫俾客人睇嘅網頁**。客人落網站唔會「打開 llms.txt 嚟購物」。分別係 **邊部機械、讀嚟做咩**。

| | Schema | llms.txt | agents.md |
| --- | --- | --- | --- |
| 用白話講 | 公司同產品嘅 **結構化名片** | 俾 AI 助手嘅 **一頁品牌簡介** | Shopify 裡面嘅 **正本檔**；改它就等於改 llms.txt |
| 主要讀者 | Google（搜尋、地圖、知識卡）；AI 有時都會抄 | ChatGPT、Perplexity、Gemini 等 | 唔係第三個對外頻道；係產生 llms.txt 的源 |
| 客人會唔會見到 | 唔會。藏喺網頁原始碼 | 幾乎唔會。網址係 `/llms.txt` | 幾乎唔會。網址係 `/agents.md` |
| 幫到咩生意 | 品牌搜尋更穩、地圖／營業時間、產品價錢標記 | 有人問 AI「香港邊度買 Gessi／B&B」時被點名 | 同上（因為 Shopify 用它去餵 llms.txt） |
| 我哋而家改邊度 | Theme `header.liquid` 嗰段 Organization JSON-LD | **唔使分開改。** 加 `agents.md.liquid` 三條網址一齊變 | Edit code → `templates/agents.md.liquid` |

## 三句可以照讀

1. **Schema** 係同 Google 講：「我哋叫 COLOURLIVING，喺灣仔洛克道 333 號，賣歐洲傢俬，呢件貨幾錢。」搜尋同地圖靠呢份。
2. **llms.txt** 係同 ChatGPT 呢類 AI 講同一套事實，用普通人讀得明嘅短文，等佢哋答「香港邊度睇 Gessi」時抄我哋，而唔係抄錯地址定競品。
3. **agents.md** 唔係多一個要經營嘅渠道。Shopify 規定：改 `agents.md` 就會一齊改 `/llms.txt`。所以技術上做一個檔，對外效果係 AI 簡介。

## 一個比喻

- Schema = 公司註冊處／名片上的欄位（名、地址、電話、類型），俾 Google 填表。
- llms.txt = 俾新助理嘅一頁 briefing（我哋係邊、賣咩、只送香港、去邊預約）。
- agents.md = 呢份 briefing 放喺 Shopify 檔案櫃嘅檔名；llms.txt 係印出嚟嘅副本。

三者要 **同一套 NAP**（店名、洛克道、電話、營業時間）。唔一致，Google 同 AI 會各信各嘅。
