# 🌍 TravelTime 等時圈產生器

![WebGIS](https://img.shields.io/badge/Category-WebGIS-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Vanilla JS](https://img.shields.io/badge/Frontend-Vanilla%20JS-orange.svg)
![TailwindCSS](https://img.shields.io/badge/Style-Tailwind%20CSS-38bdf8.svg)

一個完全基於網頁前端（Client-side）技術打造的 **TravelTime API 批次等時圈處理工具**。使用者只需準備包含座標的 CSV 檔案，即可在瀏覽器內一鍵批次直擊 TravelTime API 獲取等時圈，並自動打包下載為標準的 GeoJSON 格式，無須安裝任何後端環境或 Python 套件。

## ✨ 核心特色

- 🎯 **直擊座標與格式自動校正**：自動清理 CSV 欄位空格、轉換大小寫，完美相容 `id`, `x`, `y` 圖資欄位。
- 🛡️ **資安零風險 (Client-Side Only)**：所有資料處理、時戳轉換與 Blob 檔案封裝皆在使用者瀏覽器記憶體內完成，絕不上傳至任何第三方伺服器。
- 🚀 **完全擺脫 SDK 攔截**：捨棄官方特定語言 SDK，改用最純粹的原生 `fetch` 協定，完美避開特定企業網路環境下的本機 Proxy 阻擋與 SSL 憑證校驗錯誤。
- 🐢 **防爆流量自適應避讓機制 (429 Anti-Throttle)**：
  - 內建線性冷卻機制（每筆請求成功後溫和休息 2 秒）。
  - 若遭遇伺服器 `HTTP 429` 流量限制，系統將**自動原地暫停 65 秒**並於冷卻後自動重試該點位，確保大批次任務能穩健跑完。
- 📊 **多邊形屬性注入 (Property Injection)**：產出的 GeoJSON 內部動態注入了點位 `location_id` 與時間範圍 `time_minutes`，方便後續直接導入 **QGIS、ArcGIS 或 Leaflet.js** 進行 Table Join 與樣式渲染。
- 📥 **防亂碼範例下載**：內建 UTF-8 BOM 編碼的範例 CSV 下載功能，確保同仁使用 Excel 開啟時中文絕不產生亂碼。

---

## 🚀 快速開始 (Quick Start)

本專案已支援 **GitHub Pages** 佈署，您可以直接雙擊本地的 `index.html` 或透過線上網址開啟。

### 使用步驟

1. **取得 API 金鑰**：請先至 [TravelTime 官網](https://traveltime.com/) 註冊並獲取您的 `Application ID` 與 `API Key`。
2. **準備圖資檔案**：點擊介面上的 **「📥 下載範例 CSV 檔案」** 獲取標準範本。請確保您的 CSV 欄位包含：
   - `id`：點位識別碼（如：台北車站、1、A-01）
   - `x`：經度 (Longitude)
   - `y`：緯度 (Latitude)
3. **設定參數**：輸入金鑰、等時圈範圍（分鐘）與交通工具（步行、開車、大眾運輸、自行車）。
4. **開始執行**：上傳 CSV 後點擊「開始產生」，並可在右側主控台即時觀看 **Live Logs 對帳表**。
5. **打包下載**：任務完成後，點擊綠色按鈕即可獲取 `output_isochrones.geojson`。若有失敗點位，亦可單獨下載失敗清單。

---

## 📂 CSV 檔案格式範例

```csv
id,x,y
台北車站,121.5170,25.0478
台北101,121.5644,25.0339
板橋車站,121.4626,25.0130
