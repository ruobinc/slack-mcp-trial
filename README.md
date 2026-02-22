# slack-mcp-trial
Slack MCP trial


# ローカル
1. Clone this project onto your machine
git clone https://github.com/slack-samples/bolt-js-slack-mcp-server.git

2. 
cd bolt-js-slack-mcp-server

3. SLACK_STATE_SECRET
openssl rand -hex 32

4. 
npm install
npm start

# ngrok
1. ローカルサーバー起動
npm start

2. ngrokトンネル接続
ngrok http 3000


# Slack
https://docs.slack.dev/ai/slack-mcp-server#authentication
## リダイレクトURL
https://kamila-mandibular-delbert.ngrok-free.dev/slack/oauth_redirect
https://chatgpt.com/connector_platform_oauth_redirect
https://platform.openai.com/apps-manage/oauth

## Event Subscriptions
https://kamila-mandibular-delbert.ngrok-free.dev/slack/events


# ChatGPT
MCPサーバーURL: https://mcp.slack.com/mcp
認証: OAuth
OAuth クライアント ID: Slack App の Client ID
OAuth クライアント シークレット: Slack App の Client Secret


# Heroku
1. Herokuアプリ作成
```bash
heroku login
APP_NAME=ruobin-slack-mcp-app
heroku create "$APP_NAME"
```
2. Heroku 環境変数設定（.env をHerokuへ渡す）
```bash
grep -E '^[A-Za-z_][A-Za-z0-9_]*=' ./bolt-js-slack-mcp-server/.env | xargs heroku config:set -a "$APP_NAME"
```

3. デプロイ
```bash
cd ./bolt-js-slack-mcp-server
git remote add heroku "https://git.heroku.com/${APP_NAME}.git"
git push heroku HEAD:main
```

4. 確認
```bash
heroku ps:scale web=1 -a "$APP_NAME"
heroku logs --tail -a "$APP_NAME"
```

5. URL確認
```bash
heroku apps:info -a "$APP_NAME" -s | rg '^web_url=' | cut -d= -f2
```