# SAM Demo for CodePipeline

CodePipelineでデプロイするSAMアプリケーションのデモです。

## 構成

- **Lambda関数**: Python 3.13でGET/POSTリクエストを処理
- **API Gateway**: RESTful API（GET /items, POST /items）+ APIキー認証
- **DynamoDB**: シンプルなテーブル（id, name, description）
- **CodeDeploy**: Canary10Percent5Minutesでデプロイ

## ローカルデプロイ

```bash
# ビルド
sam build

# デプロイ
sam deploy --guided
```

## CodePipelineセットアップ

1. S3バケットを作成（アーティファクト用）
2. CodePipelineを設定
3. ソースをGitHub/CodeCommitに配置
4. buildspec.ymlのBUCKET_NAME環境変数を設定

## API使用例

```bash
# APIキー取得
aws apigateway get-api-key --api-key [API_KEY_ID] --include-value

# アイテム一覧取得
curl -H "x-api-key: [API_KEY_VALUE]" \
  https://[API_ID].execute-api.[REGION].amazonaws.com/Prod/items

# アイテム作成
curl -X POST https://[API_ID].execute-api.[REGION].amazonaws.com/Prod/items \
  -H "Content-Type: application/json" \
  -H "x-api-key: [API_KEY_VALUE]" \
  -d '{"name": "Sample Item", "description": "This is a sample item"}'
```

## ファイル構成

```
.
├── template.yaml      # SAMテンプレート
├── buildspec.yml      # CodeBuild設定
├── src/
│   └── app.py        # Lambda関数
└── README.md         # このファイル
```