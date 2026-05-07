# 股票估值 App — 安裝說明

## 檔案清單
```
stockapp/
├── index.html        ← 主程式（所有功能都在這裡）
├── manifest.json     ← PWA 設定
├── sw.js             ← 離線快取
├── icons/
│   ├── icon-192.png  ← App 圖示（小）
│   └── icon-512.png  ← App 圖示（大）
└── README.md
```

---

## 第一步：取得 Finnhub API Key（免費，2分鐘）

1. 前往 https://finnhub.io
2. 點右上角 **Get free API key**
3. 用 Email 註冊（不需信用卡）
4. 登入後在 Dashboard 複製你的 API Key（格式類似 `d1abc2xyz3efg456`）

---

## 第二步：填入 API Key

打開 `index.html`，找到第 9 行：

```javascript
const FINNHUB_KEY = 'YOUR_KEY_HERE';
```

把 `YOUR_KEY_HERE` 換成你的 Key：

```javascript
const FINNHUB_KEY = 'd1abc2xyz3efg456';  // 你的真實 Key
```

---

## 第三步：上傳到 GitHub Pages（免費主機）

### 3-1 建立 GitHub 帳號
前往 https://github.com 免費註冊

### 3-2 建立新 Repository
1. 登入後點右上角「+」→「New repository」
2. Repository name 填：`stockapp`
3. 勾選「Public」
4. 點「Create repository」

### 3-3 上傳檔案
1. 點頁面中的「uploading an existing file」
2. 把整個 stockapp 資料夾內的**所有檔案**拖進去
   （index.html、manifest.json、sw.js、icons 資料夾）
3. 點「Commit changes」

### 3-4 開啟 GitHub Pages
1. 進入你的 Repository → 點上方「Settings」
2. 左側選「Pages」
3. Source 選「Deploy from a branch」
4. Branch 選「main」，資料夾選「/ (root)」
5. 點「Save」

等 1~2 分鐘，你的網址會是：
```
https://你的GitHub帳號.github.io/stockapp
```

---

## 第四步：加到 iPhone 主畫面

1. 用 iPhone 的 **Safari**（必須是 Safari，Chrome 不支援 PWA）打開你的網址
2. 點下方分享按鈕（方形加箭頭的圖示）
3. 選「加入主畫面」
4. 名稱保持「股票估值」，點「新增」
5. 完成！主畫面會出現 App 圖示

---

## 功能說明

| 功能 | 說明 |
|------|------|
| 即時股價 | Finnhub API，每分鐘更新一次 |
| 即時匯率 | USD/TWD 自動抓取，美股一律換算台幣 |
| 公司選擇 | NVIDIA、TSM ADR、台積電、聯發科、群聯 |
| 對比模式 | 同時顯示兩家公司並排比較 |
| PE 目標股價表 | PE 10/15/18/20/25/28/30 保守估算 |
| 計算機 | EPS + PE 滑桿即時算目標股價 |
| 離線模式 | 無網路時仍可查看上次資料 |

---

## 注意事項

- Finnhub 免費版：美股即時、台股延遲 15 分鐘
- 免費 API 每分鐘 60 次請求，個人使用完全夠用
- 所有 EPS 預估數字為法人共識保守版，僅供參考
- **本工具不構成任何投資建議**

---

## 之後要更新資料怎麼做？

在 `index.html` 裡找到 `COMPANIES` 物件，直接修改數字即可，然後重新上傳到 GitHub，網頁會自動更新。

例如更新群聯的保守 EPS：
```javascript
PHISON: {
  ...
  eps2026_bear: 68,  // 改成你要的數字
  ...
}
```
