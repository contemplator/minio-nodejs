# MinIO File Uploader

本專案提供一個簡易的檔案上傳服務，結合 MinIO 物件儲存與 Node.js，並透過 Docker Compose 快速部署。

## 快速開始

### 1. 使用 Docker Compose 啟動 MinIO

請確保已安裝 [Docker](https://www.docker.com/) 與 [Docker Compose](https://docs.docker.com/compose/)。

```bash
docker-compose up -d
```

這會根據 `docker-compose.yml` 啟動 MinIO 服務。

### 2. 設定環境變數

請在專案根目錄建立 `.env` 檔案，內容範例如下：

```env
MINIO_ENDPOINT=localhost
MINIO_PORT=9000
MINIO_ACCESS_KEY=minioadmin
MINIO_SECRET_KEY=minioadmin
MINIO_BUCKET=mybucket
```

`.env` 用於設定 MinIO 連線資訊與預設 bucket 名稱，Node.js 應用程式會讀取這些環境變數。

### 3. 執行 Node.js 檔案上傳程式

確保已安裝 [Node.js](https://nodejs.org/)。

安裝依賴套件：

```bash
npm install
```

執行檔案上傳程式：

```bash
node file-uploader.mjs
```

程式會根據 `.env` 設定，將檔案上傳至 MinIO。

## 目錄結構

```
.
├── docker-compose.yml
├── file-uploader.mjs
├── .env
└── README.md
```
