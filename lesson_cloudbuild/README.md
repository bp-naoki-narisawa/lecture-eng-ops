# CloudBuildからCloudRunへのデプロイ

環境変数を設定:
```
IMAGE_NAME=image-hoge # コンテナイメージの名前
SERVICE_NAME=service-hoge # CloudRunへデプロイされるサービス名
```

Cloud Buildを実行:
```
gcloud builds submit --substitutions _IMAGE_NAME=$IMAGE_NAME,_SERVICE_NAME=$SERVICE_NAME
```

デプロイされたサービスへのアクセス
```
SERVICE_URL=$(gcloud run services describe $SERVICE_NAME --format 'value(status.url)' --region us-central1)
curl -H "Authorization: Bearer $(gcloud auth print-identity-token)" $SERVICE_URL
```
