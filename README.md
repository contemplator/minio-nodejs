# MinIO File Uploader

本專案提供一個簡易的檔案上傳服務，結合 MinIO 物件儲存與 Node.js，並透過 Docker Compose 快速部署。

## 快速開始

### 1. 使用 Docker Compose 啟動 MinIO

請確保已安裝 [Docker](https://www.docker.com/) 與 [Docker Compose](https://docs.docker.com/compose/)。

```bash
docker-compose up -d
```

這會根據 `docker-compose.yml` 啟動 MinIO 服務。

### 2. 登入 MinIO 以及設定使用者與權限

瀏覽器登入 Console 頁面：

啟動 MinIO 後，可透過瀏覽器進入 [http://localhost:9000](http://localhost:9000/)，使用預設帳號 `minioadmin` / `minioadmin` 登入管理介面。

透過 mc cli 設定使用者及權限：

1. 安裝 MinIO Client (mc)：
    ```bash
    brew install minio/stable/mc
    ```

2. 設定 MinIO 連線別名：
    ```bash
    mc alias set myminio http://localhost:9000 minioadmin minioadmin
    ```

3. 新增使用者（例如：leo.lin）：
    ```bash
    mc admin user add myminio leo.lin password
    ```

4. 檢查可用的權限政策（policy）：
    ```bash
    mc admin policy list myminio
    mc admin policy info myminio readonly
    ```

5. 將 `readwrite` 權限政策指派給新使用者：
    ```bash
    mc admin policy attach myminio readwrite --user=leo.lin
    ```

### 3. 設定 Nodejs 環境變數

請在專案根目錄建立 `.env` 檔案，內容範例如下：

```env
MINIO_ENDPOINT=localhost
MINIO_PORT=9000
MINIO_ACCESS_KEY=minioadmin
MINIO_SECRET_KEY=minioadmin
MINIO_BUCKET=mybucket
```

`MINIO_ENDPOINT` 和 `MINIO_PORT` 視你 Docker 設定為準，預設就是 `localhost` 和 `9000`

`MINIO_ACCESS_KEY` 就是 minIO 登入的帳號，也就是範例中的 `leo.lin`

`MINIO_SECRET_KEY` 就是 minIO 登入的密碼，也就是範例中的 `password`

`MINIO_BUCKET` 就是登入 minIO Console 網頁後增加的 Bucket 名稱

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
