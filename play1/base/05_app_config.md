# アプリケーション設定

Play! の設定は依存関係を除き、全て `conf/application.conf` に記述されます。

## 環境毎の設定切り替え

アプリケーションの設定をローカル・テスト環境・本番環境とで設定内容を切り替えたい場合、Play! ではフレームワークIDを利用します。

フレームワークIDは `play id` コマンド、または `play run --%xxx` コマンドで指定することが可能です。
指定されたフレームワークIDをプレフィックスとして利用することで、環境毎に設定を切り替えることが出来ます。

```
# フレームワークIDが未指定 = ローカル環境では dev モードで動作する
application.mode = dev
# play run --%prod で起動している本番環境では prod モードで動作する
%prod.application.mode = prod
```

フレームワークIDを利用して、application.conf を環境毎に編集することが無いようにしましょう。

## 代表的な項目

### 基本設定

```
# アプリケーション名
application.name=play-tutorial

# モード、dev の場合はスレッド1本・動的コンパイルで動作する
application.mode=dev

# ポート番号
http.port=9000

# ログレベル
application.log=INFO

# JDK バージョン
java.source=1.7
```

## DB設定

```
# DB 接続文字列、db=mem とするとインメモリDBとして動作する
db=mysql://user:pwd@host/database

# DBコネクションプール設定
db.pool.timeout=1000
db.pool.maxSize=30
db.pool.minSize=10

# デバッグ用にSQLを出力するかどうか
jpa.debugSQL=true
```
