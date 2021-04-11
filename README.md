# AWS Cost Report Notification To Teams
## Overview
毎日AM 9:00(JST)に前日までで発生した当月のAWS使用料(現在ap-northeast-1のみ)をTeams Incoming Webhookに通知する

## Get Started

### 1.Teams Incoming Webhookを追加
[任意のTeamsチャネルにIncoming Webhookを追加](https://docs.microsoft.com/ja-jp/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook#add-an-incoming-webhook-to-a-teams-channel)

### 2.いずれかの方法でアプリケーションをデプロイ
1. AWS Serverless Application Repositoryでデプロイ (推奨)
* [アプリケーションページ](https://ap-northeast-1.console.aws.amazon.com/lambda/home#/create/app?applicationId=arn:aws:serverlessrepo:ap-northeast-1:521635626865:applications/costreport-notification-to-teams) から
* TeamsHookUrl に Teams Incoming Webhookを作成 で作成されたWebhookのURLをペーストして デプロイ を押す

2. AWS CloudFormationからデプロイ
* [GitHub](https://github.com/mihoshima278/costreport-notification-to-teams) から最新の packaged.yaml を入手

* CloudFormationスタックを作成

```bash
aws cloudformation deploy \
  --template-file packaged.yaml \
  --stack-name <<<YOUR STACK NAME>>> \
  --parameter-overrides TeamsHookUrl=<<<YOUR TEAMS INCOMING WEBHOOK URL>>> \
  --capabilities CAPABILITY_IAM
```

### 3.テストイベントを発行し、Teamsへの通知を確認する
1. スケジューリングされた時刻を待たなくても、Lambdaでテストイベントを実行することで通知が確認可
* [以下のページ](https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/getting-started-create-function.html)における**Lambda 関数を呼び出す**を参照

## Uninstall
CloudFormationスタックを削除

## License
[LICENSE](./LICENSE)を参照
