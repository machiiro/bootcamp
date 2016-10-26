# インストール

## インストール

ダウンロードページより、play 1.2 系の最新バージョンの zip をダウンロードします。
https://www.playframework.com/download#older-versions

ダウンロード後、お好きなディレクトリに zip ファイルを展開します。
ここでは `~/dev/play/1.2.7` に展開した前提で進めます。

展開したディレクトリに移動し、`play` コマンドを実行できればインストール完了です。
play コマンドは良く利用するので、OS ユーザーの実行パスに通しておくと良いです。

```
$ cd ~/dev/play/1.2.7
# ./play
~        _            _
~  _ __ | | __ _ _  _| |
~ | '_ \| |/ _' | || |_|
~ |  __/|_|\____|\__ (_)
~ |_|            |__/
~
~ play! 1.2.7.2, http://www.playframework.org
~
~ Usage: play cmd [app_path] [--options]
~
~ with,  new      Create a new application
~        run      Run the application in the current shell
~        help     Show play help
~
```

## play コマンド

ここでは代表的な play コマンドを紹介します。

なお、アプリケーションに作用するコマンドは、アプリケーションのディレクトリ直下か、引数にパスを指定する必要があります。

```
# プロジェクトのディレクトリ
$ play run
~        _            _
~  _ __ | | __ _ _  _| |
~ | '_ \| |/ _' | || |_|
~ |  __/|_|\____|\__ (_)
~ |_|            |__/
~
~ play! 1.2.7.2, http://www.playframework.org
~
~ Oops. conf/routes or conf/application.conf missing.
~ /path-to-path/xxx does not seem to host a valid application.
~

$ play run /path-to-path/your-application
~        _            _
~  _ __ | | __ _ _  _| |
~ | '_ \| |/ _' | || |_|
~ |  __/|_|\____|\__ (_)
~ |_|            |__/
~
~ play! 1.2.7.2, http://www.playframework.org
~

...

```

### 基本

| コマンド | 説明 |
| --- | --- |
| play help | ヘルプを表示する |
| play version | Play! のバージョンを表示する |

### アプリケーション作成

| コマンド | 説明 |
| --- | --- |
| play new {アプリケーション名} | アプリケーションの雛形を作成する |
| play dependencies | アプリケーションの依存設定を読み込み、依存ライブラリをインストールする |
| play eclipsify | アプリケーションを Eclipse プロジェクトに変換する |
| play idealize | アプリケーションを IntelliJ IDEA プロジェクトに変換する |

### モジュール操作

| コマンド | 説明 |
| --- | --- |
| play install {モジュール名} | モジュールをインストールする |
| play list-modules | Play! モジュールの一覧を表示する |
| play modules | アプリケーションが依存しているモジュールの一覧を表示する |

### 起動・停止

| コマンド | 説明 |
| --- | --- |
| play precompile | アプリケーションのソースをコンパイルする |
| play run | アプリケーションを起動する |
| play start | アプリケーションをバックグラウンドで起動する |
| play stop | アプリケーションを停止する |
| play restart | アプリケーションを再起動する |
| play status | アプリケーションの稼働状況、JVM設定、スレッド等詳細情報を表示する |
