# 詩境｜生成式 AI 古典詩詞互動系統

「詩境」是一個結合 Gemini API 與 本機唐詩資料庫，讓使用者用作者、篇名、詩句片段或意境描述召喚詩作，並以「詩魂現身」的方式閱讀古典詩詞的網頁。

## 檔案結構

```text
├── index.html              # 網站入口
├── style.css               # 介面樣式
├── app.js                  # 互動、本機詩庫、TTS 與 API 邏輯
├── poems.json              # 本機詩詞資料
├── README.md               # 專案說明
├── USER_GUIDE.md           # 使用者指南
├── CHANGELOG.md            # 完整更新紀錄
└── docs/                   # 期末展示與設計文件
    ├── FINAL_REPORT.md      # 期末專題報告
    ├── DEMO_VIDEO_SCRIPT.md # Demo 影片腳本與現場展示流程
    └── SOUL.md              # 詩魂人格與設計原則
```
## 使用方式

1. 開啟網站。
<img width="2528" height="1301" alt="image" src="https://github.com/user-attachments/assets/d59bb710-4407-4318-829f-35e92e0018b0" />

2. 可先不輸入 API Key，直接查詢本機詩庫，例如：`靜夜思`、`石壕吏`、`床前明月光`等資料庫有涵蓋的作品。
<img width="1721" height="1109" alt="image" src="https://github.com/user-attachments/assets/e5f20d61-602c-4e4e-9385-e1fba9340f0b" />

3. 可按「🎲 隨機一首」從本機詩庫抽出作品，不消耗 Gemini API。
<img width="2529" height="1301" alt="image" src="https://github.com/user-attachments/assets/297e6cdd-dee5-4d36-bf80-ff6d94f576bb" />

4. 若要使用 Gemini，點左側 `API KEY`，貼上 key 後會自動輕量測試一次；測試成功後即可使用 AI 分析與詩魂問答。輸出內容會明確顯示來源：Gemini 或本機詩庫。
<img width="972" height="534" alt="image" src="https://github.com/user-attachments/assets/931cf8f5-a607-4565-bf99-c984615ed436" />

5. API 狀態條顯示已連線、僅本機或配額受限。
<img width="323" height="241" alt="image" src="https://github.com/user-attachments/assets/75483810-a8cb-431a-be12-f4c21f4ad253" />
<img width="339" height="220" alt="image" src="https://github.com/user-attachments/assets/f1a1690d-64e6-4f50-a777-9224846bf134" />
<img width="337" height="236" alt="image" src="https://github.com/user-attachments/assets/170d05c0-e255-4acc-addb-29b6c0716a11" />

6. 發生連線錯誤時，提供重試查詢 API、切換 API Key、查詢本機類似詩詞、隨機召喚、返回重新輸入其他內容。
<img width="1716" height="286" alt="image" src="https://github.com/user-attachments/assets/47e34871-e057-4e52-ad91-ab0c1aeb8c63" />


7. 查到詩後，可按「朗讀」使用瀏覽器內建語音朗讀詩文或詩魂自語。
<img width="1621" height="369" alt="image" src="https://github.com/user-attachments/assets/96ebc36a-42be-4acd-b8ee-3d57c76281b2" />
<img width="1621" height="360" alt="image" src="https://github.com/user-attachments/assets/f14bb44e-bf6d-49ff-99a7-935f5ecc9928" />

8. 可切換分析頁籤、向詩魂提問、收藏或複製詩作。
<img width="1866" height="601" alt="image" src="https://github.com/user-attachments/assets/e7be617a-b2d3-4d8f-a6da-3f421f14ef85" />
<img width="1943" height="658" alt="image" src="https://github.com/user-attachments/assets/6ce6fb07-96cc-489e-ab08-56920a1ee271" />
<img width="524" height="661" alt="image" src="https://github.com/user-attachments/assets/cbc4ef47-53d9-4f42-9245-833636bb1556" />

9. 可到「雙魂對話」選兩位詩人，輸入主題後生成對話。
<img width="2491" height="1292" alt="image" src="https://github.com/user-attachments/assets/4c3ae003-845a-4f79-9b2e-b35f9f40629e" />

10. API Key 只存 `sessionStorage`，關閉分頁後清除。
<img width="1745" height="901" alt="image" src="https://github.com/user-attachments/assets/7068900a-9ec3-4dfe-9eed-66ecfb2268e7" />

## 本機詩庫限制

目前 `poems.json` 主要收錄唐詩。本機模式無法查到宋詞或其他朝代作品，例如蘇軾、李清照的部分作品可能需要 Gemini API 才能生成解讀。

## 目前版本：v1.5.0

整合說明重點如下：

- 前端拆分為 `index.html`、`style.css`、`app.js`、`poems.json`，便於 GitHub Pages 部署與後續維護。
- 本機詩庫改為 `poems.json` lazy-load，不輸入 Gemini API Key 也能查詢唐詩。
- 新增隨機召喚、收藏、複製、詩魂問答、雙魂對話與免費瀏覽器朗讀。
- API Key 僅存 `sessionStorage`，關閉分頁後清除，不寫入 GitHub。
- 修正 API 狀態、429 配額冷卻、手機版導覽、詩文白框高度與重複詩藏入口。
- 修正原詩混入「一作／通／又作」等校勘註記的問題，校注會獨立顯示。
- 修正 `poems.json` 快取問題，使用者不需要手動在網址後加版本參數。
- 修正本機詩庫輸出清理，避免「譯文及注釋／注釋／註解／英譯」等原始資料標籤進入「詩魂自述」或「魂歸何處」。
- 補強長篇題序分離，原詩直排區只保留詩句本體。
- 更新 README、USER_GUIDE、CHANGELOG 與 docs 文件，讓發布包內的說明與實際程式一致。
- 
###前面幾輪更新
- **v1.0.0**：初版通靈問詩、詩魂互動、收藏、複製、Gemini API 查詢。
- **v1.1.0**：拆分 `style.css` / `app.js` / `poems.json`，建立本機詩庫 lazy-load 與部署文件。
- **v1.2.0**：修正手機版 UI、詩文白框、API 狀態、隨機召喚與重複詩藏入口；加入免費瀏覽器朗讀。
- **v1.3.0**：改善本機相近作品推薦與錯誤提示流程。
- **v1.4.0**：修正校注／異文混入原詩、`poems.json` 快取與前端資源版本問題。
- **v1.4.1**：修正「詩魂自述」與「魂歸何處」誤顯示譯文標題、注釋標籤與英譯資料的問題。
- **v1.5.0**：補強譯文清理，處理「註解」與 inline 注釋，將長篇題序移出原詩正文，並補齊發布說明文件。

詳細內容請見 `CHANGELOG.md`。

## 期末展示文件

本發布包保留必要的 Week 16 成品展示與反思文件：

- `docs/FINAL_REPORT.md`：期末專題報告
- `docs/DEMO_VIDEO_SCRIPT.md`：Demo 影片腳本與現場展示流程
- `docs/SOUL.md`：詩魂人格與設計原則
- `CHANGELOG.md`：完整更版紀錄
