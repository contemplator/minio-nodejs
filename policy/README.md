# MinIO 權限政策

## 建立自定義權限政策

可用於 attach 於 User 

```bash
mc admin policy create myminio android-read-policy ./policy/android-read.json
```

## 為 User 添加權限

```bash
mc admin policy attach myminio android-read-policy --user leo.lin
```

## 建立 Service Account (Access Key) 時同時添加權限

```bash
mc admin accesskey create myminio/ leo.lin --policy ./policy/android-read.json
```