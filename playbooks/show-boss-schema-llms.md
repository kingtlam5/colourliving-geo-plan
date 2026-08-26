# 點樣 show 俾管理層：schema / llms.txt 改完有咩用（唔使睇 code）

**先講一句，避免期望錯：** 客人打開 https://colourliving.shop 的 **畫面唔會變**。呢兩樣唔係改 banner、唔係改價錢。有用嘅係 Google 同 ChatGPT **讀到嘅資料**。要證明，就 screenshot **機械睇到嘅頁**，唔係 screenshot 網店首頁。

開會用 10 分鐘：3 張 **而家** 圖 + 改完再影 3 張 **之後** 圖 + 講清楚邊啲要等 Google／AI 幾週。

---

## 一、用呢個比喻開場

| 客人見到 | 機械見到（你要 screenshot 呢邊） |
| --- | --- |
| 網店畫面 | Google 測試工具讀到嘅 JSON 名片 |
| （唔會打開） | 瀏覽器打開 `/llms.txt` 嗰篇文字 |
| Google 十條藍字、地圖、ChatGPT 答案 | 幾週後先變；今日用測試工具證明「原料已換」 |

改 schema／llms = 換公司登記同 AI briefing。登記換咗，地圖同 AI 答案唔係即日自動變新招牌——但 **而家可以證明 Google／AI 將會讀到邊份新資料**。

---

## 二、Schema：screenshot「Google 而家點讀我哋」

呢個最似「Google crawl 我地」。唔係一條蜘蛛爬過畫面，而係 Google 官方工具話你知佢從頁面抽到咩。

### 圖 1 — Google 豐富結果測試（最重要）

1. 開：https://search.google.com/test/rich-results  
2. 貼：`https://colourliving.shop/`  
3. 撳測試 → screenshot **整頁結果**

**重要：而家首頁顯示「No items detected」係正常，唔係網站壞咗。**  
Rich Results Test **只報會變成搜尋特別樣式的類型**（產品星星、FAQ、本地商家卡）。普通 `Organization`（店名、logo、社交）同 `WebSite` **唔算 rich result**，所以工具當「0 items」。Google 仍然有讀到 schema。

要見到而家嗰份 Organization：用 https://validator.schema.org/ 貼首頁 URL，或喺豐富結果頁撳 **VIEW TESTED PAGE** 搜 `ld+json`。  
測產品頁（例如 Alys 床）先會喺 Rich Results Test 見到 **Product**。  
Publish FurnitureStore + 地址之後，首頁呢個工具 **有機會** 出現 Local business；仍然以 schema.org validator 做 Organization 的 before／after。

再貼一隻產品 URL（例如 Alys 床）測一次：證明產品價錢 schema **仍然有效**（你冇整壞 checkout 標記）。

（工具有時用快取。改完即測若仍舊，撳「測試實際網址」或等數分鐘再測。GSC **URL 檢查 → 要求編入索引** 可加快 Google 收新 HTML。）

### 圖 2 — 原始碼裡機械睇到嘅名片（1 分鐘）

1. Chrome 開 https://colourliving.shop/  
2. 右鍵 → **查看網頁原始碼**  
3. `Ctrl+F` 搜 `ld+json` 或 `sameAs`  
4. Screenshot 嗰段 JSON

Before：`sameAs` 有 `""`，冇 address。  
After：有 `FurnitureStore`、`333 Lockhart Road`，冇空字串。

話俾老細聽：客人撳右鍵先睇到；Googlebot 每次爬頁都讀呢段。

### 圖 3 — GSC「Google 點樣看待呢頁」（你已有 GSC）

1. Google Search Console → `colourliving.shop`  
2. 上面搜尋列貼 `https://colourliving.shop/`  
3. **URL 檢查**  
4. Screenshot：「已編入索引／未編入」、最後一次爬取、偵測到的項目  
5. 可撳 **查看已編入索引的網頁**（或「測試中的網址」）睇 Googlebot 拿到的 HTML

呢個先係「Google crawl 我地」的官方畫面。Schema publish 後過幾日再檢查同一 URL，對住日期。

**唔好承諾：** 測完即日 Google 搜「COLOURLIVING」知識卡會變。知識卡／地圖要 GBP + 時間。你證明嘅係 **原料已正確**。

