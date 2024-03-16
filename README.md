# AWS SAM のハンズオン

### 環境設定

-   [Node.js](https://nodejs.org/en)
-   [Docker](https://docs.docker.jp/desktop/install.html)
-   [AWS CLI](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html)
-   [AWS SAM](https://docs.aws.amazon.com/ja_jp/serverless-application-model/latest/developerguide/install-sam-cli.html)

<br/>

### ディレクトリ構成

```bash
aws-sam-handon
│
├── .aws-sam
│   # AWS SAMによってビルドされたアーティファクトやローカルでのテスト環境の構成ファイルが格納されるディレクトリ
│
├── events
│   └── event.json # ローカルでLambda関数をテストする際に使用する、イベントデータが記載されたJSONファイル
│
├── hello-world
│   ├── tests
│   │   └── unit
│   │       └── test-handler.mjs # Lambda関数の単体テストを記述するモジュールファイル
│   │
│   ├── .npmignore # npmがパッケージを作成する際に無視するべきファイルやディレクトリを指定するファイル
│   ├── app.js # Lambda関数の実際の処理を記述するメインのJavaScriptファイル
│   └── package.json # プロジェクトの依存関係やスクリプトなどを管理するnpmの設定ファイル
│
├── .gitignore # Gitバージョン管理から除外するファイルやディレクトリを指定するファイル
├── .prettierrc.json # Prettierコードフォーマッターの設定ファイル
├── README.md # プロジェクトの説明を記述するマークダウンファイル
├── samconfig.toml # SAM CLIの設定を記述するファイル。デプロイコマンドのオプションなどを定義できる
└── template.yaml # SAMテンプレートファイル。プロジェクトのAWSリソースを定義する

```

<br/>

### コマンド

-   初期化

```bash
sam init
```

-   ビルド（ソース更新の都度実行する）

```bash
sam build
```

-   ローカル環境で API エンドポイントの起動

```bash
sam local start-api

# 起動時にすべての関数のコンテナがロードされ、呼び出し間で保持
sam local start-api --warm-containers eager

# 各関数が初めて呼び出される場合に限り、コンテナがロード。その後、追加の呼び出しのために永続化
sam local start-api --warm-containers lazy

```

-   ローカル環境で Lambda 関数の呼び出し

```bash
sam local invoke

# 関数の指定（イベント指定なし）
sam local invoke "HelloWorldFunction" --no-event

# 関数の指定（イベント指定あり）
sam local invoke "HelloWorldFunction" -e events/event.json

# ログをファイルに保存
sam local invoke "HelloWorldFunction" -e events/event.json > result.log
```

<br/>

### 参考資料

[AWS Serverless Application Model （AWS SAM) とは](https://docs.aws.amazon.com/ja_jp/serverless-application-model/latest/developerguide/what-is-sam.html)
