# serverless + auth0 + aws 写経

このリポジトリは serverless + auth0 + aws　の写経です。
以下ページを参考に、動くプログラムを作りました。

https://www.serverless.com/examples/aws-node-auth0-custom-authorizers-api

## 前提条件

### 必須アカウント

以下アカウントを用意する

* AWS
* auth0

### 必須ソフト
以下ソフトが開発環境にインストールされていること

* node.js(v16.5.0以上)
* npm(7.19.1以上)
* yarn(1.22.10以上)  
* serverless
  * Framework Core: 2.52.1
  * Plugin: 5.4.3
  * SDK: 4.2.5
  * Components: 3.14.0

### serverless cli AWS設定
以下サイトを参考に、serverless cliのAWS設定を完了させる。

https://www.serverless.com/framework/docs/providers/aws/guide/credentials/

### auth0 開発環境URL登録
auth0アプリケーション設定の以下項目に```http://localhost:8080```を追加する

* Allowed Callback URLs
* Allowed Logout URLs
* Allowed Web Origins

### auth0 PEMファイルの入手
auth0が提供するPEMファイルを入手する。
例えば、以下サイトからPEMをダウンロードすることができる。

https://auth0.com/docs/config/tenant-settings/signing-keys#how-it-works

## 動かし方

### 初回

```shell
cd <本リポジトリをcloneした場所>
yarn install


cp secrets.example.json secrets.json
# 各種プロパティに環境に応じた値をセットする
vim secrets.json
cp <auth0PEMファイル> public_key
sls deploy

cp frontend/config.template.js frontend/config.js
# 各種変数に環境に応じた値をセットする
vim frontend/config.js


yarn start
# ブラウザでhttp://localhost:8080を開く
```

### 2回目以降

```shell
cd <本リポジトリをcloneした場所>
yarn start
```