# 產品頁 SOP（**只限流程第 2 步**）

總順序：[content-workflow.md](content-workflow.md)。同 collection SOP 一齊做完就停；寫 Journal 唔用呢份。

每次改一個 SKU 都走完整張清單。英雄產品用人工；長尾可用模板但要過眼。

---

## 1. 顯示標題（Storefront title）

**EN：** `Brand + Collection + Product type + Model/SKU`  
**ZH：** `品牌 + 系列 + 中文品類 + 型號`

| 差 | 好 |
| --- | --- |
| Alys LY153 Bed | B&B Italia Alys LY153 Bed |
| Rilievo 59001299 | Gessi Rilievo basin mixer 59001299 |
| Insignia A5A323AC00 | Roca Insignia A5A323AC00 basin mixer |
| IC 10 Anniversary F1 F3173344 Floor Lamp | Flos IC Lights 10 Anniversary F3173344 floor lamp |

中文例：`Gessi Rilievo 面盆龍頭 59001299`

字數：盡量 60–80 字元內，型號唔可刪。

---

## 2. SEO title / meta description（theme metafield 或 Shopify SEO 欄）

**EN title：** `Gessi Rilievo Basin Mixer | COLOURLIVING HK`  
**ZH title：** `Gessi Rilievo 面盆龍頭｜COLOURLIVING 香港`

**Description 公式：**  
`[一句功能] [產地/設計師] [香港可睇或現貨] [預約/送貨]`

例：Italian Gessi Rilievo basin mixer in chrome. View and specify at COLOURLIVING, 333 Lockhart Road, Wan Chai. Hong Kong delivery.

---

## 3. 開頭答案段（40–80 字，放描述最頂）

必須完整句子，含品牌、品類、一項規格、香港行動。

EN 例：

> The B&B Italia Alys LY153 bed, designed by Gabriele and Oscar Buratti, is a leather-upholstered bed frame available to view at COLOURLIVING in Wan Chai. Confirm display-stock condition and Hong Kong delivery with our specialists before purchase.

ZH 例：

> B&B Italia Alys LY153 床架由 Gabriele and Oscar Buratti 設計，皮革床頭造型可於灣仔 COLOURLIVING 陳列室鑑賞。傢俬或為陳列品，購買前請與專人確認狀態、呎吋及香港送貨安排。

跟住先放品牌故事（可保留英文原文 + 中文摘要）。

---

## 4. 規格表（保持欄位，中英 label）

建議固定欄位：

- Brand / 品牌
- Brand origin / 產地
- Collection / 系列
- Designer / 設計師
- Design year / 設計年份
- Model no. / 型號
- SKU
- Dimensions mm / 呎吋
- Finish / 面飾
- Product type / 產品類型（人讀：Basin mixer，唔好 dump JSON）

空欄唔好顯示「Bundle:」空白行。

---

## 5. 香港購買模組（可做 metafield 全站共用 + 產品覆寫）

- 送貨只限香港
- 滿 HK$3,000 免運條件
- 傢俬／燈飾可能是 display unit
- 預購價或不同
- 保養 1 年（若屬實）
- CTA：WhatsApp / Book showroom

---

## 6. 產品 FAQ（每品類 3 條，唔好再用全站訂單 FAQ 當唯一 FAQ）

龍頭例：

- Is this the complete mixer or trim only?
- Which finish is in stock in Hong Kong?
- Can COLOURLIVING arrange specification for a renovation project?

梳化例：

- What is the width, and does it fit a typical HK lift?
- Is this a display piece?
- Can I see the fabric in Wan Chai?

---

## 7. Admin 欄位（影響 GEO JSON / Merchant）

- Vendor = 官方品牌拼寫（B&B Italia 唔好 BB Italia 混用）
- Product type = 標準詞（Bed, Basin Mixer, Floor Lamp）
- Tags = `brand:gessi`, `category:faucet`, `room:bathroom`, `lang-ready:zh`
- SKU / barcode
- Weight（物流）
- 價格 HKD 同頁面一致
- 庫存狀態真實

---

## 8. 媒體

- 主圖白底或官方圖
- 第二張起：陳列室實拍更佳
- Alt：`Gessi Rilievo chrome basin mixer`
- 呎吋圖有則放，利於 AI 引用

---

## 9. 內連

- 品牌 collection
- 品類 collection
- 2–3 個同系列
- Showroom 頁

---

## 10. 發布檢查

- [ ] 中英 title 都有品牌 + 品類 + 型號
- [ ] 無模板洩漏、無 `?` 取代重音字母
- [ ] 價格、庫存、Merchant 一致
- [ ] 答案段可見於「查看原始 HTML」（唔好只喺 tab 載入後出現）
- [ ] 法律：授權、exclusive 用詞正確
