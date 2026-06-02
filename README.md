# 詩境｜生成式 AI 古典詩詞互動系統

「詩境」是一個純靜態網頁作品，結合本機唐詩資料庫與 Gemini API，讓使用者用作者、篇名、詩句片段或意境描述召喚詩作，並以「詩魂現身」的方式閱讀古典詩詞。

## 線上展示

部署到 GitHub Pages 後，網址通常會是：

https://paul931130.github.io/-shijing/

如果 repository 名稱不同，請將網址最後的 `-shijing` 改成實際 repo 名稱。

## 專案特色

- 本機 `poems.json` 優先查詢，減少 API 消耗。
- Gemini API 可補足意境式查詢與詩魂問答。
- API Key 只存 `sessionStorage`，關閉分頁後清除。
- 明確顯示來源：Gemini 或本機詩庫。
- API 狀態條顯示已連線、僅本機或配額受限。
- 錯誤卡提供重試 API、切換 API Key、推薦本機類似文章。
- 支援收藏詩作與複製詩作。
- CSS/JS 已拆分，適合 GitHub Pages 靜態部署。

## 檔案結構

```
-shijing/
├── index.html              # 網站入口
├── style.css               # 介面樣式
├── app.js                  # 互動與 API 邏輯
├── poems.json              # 本機詩詞資料
├── README.md               # 專案說明
├── CHECKSUMS.txt           # 發布檔案 SHA-256
└── docs/
    ├── USER_GUIDE.md       # 使用者指南
    ├── PROJECT_REPORT.md   # 課程專案報告 Markdown
    └── SOUL.md             # 作品人格與設計原則
```
## 文件導覽

- [使用者指南](docs/USER_GUIDE.md)
- [專題報告 Markdown](docs/PROJECT_REPORT.md)
- [作品人格與設計原則](docs/SOUL.md)


## 使用方式

1. 開啟網站。
2. 可先不輸入 API Key，直接查詢本機詩庫，例如：`靜夜思`、`石壕吏`、`床前明月光`。
3. 若要使用 Gemini，點左側 `API KEY`，貼上 key 後系統會自動測試。
4. 查到詩後可切換分析頁籤、向詩魂提問、收藏或複製詩作。
5. 可到「雙魂對話」選兩位詩人，輸入主題後生成對話。

## 本機詩庫限制

目前 `poems.json` 主要收錄唐詩。本機模式不一定能查到宋詞或其他朝代作品，例如蘇軾、李清照的部分作品可能需要 Gemini API 才能生成解讀。

## API Key 安全

本專案不會把 API Key 寫進程式碼，也不會保存到長期 `localStorage`。Key 只暫存在目前分頁的 `sessionStorage`，關閉分頁後即清除。

注意：這仍是前端直連 API 的展示型做法，適合課程展示與個人使用。若要公開給大量使用者，建議改成後端代理服務，避免 key 暴露與配額濫用。

## 本機測試

在專案資料夾執行：

```bash
python -m http.server 8000
```

然後開啟：

```
http://localhost:8000/
```

建議測試輸入：

- `靜夜思`
- `石壕吏`
- `床前明月光`
- `邊塞悲壯`

## 發布到 GitHub Pages

1. 建立 GitHub repository。
2. 上傳本資料夾所有檔案。
3. 到 repository 的 Settings → Pages。
4. Source 選 `Deploy from a branch`。
5. Branch 選 `main`，資料夾選 `/root`。
6. 等待 GitHub 產生公開網址。

## 技術架構

- HTML：頁面結構
- CSS：古典紙本視覺、直排詩文、響應式版面
- JavaScript：本機詩庫查詢、Gemini API、收藏、互動狀態
- Gemini 2.5 Flash：意境式查詢、詩魂問答、雙魂對話
- GitHub Pages：靜態網站部署

## 測試檢查

- `node --check app.js`
- 確認 `index.html` 不含硬編碼 API Key
- 確認 `poems.json` 可解析且筆數約 315
- 手機寬度檢查導覽列、輸入區、詩文卡片與按鈕是否重疊
