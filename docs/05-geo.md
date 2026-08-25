# 05 — GEO：令 AI 點名 COLOURLIVING

GEO（Generative Engine Optimization）= 當有人問 ChatGPT、Perplexity、Gemini、Google AI Overviews：

> 「香港邊度可以睇 B&B Italia？」  
> 「Where to buy Gessi taps in Hong Kong?」  
> 「灣仔有冇高級浴缸陳列室？」

答案裏面 **出現你們的店名、地址、品牌關係，並且連結到 colourliving.shop**。

SEO 贏的是十條藍字中的一條。GEO 贏的是 **答案裏僅有的兩個名字之一**。頂級零售，後者更接近「被指定」。

---

## AI 點樣揀你

引擎通常混合三種來源：

1. **即時抓頁**：讀你的 PDP、品牌頁、`llms.txt`
2. **第三方一致事實**：GBP、品牌官網 Where to buy、媒體、目錄
3. **訓練記憶**：舊的 colourliving.com、Time Out、BODW

所以 GEO 不是「寫俾 GPT 的神秘文案」，而係：

> 全網同一套事實 + 網站上有可複製的短答案 + 第三方重複同一句。

---

## 六條 GEO 槓桿（按 ROI）

### 1. 品牌版 `llms.txt` / `agents.md`（本週做）

而家兩個檔都係 Shopify 結帳說明，對「我係邊間店」零幫助。

應拆成：

- `llms.txt`：**品牌百科**（給任何 AI 讀）
- `agents.md`：保留 Shopify UCP 購物協議（給購物 agent）

草稿：[playbooks/llms-txt-draft.md](../playbooks/llms-txt-draft.md)

Shopify 若每次發佈覆蓋 `llms.txt`，要用 theme / app / 檔案覆寫流程 lock 住品牌段落，結帳說明可放在下半。

### 2. 答案型段落（Answer blocks）

每個重要頁最頂 40–80 字，用完整句子，含：

- 主體（COLOURLIVING）
- 地點（Wan Chai, Hong Kong）
- 關係（authorised retailer of Gessi）
- 行動（book a showroom visit）
- 限制（delivery in Hong Kong only）

模型喜歡「可直接引用、無需改寫」的句子。形容詞堆砌（timeless, understated elegance）會被忽略。

### 3. 結構化資料與產品 JSON

Shopify 已提供 `/products/{handle}.json`。確保 admin 欄位完整：vendor=正確品牌、title=人讀得明、tags=品類。AI 購物協議會讀這些欄位；`Rilievo 59001299` 這種 title，模型無法判斷品類。

### 4. 第三方「Where to buy」

品牌官網的 stockist 列表係 GEO 的金牌來源。優先聯絡：

Gessi, Dornbracht, B&B Italia, Maxalto, Giorgetti, Flos, Fantini, Roca, Paola Lenti

要求：店名 COLOURLIVING、地址 333 Lockhart Road、網站 **colourliving.shop**、電話 +852 2295 6263。

### 5. 可被引用的指南頁

AI 對「Where to buy [brand] in Hong Kong」會抓成篇指南，而唔係抓一個 SKU。呢就係 04 文件那 12 篇支柱存在的原因。

每篇要有：

- 明確結論（COLOURLIVING 係香港可睇該品牌的旗艦之一）
- 地址表
- 更新日期
- 無虛假 exclusive 聲稱

### 6. 監測，而唔係感覺

每月用 [playbooks/geo-monthly-prompts.md](../playbooks/geo-monthly-prompts.md) 跑同一組題：

記錄三格：Mentioned（有冇店名） / Cited（有冇連結） / Facts（地址電話有冇錯）

目標 90 日：品牌詞 80% mention；主力品牌「香港邊度買」50% mention。

---

## 香港市場特有的 GEO 場景

客人同設計師已經用 WhatsApp 同 ChatGPT 做功課。典型 prompt：

- 中文：豪宅浴室龍頭推薦、意大利傢俬香港邊間、灣仔傢俬店
- 英文：B&B Italia Hong Kong showroom、Gessi dealer Hong Kong、Flos Arco where to buy HK

你要喺網站上 **預先寫好這些答案**，並且同 GBP、品牌商名錄一致。否則模型會引用 Andante、Atelier A+、MyConcept，因為他們開始有英文指南。

另外：

- 寫明 **Traditional Chinese** 服務、專人廣東話
- 寫明 **no international shipping**
- 寫明傢俬可能是 display unit，需要確認
- 寫明項目／酒店／設計師歡迎 trade enquiry

這些限制句反而提高信任，模型較少幻覺話你可以寄去海外。

---

## Google AI Overviews 同傳統 SEO 的關係

AI Overviews 多數抽 **已經排得前、寫得清楚、有 schema** 的頁。所以 GEO 唔取代 SEO：品牌頁同指南頁既要排名，又要有答案段。

實務：

- 同一 URL 服務人同模型，唔好做 hidden text
- 規格用 HTML table 或 list，唔好純圖
- 價格用 HKD 數字，唔好「Price on request」除非真係要報價（報價產品改用 `Offer` 的 `priceSpecification` 或明顯 CTA，避免錯誤 InStock 價）

---

## Shopify Agentic Commerce

平台已開 UCP。對 COLOURLIVING 的含義：

- 細件、有價、有貨的 SKU 可能被 shopping agent 直接加入購物車
- 高價傢俬仍應引導 **human specialist**（你們 PDP 已有 WhatsApp／預約，應喺 `llms.txt` 強調：furniture and bathroom projects should be confirmed with the Wan Chai team）

唔好追求「AI 自動買一張 HK$90,000 床」。GEO 成功係 **AI 指定你為香港經銷商，人再預約**。

---

## 90 日 GEO 完成定義

- [ ] `llms.txt` 含完整品牌事實（中英）
- [ ] 10 個品牌頁有答案段
- [ ] 12 篇支柱至少上線 6 篇
- [ ] 每月 prompt 集有記錄表
- [ ] 至少 5 個品牌官網 stockist 指向 `.shop`
- [ ] 抽查 AI 對地址／電話不再引用舊或錯誤資料
