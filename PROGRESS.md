# 工作進度交接 · Session Handoff

> 這份檔案是給「下一個對話視窗」用的交接文件，不是公開的專案說明（那是 `README.md`）。
> 在新對話開始時，請先讀這份，就能無縫接續。最後更新：2026-06-17（現已含中／英／日**三語**版，並已 push 上線）。

---

## ⚠️ 0. 最重要：專案位置與身分（別跟另一個專案搞混）

使用者有**兩個容易混淆**的 Vision Zero Taiwan 街道專案：

| 專案 | 路徑 | 性質 |
|------|------|------|
| **StreetSoulQuiz**（← 就是這個） | `/Users/yunching0513/StreetSoulQuiz` | 靜態 HTML 16 型人格測驗 |
| street-vision | `/Users/yunching0513/202604 - 街道願景專案` | 本地 Next.js 資料視覺化 app（**不要**在這裡做測驗的事） |

- **本專案路徑**：`/Users/yunching0513/StreetSoulQuiz`
- **線上網址**：https://yunching0513.github.io/StreetSoulQuiz/
- **git remote**：`origin` = `yunching0513/StreetSoulQuiz`（使用者的 fork，push 到這）、`upstream` = `Visionzerotaiwan/StreetSoulQuiz`（之後再同步）
- 技術：純 HTML / CSS / vanilla JS，**無 build、無 npm**。所有東西都在單一 `index.html`（約 2700+ 行，全部 inline）。
- 當使用者說「用我自己的」= 指這個 GitHub fork。

---

## ✅ 1. 目前 git 狀態（已上線）

所有工作（前一批 + **日文版三語**）已 commit 並 push 到 `origin/main`，GitHub Pages 已部署，工作區乾淨。

已涵蓋：`index.html`（中／英／日三語、配對好友/幸運兒、雙分享圖卡、可愛音效、地圖連結、小行人、雙齊零正名）、`pedestrian.png`（已追蹤）、`VZT_petition_bilingual.html`、`PROGRESS.md`（本檔）。

**之後要再改 → 照常上線：**
```bash
cd /Users/yunching0513/StreetSoulQuiz
git add -A && git commit -m "..." && git push origin main   # Pages 約 1 分鐘後更新
```

> 待辦：日後把改動同步到 `upstream`（Visionzerotaiwan/StreetSoulQuiz）— 目前先不做。

### 🌐 三語架構（中／英／日）速記
- 語言由 `<body>` 的 class 決定：`zh` / `en` / `ja`。helper `getLang()` 回傳三者之一。
- CSS 互斥隱藏（約 line 320）：`body.zh` 藏 `.en-only,.ja-only`；`body.en` 藏 `.zh-only,.ja-only`；`body.ja` 藏 `.zh-only,.en-only`。
- **靜態/模板**：每組 `.zh-only`/`.en-only` 旁都加一個 `.ja-only` 兄弟元素。
- **資料**：日文走平行物件 `TYPES_JA`／`DEMANDS_JA`／`QUESTIONS_JA`／`TYPE_DEMAND_WHY_JA`（中英原資料沒動）。
- **JS 條件**（圖卡/分享文案）：原本 `isEn ? en : zh` → 改 `const lang=getLang()` + `L(zh,en,ja)` 三選一；`buildBondsCard / downloadShareCard / showImageModal` 都吃 `lang`。
- 語言選擇器與右上角 toggle 都已加「日本語」。
- 新增文案 → 記得補 `.ja-only` + 對應 `_JA` 欄位，並用 Playwright 三語各驗一次（**務必 stub `logToSheet`**）。

---

## ✅ 2. 本 session 完成的八項工作

1. **結果頁配對區塊**：新增「🚶 最佳散步好夥伴」與「🍀 街道幸運兒」兩張配對卡。
   - 函式 `renderBondsSection(code)`；buddy = 翻 social 軸、lucky = 翻全部四軸（皆為互逆配對，16 型都驗過：互相對應、不會配到自己）。
2. **版面位置**：配對區塊移到 **Manifesto 下面**；標題為「在這座城市裡，誰是你的漫步好朋友？」。
3. **分享圖卡產生兩張**（html2canvas，各 1080×1350 @scale2 = 2160×2700）：
   - **Card 1**：原本的街道靈魂卡（不動）。
   - **Card 2**：`buildBondsCard()` — 漫步好夥伴 + 街道幸運兒 + **你最閃閃發光的時刻（天賦 3 項）** + 雙齊零行動起點。
   - 下載走 `downloadShareCard()` → `showImageModal({cards:[card1,card2]})` 雙卡 modal。
4. **可愛音效**：`SFX` 模組（Web Audio API 合成，無音檔）。三角波 + 八度泛音、C 大調五聲音階。各互動有 hook（選語言/開始/答題/上一題/揭曉結果/切分頁），右上角有靜音鈕，狀態存 localStorage `ssq-muted`。
5. **地圖成果連結**：`.atlas-card`，連到 https://visionzerotaiwan.github.io/taiwan-mobility-atlas/ （本次倡議最重要成果），深色底 + lime 光暈。
6. **結果頁順序重排**：類型 → Manifesto → 天賦/成長/行動 → 夢想城市配對 → 誰與你同行(漫步好朋友) → 分享 → 🗺️地圖成果 → 五大訴求 → 延伸閱讀分頁 → 致謝。
7. **第一頁小行人插圖**：intro 標題右側加 `pedestrian.png`（使用者提供的 VZT 吉祥物，2080×1542）。`.intro-hero` flex 排版，手機版（≤560px）改直向堆疊。
8. **雙齊零正名 + 標題改字**：全站「雙零」→「雙齊零」（0 個殘留）；標題「在這座城市裡，誰與你同行？」→「誰是你的漫步好朋友？」。連署頁 `VZT_petition_bilingual.html` 的《雙零交通願景自治條例》也一併改成《雙齊零…》。

