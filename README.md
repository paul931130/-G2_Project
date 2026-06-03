# 詩境｜生成式 AI 古典詩詞互動系統

「詩境」是一個結合 Gemini API 與 本機唐詩資料庫，讓使用者用作者、篇名、詩句片段或意境描述召喚詩作，並以「詩魂現身」的方式閱讀古典詩詞的網頁。

## 檔案結構

```text
├── index.html              # 網站
├── style.css               # 介面樣式
├── app.js                  # 互動、本機詩庫、TTS 與 API 邏輯
├── poems.json              # 本機詩詞資料
├── README.md               # 專案說明
├── USER_GUIDE.md           # 使用者指南
└── docs/                   # 報告資料
    ├── README.md           # docs資料夾說明
    ├── USER_GUIDE.md       # 使用者指南
    ├── PROJECT_REPORT.md   # 專題報告 Markdown
    └── SOUL.md             # 作者人格設定
```


## 使用方式

1. 開啟網站。
<img width="2528" height="1301" alt="image" src="https://github.com/user-attachments/assets/d59bb710-4407-4318-829f-35e92e0018b0" />

2. 可先不輸入 API Key，直接查詢本機詩庫，例如：`靜夜思`、`石壕吏`、`床前明月光`等資料庫有涵蓋的作品。
<img width="1721" height="1109" alt="image" src="https://github.com/user-attachments/assets/e5f20d61-602c-4e4e-9385-e1fba9340f0b" />

3. 可按「🎲 隨機一首」從本機詩庫抽出作品，不消耗 Gemini API。
<img width="2529" height="1301" alt="image" src="https://github.com/user-attachments/assets/297e6cdd-dee5-4d36-bf80-ff6d94f576bb" />

4. 若要使用 Gemini，點左側 `API KEY`，貼上 key 後會自動輕量測試一次；測試成功後即可使用 AI 分析與詩魂問答。- 輸出內容明確顯示來源：Gemini 或本機詩庫。
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

## v1.2.0 修正重點

- 修正原文白色方框：依詩句長度自動調整高度，短詩不再硬撐，文字置中。
- 修正隨機召喚：隨機詩來源為本機詩庫，但不再覆蓋 Gemini API 連線狀態。
- 修正本機相近推薦：使用本機資料時不再誤顯示 API 未連線。
- 優化手機版導覽列與操作按鈕，降低擋到標題或擠壓內容的機率。
- 啟動時若本分頁已有暫存 API key，先維持已連線狀態，再背景輕量測試。
  
## v1.3.0 修正重點
- 修正本機相近詩詞查無結果提示
