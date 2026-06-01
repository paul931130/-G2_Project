# 詩境｜生成式 AI 古典詩詞互動系統

> 以生成式 AI 與本機詩庫為核心，打造可查詢、可解析、可對話、可收藏的古典詩詞互動網站。

## 專案概述

**詩境**是一個古典詩詞互動學習網頁。使用者可以輸入詩名、作者、詩句片段或意境描述，系統會回傳相關詩作，並提供詩文原文、白話釋義、情緒分析、創作背景與詩人角色互動。

本專案的目標不是單純讓 AI 產生文字，而是將生成式 AI 應用在古典詩詞理解流程中，改善傳統詩詞學習常見的問題：

- 只背誦詩句，卻不理解詩意。
- 只看白話翻譯，缺少情緒與歷史脈絡。
- 學習過程單向，缺乏互動與沉浸感。
- AI 服務不穩時，系統容易完全失效。

因此，本專案採用 **本機詩庫 + Gemini API** 的混合架構。沒有 API Key 時可使用本機詩庫；輸入 API Key 後可啟用生成式 AI 解析與詩人對話功能。

---

## 線上展示

若已部署 GitHub Pages，可將網址填在這裡：

```text
https://你的GitHub帳號.github.io/你的repo名稱/
```

---

## 主要功能

### 1. 通靈問詩

使用者可以輸入：

- 詩名，例如：`靜夜思`
- 作者，例如：`李白`
- 詩句片段，例如：`床前明月光`
- 意境描述，例如：`思鄉的詩`、`邊塞悲壯`

系統會回傳詩作內容與分析結果。

### 2. 本機詩庫 Lazy-load

大型詩庫已從 HTML 中拆出，獨立存放於：

```text
poems.json
```

系統只有在需要查詢本機詩庫時，才會載入 `poems.json`，避免 HTML 檔案過大，也方便後續維護資料。

目前本機詩庫約收錄 **315 首詩作**。

### 3. Gemini AI 解析

使用者可自行輸入 Gemini API Key，啟用：

- 自然語言查詢
- 詩詞語意解析
- 情緒分析
- 詩人角色對話
- 雙詩人主題對話

公開版本不內建任何 API Key。

### 4. 詩人角色對話

查詢詩作後，使用者可以向詩人角色提問，例如：

```text
這首詩是在什麼心情下寫的？
```

AI 會以接近該詩人風格的語氣回應。

### 5. 雙魂對話

使用者可以選擇兩位詩人，並指定一個主題，讓兩位詩人展開對話。

範例：

```text
李白 × 蘇軾
主題：月亮
```

### 6. 詩藏功能

使用者可以收藏喜歡的詩作。收藏資料儲存在瀏覽器 `localStorage` 中，不會上傳到伺服器。

---

## 專案結構

```text
shijing-poem-ai/
├── index.html        # 主網頁
├── poems.json        # 本機詩庫資料
├── README.md         # 專案說明文件
├── USER_GUIDE.md     # 使用者指南
└── CHECKSUMS.txt     # 檔案完整性校驗
```

> `index.html` 和 `poems.json` 必須位於同一層，否則本機詩庫無法正確載入。

---

## 使用方式

### 本機執行

請不要直接雙擊 `index.html`，因為瀏覽器可能會限制本機檔案讀取，導致 `poems.json` 無法載入。

建議使用簡易伺服器：

```bash
python -m http.server 8000
```

然後打開：

```text
http://localhost:8000
```

### 部署到 GitHub Pages

1. 建立 GitHub Repository。
2. 上傳以下檔案到 repo 根目錄：

```text
index.html
poems.json
README.md
USER_GUIDE.md
CHECKSUMS.txt
```

3. 到 `Settings → Pages`。
4. 設定：

```text
Source: Deploy from a branch
Branch: main
Folder: /root
```

5. 儲存後等待 GitHub Pages 部署完成。

---

## 技術架構

本專案採用純前端靜態網站架構：

- HTML
- CSS
- JavaScript
- JSON 本機資料庫
- Gemini API
- localStorage
- sessionStorage
- GitHub Pages / Netlify 靜態部署

### 資料流程

```text
使用者輸入
   ↓
判斷是否使用 Gemini API
   ↓
有 API Key → Gemini 生成解析
沒有 API Key / API 失敗 → 本機詩庫查詢
   ↓
畫面渲染詩文、翻譯、賞析與互動內容
   ↓
使用者可收藏或進一步對話
```

---

## 安全性設計

本專案公開版不內建 API Key。

目前設計：

- Gemini API Key 由使用者自行輸入。
- API Key 暫存在 `sessionStorage`。
- 關閉分頁後，API Key 會自動清除。
- 收藏資料只存於使用者瀏覽器 `localStorage`。
- 無登入功能。
- 無後端資料庫。
- 不蒐集個人資料。

發布前建議檢查：

```text
確認 index.html 內沒有 AIza
確認 poems.json 內沒有 API Key 或私人資料
確認資料夾內沒有 .env、密碼筆記或舊版 HTML
```

---

## 測試建議

部署後可測試以下輸入：

```text
靜夜思
李白
王維
床前明月光
思鄉的詩
邊塞悲壯
```

也可以測試：

- 不輸入 API Key 時，本機詩庫是否能正常查詢。
- 輸入 API Key 後，AI 解析是否能正常回覆。
- 收藏後重新整理，詩藏是否保留。
- 手機版導覽列是否正常顯示。

---

## 限制與未來改進

目前版本仍屬前端 MVP，後續可改進：

- 加入後端 Proxy，避免前端直接呼叫 Gemini API。
- 增加詩庫搜尋索引，提高大量資料查詢效率。
- 新增主題分類與標籤篩選。
- 加入更多詩詞資料來源與版本比對。
- 提供學習紀錄或測驗模式。
- 增加引用來源與文獻標註。

---

## 使用者指南

一般使用者可參考：

```text
USER_GUIDE.md
```

---

## 作者

本專案為生成式 AI 課程專題作品。
