# GBP：一個洛克道店，唔好每個品牌一張檔案

Google 政策：**同一盤生意、同一個門牌，只可以有一個 Business Profile。**  
[Guidelines](https://support.google.com/business/answer/3038177)／[Resolve duplicates](https://support.google.com/business/answer/12756178)。

COLOURLIVING 係 **一間** House of Brands 旗艦（333 Lockhart Road、同一電話、同一班人、同一個門口）。B&B Italia 樓層、Maxalto、龍頭牆係 **陳列**，唔係另一間公司。

同事開嘅「B&B Italia at COLOURLIVING」「Herman Miller by COLOURLIVING」「Maxalto by Dentro」＝ **重複檔案**。唔好由得佢。**要合併入一張正牌 COLOURLIVING。**

---

## 點解唔可以留多張／當 department

| 誤會 | 實際 |
| --- | --- |
| 每個品牌一張檔，搜「Gessi Hong Kong」會出我哋 | 短期或會。Google 當誤導，可隱藏、合併錯檔、甚至連累正牌被標 duplicate |
| 同址可以開 department | Department 要 **真部門**：不同類別、通常不同電話／時間／入口（醫院科、車行 sales vs service）。傢俬陳列室品牌牆 **唔合格** |
| 地址電話一樣但店名唔同就唔算重複 | 政策睇「係咪同一盤生意」，唔單睇店名 |
| Maxalto by Dentro 冇 COLOURLIVING 三個字，當另一間 | Dentro 係舊招牌／舊叙事。同一個門牌賣 Maxalto = 同一間店。留住會令知識圖譜以為灣仔有兩間舖 |

品牌搜尋應靠：**正牌 GBP 簡介／相片／產品 + 網站 collection + llms.txt + vendor locator**，唔靠假分店。

---

## 留邊張（survivor）

只留 **一張**：

- 店名：**COLOURLIVING**（可加 Wan Chai / 灣仔，唔好加品牌名）
- 已 verify、你而家 manage 到
- 評論最多／開得最耐（合併後評論通常會併過去；回覆或會冇）
- 類別主：**Furniture store**
- NAP 同 [nap-source-of-truth.md](nap-source-of-truth.md) 逐字
- Website：`https://colourliving.com`（301 去店）

**唔好**把 survivor 改名做「B&B Italia at COLOURLIVING」——Google 要店名同門口招牌一致。

---

## 其他檔點處理

| 類型 | 做法 |
| --- | --- |
| `… at COLOURLIVING` / `… by COLOURLIVING`（B&B、Gessi、Flos、Herman Miller…） | **Request merge** 入正牌。唔好「永久關閉」（關咗評論多數帶唔走） |
| `Maxalto by Dentro`、舊公司名、錯品牌名 | 一樣 **merge 入 COLOURLIVING**（同一門牌舊名）。簡介唔好再寫 Dentro 做而家店名 |
| 已冇代理嘅品牌（例如 Herman Miller 若已離場） | 仍然係重複檔，照 merge。**唔好**留住誤導「呢度仲賣」 |
| 第二個實體店／已結業分店（另一個地址） | **唔好 merge。** 標 Permanently closed |
| 你管唔到、未 verify 的垃圾 pin | Maps 對住正牌 **報 duplicate**；必要時 GBP 支援 |

合併成功：評論合併；你指定邊張係正牌。Google 人手審，要等。

---

## 你喺 Admin 點做（有權限）

1. **盤點。** 試算表：店名、Maps URL、評論數、verify 未、電話、網站。標 survivor。  
2. **NAP 對齊。** 重複檔地址／電話改到同 survivor **完全一樣**（合併條件）。店名暫時唔使改到同名。  
3. **申請 merge（唔係 Dashboard 一個「Merge」掣）。**  
   - [Resolve duplicate profiles](https://support.google.com/business/answer/12756178) → 支援 → 講 merge duplicate  
   - 交兩張檔的 **Business Profile ID**（檔案 ⋯ → Settings → Advanced）同 Maps URL  
   - 寫明：同一間店、同一地址 333 Lockhart Road；survivor = COLOURLIVING；其他係舊同事按品牌開的重複檔  
4. **Maps：** 開重複檔 → Suggest an edit → 標 duplicate／同一間生意。  
5. **一次合併兩三張**，等 Google 做完再下一批。唔好一日報二十張。  
6. **等。** 唔好同時改 survivor 店名、搬地址。合併期間唔好關閉重複檔。

管唔到的檔：用公司文件（BR、水電單、門牌相）向支援證明所有權，或只報 duplicate。

---

## 合併之後品牌點出現

正牌 COLOURLIVING 一張檔：

- 簡介：House of Brands；列 B&B Italia、Maxalto、Gessi、Flos…（授權用語跟 NAP 檔）  
- 相片：分相簿（家具／浴室／B&B 樓層），相說明寫品牌  
- 產品／帖：連去 `/collections/gessi` 等  
- 網站、schema `knowsAbout`、llms.txt 已經係品牌名單來源  

**唔好再開**「Gessi at COLOURLIVING」。

Apple Business Connect／Bing Places 若都有品牌分身，同樣收斂成一個 COLOURLIVING。