---

## 📋 3. 待辦 / 下一步

- [ ] **commit + push**（見上方第 1 節；務必含 `git add pedestrian.png`）→ 使用者尚未確認是否上線。
- [ ] 使用者提到「之後用 visionzerotaiwan 來更新」= 日後把改動同步到 `upstream`（Visionzerotaiwan/StreetSoulQuiz），目前**先不做**。
- [ ] 視覺最終確認：本 session 因 API 圖片數限制，Card 2 的截圖沒能親眼看；功能驗證（內容高 = 容器高 = 1350，無裁切）已過。建議在新對話用 Playwright 重截一張 Card 2 做最終目視確認。

---

## 🧪 4. 如何預覽與測試

**本地預覽**（靜態 server，注意 8000 常被佔用，改用 8123）：

```bash
cd /Users/yunching0513/StreetSoulQuiz
python3 -m http.server 8123
# 開 http://127.0.0.1:8123
```

**Playwright 驗證結果頁的標準做法**（直接跳到指定型，不用真的答 12 題）：

```js
// 1) 強制某個型 + 把 logToSheet 變 no-op（避免污染正式 Google Sheet！）
await page.evaluate(() => {
  window.calculateType = () => 'MECY';   // 任一 4 字代碼
  window.logToSheet   = () => {};        // ← 測試務必 stub，別寫進正式試算表
});
// 2) 呼叫 showResult()（內含 1300ms setTimeout 才 render）
await page.evaluate(() => showResult());
await page.waitForTimeout(1500);
// 3) 要驗 Card 2：呼叫 downloadShareCard() 後檢查產生的兩張卡
```

> **鐵則：測試一定要 stub `logToSheet`**，否則每次測試都會寫一筆假資料到正式 Google Sheet。

---

## 🗺️ 5. 程式架構速查（都在 `index.html`）

- **`TYPES`**（約 line 1079+）：16 型資料物件。每型有 `emoji`、`zh_name`/`en_name`、`rarity`、`desc_*`、`strengths_zh`/`strengths_en`（3 項陣列）、`growth_*`、`action_*`、城市配對 `match_*`、`article_*`、`quote_*`。
- **`renderBondsSection(code)`**：配對區塊。輔助：`AXIS_OPP`（軸對立表）、`flipAxes(code,idxs)`、`buddyReason()`、`luckyReason()`。buddy=`flipAxes(code,[2])`、lucky=`flipAxes(code,[0,1,2,3])`。
- **`buildBondsCard(code,t,isEn)`**（約 line 2667）：分享 Card 2 的 HTML。結構：sc-top → sc2-body（kicker→title→兩格配對→**sc2-strengths 天賦**→sc2-action 雙齊零行動）→ sc-bottom CTA。
- **`canvasFromShareCard(card,fileName)`**：html2canvas 封裝，回傳 `{dataUrl,blob,file,fileName}`。
- **`downloadShareCard()`**：產 Card 1（inline 原 HTML）+ Card 2（buildBondsCard），呼叫 `showImageModal`。
- **`showImageModal({cards,isEn,code})`**：雙卡 modal，每張各自有下載/分享鈕（用 `data-i` 區分）。
- **`renderReadingTabs()` / `switchReadingTab(btn,idx)`**：延伸閱讀 3 分頁（核心讀本／另一種可能／政策論述）。
- **`SFX`** 模組（startQuiz 之前）：IIFE 回傳 `{isMuted,setMuted,tap(i),pop(),pick(),blip(),back(),reveal()}`；另有 `toggleSound()`。
- **intro hero**（約 line 856）：`.intro-hero` > `.intro-hero-text` + `<img class="intro-art" src="pedestrian.png" onerror="this.remove()">`。
- **`.atlas-card`**：在 `renderDemandSection(code)` 之後，地圖成果連結。

**設計 token（`:root`）**：`--lime:#C8D400`、`--lime-dk:#A8B200`、`--coral:#FF6B5B`、`--cream:#FBF7EC`、`--paper:#FFFCF2`、`--black:#1A1A1A`、`--ink:#252525`；字型 `--zh`(Noto Sans TC)、`--en`(Space Grotesk)、`--serif`(DM Serif Display)、`--mono`(JetBrains Mono)。

**16 型代碼**：4 字母 `[pace M/R][route E/H][social C/S][focus Y/I]`。

---

## ⚠️ 6. 重要注意事項（踩過的雷）

- **雙語切換**：靠 `body.zh .en-only{display:none}` / `body.en .zh-only{display:none}`（CSS 約 line 320-321）。`<body>` 必須有 class `zh` 或 `en`。新增雙語內容時用 `.zh-only` / `.en-only` 包。
- **正名**：是「雙**齊**零」不是「雙零」。新增文案別寫回「雙零」。
- **測試別污染試算表**：見第 4 節，務必 stub `logToSheet`。
- **圖片快取雷**：開發時若曾用同檔名 `pedestrian.png` 放過佔位圖，瀏覽器會吃舊快取 → 用 `pedestrian.png?cb=xxx` cache-buster 驗證即可（正式使用者沒有這問題）。
- **`pedestrian.png` 未追蹤**：commit 前一定 `git add`，否則上線會 404（有 `onerror="this.remove()"` 保護，圖會消失但不會壞版）。
- **結果頁是動態 render**：`showResult()` 裡 `setTimeout`（1300ms）才把 HTML 塞進 `#result`。測試要等。
