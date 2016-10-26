# プロセス管理

## ps - 実行中のプロセスを確認する

```bash
# ユーザーが実行したプロセスを確認する
$ ps

# 全ユーザーが実行したプロセスを確認する
$ ps a

# デーモンプロセスを含めて確認する
$ ps ax

# プロセスの実行ユーザーを表示する
$ ps aux

# あるプロセスが実行されているかどうか確認する
$ ps aux | grep java
```

## kill - プロセスを終了する

```bash
# ps コマンド等でプロセスの ID (PID) を確認する
$ ps aux

# PID を指定し、プロセスを正常終了させる
$ kill {PID}

# 正常終了しない場合に、強制終了させる
$ kill -KILL {PID}
```

## service - サービスの起動・停止を行う

サービス名は起動スクリプトのファイル名と一致します。
起動スクリプトは `/etc/init.d` 以下に配置されています。

```bash
# サービスを起動する
$ service {サービス名} start

# サービスを停止する
$ service {サービス名} stop

# サービスを再起動する
$ service {サービス名} restart
```

## chkconfig - サービスの自動起動設定を行う

```bash
# 現在の自動起動設定を確認する
# 0 〜 6 の数字はランレベルを表す、通常は 3 で起動している
$ chkconfig
acpid          	0:off	1:off	2:on	3:on	4:on	5:on	6:off
atd            	0:off	1:off	2:off	3:on	4:on	5:on	6:off
auditd         	0:off	1:off	2:on	3:on	4:on	5:on	6:off
blk-availability	0:off	1:on	2:on	3:on	4:on	5:on	6:off
cgconfig       	0:off	1:off	2:off	3:off	4:off	5:off	6:off
cgred          	0:off	1:off	2:off	3:off	4:off	5:off	6:off
...

# 現在のランレベルで自動起動を有効にする
# 対象サービスの起動スクリプトが既に用意されており、service コマンドで起動・停止可能な状態であることが前提
$ chkconfig {サービス名} on

# 自動起動を無効にする
$ chkconfig {サービス名} off
```
