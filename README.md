# 街道靈魂測驗 · Street Soul Quiz

> A 16-personality quiz that helps people see how their everyday relationship with streets connects to a broader transportation transformation agenda.
> 一場關於你、街道、與這座城市的測驗。

[![Live](https://img.shields.io/badge/Live-streetsoul.tw-C8D400?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-1A1A1A?style=flat-square)](LICENSE)
[![VZT](https://img.shields.io/badge/Vision%20Zero%20Taiwan-2026-1A1A1A?style=flat-square)](https://visionzero.tw)
[![TCAN](https://img.shields.io/badge/TCAN-Climate%20Action-1A1A1A?style=flat-square)](#)

---

## 🚦 這是什麼

一個用「16 型人格測驗」包裝的交通倡議互動網頁。透過 12 道題目，把使用者分入 16 種「街道靈魂」，並對應到《雙零交通願景自治條例》的五大訴求。

每個人都有自己跟街道的關係 — 我們希望讓那份關係，成為改變的起點。

由 **Vision Zero Taiwan（還路於民行人路權促進會）** 與 **TCAN（台灣氣候行動網路）** 共同推出，作為 2026 地方選舉政策倡議的一環。

---

## 🌐 線上體驗

- **測驗網站**：[https://你的網域/](#) ← 部署後填入
- **統計儀表板**：[https://你的網域/dashboard.html](#)
- **嵌入版本**：`/dashboard.html?embed=1`（可用 iframe 嵌入）

---

## 📂 檔案結構

```
.
├── index.html          # 測驗主網頁
├── dashboard.html      # 即時統計儀表板（讀 Google Sheet CSV）
├── README.md           # 本文件
├── LICENSE             # CC BY-SA 4.0
└── .nojekyll           # GitHub Pages 設定（避免 Jekyll 處理）
```

---

## 🛠️ 技術概覽

純前端網頁，無建構流程、無 npm 依賴：

- **HTML / CSS / Vanilla JS** — 無框架，2 秒內載入
- **html2canvas** — 結果頁產生 IG 比例分享圖卡（CDN 引入）
- **Google Apps Script** — 接收測驗結果，寫入 Google Sheet（fire-and-forget webhook）
- **Google Sheet CSV** — 儀表板資料源，每 60 秒自動更新

整個系統的後端就是一份 Google 試算表。便宜、簡單、可審視。

---

## 🚀 部署

任何靜態網頁主機都能跑，包含：

- **GitHub Pages**（本 repo 預設）
- Netlify / Vercel / Cloudflare Pages
- 自家網站 / 任何能放 HTML 的地方

部署前需設定兩個變數：

1. **`SHEET_WEBHOOK_URL`**（在 `index.html`）— Google Apps Script 部署的 webhook URL
2. **`SHEET_CSV_URL`**（在 `dashboard.html`）— Google Sheet 發佈成 CSV 的 URL

完整設定教學請洽專案維護者。

---

## 🧑‍🎨 16 型街道靈魂

| Code | 動物 | 中文名 | English |
|------|------|-------|---------|
| MECY | 🦉 | 城市觀察家 | The Urban Observer |
| MECI | 🐱 | 街角分享家 | The Corner Connector |
| MESY | 🐢 | 漫遊思考者 | The Wandering Thinker |
| MESI | 🦋 | 散步詩人 | The Stroll Poet |
| MHCY | 🐶 | 鄰里大使 | The Neighborhood Ambassador |
| MHCI | 🐰 | 早市好朋友 | The Market Mingler |
| MHSY | 🐼 | 街道守護者 | The Street Steward |
| MHSI | 🦔 | 黃昏散步家 | The Twilight Stroller |
| RECY | 🦊 | 通勤革新者 | The Commute Innovator |
| RECI | 🐬 | 城市衝浪者 | The City Surfer |
| RESY | 🦅 | 路線設計師 | The Route Architect |
| RESI | 🐎 | 自由騎士 | The Free Rider |
| RHCY | 🐘 | 大眾運輸推手 | The Transit Advocate |
| RHCI | 🐝 | 通勤好夥伴 | The Commute Companion |
| RHSY | 🐜 | 高效規劃師 | The Efficiency Designer |
| RHSI | 🦝 | 通勤忍者 | The Commute Ninja |

---

## 🤝 共同行動

歡迎其他倡議團體 fork、改寫、本地化使用。如果你也想做類似的測驗、用同套設計系統，請聯繫 VZT。

學術引用：
> Vision Zero Taiwan × TCAN (2026). *Street Soul Quiz: A 16-Personality Survey for Urban Mobility Advocacy*. Taipei, Taiwan.

---

## 📜 授權

本專案採 **CC BY-SA 4.0**（創用 CC 姓名標示 — 相同方式分享 4.0 國際）授權。

你可以自由地：
- **分享** — 以任何媒介或格式重製及散布本素材
- **修改** — 重混、轉換並依本素材建立新作品（包括商業性使用）

惟需遵守：
- **姓名標示** — 標示原作者與授權條款
- **相同方式分享** — 改作品需採用相同授權

---

## 🌿 由誰製作

- **發起**：Vision Zero Taiwan（社團法人還路於民行人路權促進會）
- **發起**：TCAN（台灣氣候行動網路）
- **整理製作**：Yun Ching Wu

街道安全 ✦ 氣候行動 ✦ 一起來

— V1.0 · May 2026
