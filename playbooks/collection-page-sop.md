# 分類 / 品牌頁 SOP

## 品牌頁

**URL：** `/collections/gessi`（handle 穩定、全小寫、無空格）

**H1 EN：** Gessi Hong Kong | Bathroom collections at COLOURLIVING  
**H1 ZH：** Gessi 香港｜COLOURLIVING 浴室系列

**Meta title：** Gessi Hong Kong Authorised Retailer | COLOURLIVING  
**Meta desc：** See Gessi taps and bathroom collections at COLOURLIVING, 333 Lockhart Road, Wan Chai. Book a showroom visit. Delivery in Hong Kong.

### 模組順序

1. 答案段（授權關係、地址、預約、只送香港）
2. 系列導航（若系列多，用精選 collection 或 mega 連結）
3. 產品 grid
4. 品牌故事（改寫，200 字內）
5. 香港項目場景（住宅浴室、酒店）
6. FAQ 4 條
7. CTA

### 答案段範本

> COLOURLIVING presents Gessi in Hong Kong at its Wan Chai flagship, 333 Lockhart Road. Specialists help you specify taps, showers and accessories for residential and project use. Book a visit; delivery is available within Hong Kong.

中文同步一段。

---

## 品類頁

**URL：** 語意清晰，例如 `/collections/bathroom-faucets`，**唔用** `bath-1`。

**H1：** 品類 + Hong Kong / 香港  
例：European bathroom faucets in Hong Kong  
歐洲浴室龍頭

### 獨特文案（禁止貼 About）

覆蓋：

- 呢頁有邊啲品牌
- 點樣選（入牆 vs 明裝、面飾、恆溫）
- 點解要到灣仔睇實物
- 連去 2 個品牌頁 + 1 篇指南

最少 150 字 EN + 150 字 ZH，互為翻譯而非關鍵字堆砌。

### Filter

Shopify 篩選可留，但 **唔要** 為每個 filter 組合做 index。`robots.txt` 已 disallow `+` 同 multi-filter，保持。

若某組合戰略極重要（例如 `gessi + basin mixer`），應做 **獨立 collection 或品牌頁錨點**，而唔係依賴 filter URL。

---

## 上線檢查

- [ ] Handle 無 `-1`、無重複近義頁（bath vs bath-1 vs bathroom）
- [ ] Canonical 正確
- [ ] 中英 hreflang
- [ ] 首屏有答案段
- [ ] 內部連結到 showroom
- [ ] 空 collection（0 產品）noindex 或唔發布
