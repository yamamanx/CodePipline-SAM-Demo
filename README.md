# SAM Demo for CodePipeline

CodePipelineでデプロイするSAMアプリケーションのデモです。

## 構成

- **Lambda関数**: Python 3.9でGET/POSTリクエストを処理
- **API Gateway**: RESTful API（GET /items, POST /items）
- **DynamoDB**: シンプルなテーブル（id, name, description）
- **CodeDeploy**: Canary10Percent5Minutesでデプロイ

## デプロイ

1. S3バケットを作成（CodePipelineのアーティファクト用）
2. CodePipelineを設定
3. ソースをGitHubまたはCodeCommitに配置

## API使用例

```bash
# アイテム一覧取得
curl https://your-api-id.execute-api.region.amazonaws.com/Prod/items

# アイテム作成
curl -X POST https://your-api-id.execute-api.region.amazonaws.com/Prod/items \
  -H "Content-Type: application/json" \
  -d '{"name": "Sample Item", "description": "This is a sample item"}'
```