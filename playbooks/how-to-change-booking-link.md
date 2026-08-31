# 點改首頁「Reserve Your Visit」同 Microsoft Bookings 連結

Live 掣而家去（2026-08-31 第二次 audit）：

`https://outlook.office.com/book/COLOURLIVINGShowroomBooking@bschk.onmicrosoft.com/?ismsaljsauthenabled`

已唔再係 `Testing@`。仍係 `bschk.onmicrosoft.com` 租戶域。

舊測試 URL（已唔應出現喺首頁）：

`https://outlook.office.com/book/Testing@bschk.onmicrosoft.com/?ismsaljsauthenabled`

呢條 **唔係** Bookings 頁面標題改到就會跟。網站掣同 Microsoft 的「page link」係兩件事。

---

## 點解你喺 Microsoft Bookings 改唔到 URL

Bookings 的公開網址係跟 **scheduling mailbox** 生出嚟，例如 `Testing@bschk.onmicrosoft.com`。  
你可以改頁面標題、服務、時間、品牌外觀；**Bookings 介面冇欄位改呢段 URL**。Microsoft 官方亦講：URL 唔會跟 display name 變。

所以喺 Bookings 入面改「Booking page」名稱／內容，Shopify 掣仍然會去 Testing@——因為掣係 **Shopify 寫死的連結**，Microsoft 唔會返轉頭改你個 theme。

---

## 你真正要改嘅地方：Shopify 掣（5 分鐘）

1. **Online Store → Themes → Customize**（現行主題）
2. 左邊 Homepage 區塊名單，撳 **Discover Design In Person**（陳列室圖 + 「Reserve Your Visit」嗰截）
3. 撳個 **Button**／「Reserve Your Visit」block
4. **Link**（有時叫 Button link / URL）→ 刪走 Testing@ 嗰條
5. 貼你而家 **Share booking page** 複製出嚟嘅正確 URL → Save

呢步唔使改 theme Liquid。Customize 改到、Save，公開頁就跟。

核對：無痕開 `https://colourliving.shop/`，右鍵掣 → Copy link。唔應再見到 `Testing@`。

---

## 如果 Share 出嚟仍然係 Testing@

即係 **Bookings 日曆本身** 仲掛住測試 mailbox。網站再點改都只係換一條仍然叫 Testing 的 URL。要 IT／Microsoft 365 admin：

1. 開一間正式 Bookings 日曆（建議 mailbox 似 `visit@colourliving.com` 或公司域名，唔好 `…onmicrosoft.com` 測試戶）。
2. Publish → **Share** → 複製新 URL。
3. 把新 URL 貼返入上面 Shopify Button Link。

**唔好**指望改 Bookings 頁面標題就令 `outlook.office.com/book/Testing@…` 變成漂亮網址。要漂亮網址，係改／新建 mailbox，或網站用自己的按鈕文字遮住醜 URL。

舊 Testing@ 日曆：正式頁上線後 Unpublish，避免客人書籤仲入測試簿。

---

## 唔好做

| 做法 | 點解 |
| --- | --- |
| 只改 Bookings 頁面 Title | URL 唔變；Shopify 掣亦唔變 |
| 喺 Microsoft 搵「Edit page link」 | 多數根本無呢個掣 |
| 改 schema／agents.md | 同預約掣無關 |