---

## 三、llms.txt：screenshot「AI 而家讀到咩 briefing」

AI 唔用豐富結果測試。佢哋會開一份純文字。呢份 **本身就係 frontend**：用瀏覽器打開即可。

### 圖 4 — 而家嘅 llms.txt（改之前請今日就影）

開：https://colourliving.shop/llms.txt  

而家（2026-08-26 仍係）Shopify 預設：教 AI 點用 Shop skill／UCP 結帳，**冇** 洛克道、Gessi、B&B、只送香港、預約陳列室。

Screenshot 最上半頁。話：ChatGPT 若嚟認我哋，而家只見到「一間可以 checkout 的 Shopify 店」，唔見到旗艦店身份。

### 圖 5 — 改完同一條 URL

Publish `agents.md.liquid` 之後，**再打開同一條** https://colourliving.shop/llms.txt  

應見到 COLOURLIVING、灣仔、品牌、中文摘要。兩張圖並排。

可同時開 https://colourliving.shop/agents.md 證明兩條一齊變。

### 圖 6 — AI 答案（長遠、先影基準線）

用無痕／新對話，問（今日影一次當 Day 0）：

- Where to buy Gessi taps in Hong Kong  
- B&B Italia showroom Hong Kong  
- 灣仔 COLOURLIVING 地址同營業時間  

引擎：ChatGPT（開搜尋）、Perplexity、Gemini。Screenshot 有冇店名、地址啱唔啱、連去邊。

90 日後同一批題再影。呢個先係「對生意有實際影響」的圖：被點名、資料啱、連去我哋。完整題庫：[geo-monthly-prompts.md](geo-monthly-prompts.md)。

**唔好話** llms 一 publish，ChatGPT 翌日一定改口。AI 有記憶同其他來源（GBP、品牌 locator）。llms 係令原料正確；圖 6 用來證明趨勢。

---

## 四、時間線（免老細以為「改完 code 即上熱搜」）

| 幾時 | 你可以 show 咩 | 仲 show 唔到咩 |
| --- | --- | --- |
| Publish 當日 | 圖 1 豐富結果、圖 2 原始碼、圖 5 llms.txt 文字已換 | Google 搜尋結果頁、ChatGPT 答案未必變 |
| 數日–2 週 | GSC URL 檢查最後爬取日更新；豐富結果穩定顯示地址 | 品牌詞排名大升——通常唔會只因為 schema |
| 1–3 個月 | 地圖／知識卡較穩（要 GBP 一齊啱）；AI 較常抄對地址 | 保證某條 keyword 第 1 |

長遠實際影響（用呢幾句）：

1. Google 認我哋係 **灣仔傢俬旗艦店**，唔只係一個網店名 + logo。本地搜「灣仔傢俬／Gessi 香港門市」先有資格同地圖一齊出現。  
2. 產品價錢標記 **保持**；我哋冇整壞購物結果。  
3. AI 問「香港邊度買 Gessi」時，有一份 **官方 briefing** 寫明我哋係邊、只送香港、去陳列室——減少抄錯競品或舊 `.com` 故事。  
4. 呢啲係地基。之後寫產品文、出中文頁、做 GBP，先會喺搜尋同 AI **答案層** 見到生意。

---

## 五、開會建議流程（10 分鐘）

1. 開網店首頁：「畫面唔會因呢兩項而變，呢個正常。」  
2. 開豐富結果測試 before 圖：「Google 而家只知店名，唔知洛克道。」  
3. 開 `/llms.txt` before 圖：「AI 而家讀到 Shopify 購物說明，唔知我哋係旗艦店。」  
4. Publish 後（或 Preview 用實際網址測）after 圖：「而家機械名片同 briefing 已換。」  
5. 開 2–3 條 ChatGPT／Perplexity Day 0 圖：「呢個係基準；90 日後同一批題再比。」  
6. 收結：投資係 **令 Google 同 AI 以後讀到正確身份**；唔係改完即日多 50 單 online。Luxury 轉換仍然靠陳列室／WhatsApp，但被搵到、被點名先有人來。

改完當日把圖 1–5 存一資料夾：`YYYY-MM-DD-schema-llms-before-after`。圖 6 每月加一次。
