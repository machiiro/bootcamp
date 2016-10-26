# パッケージ管理

パッケージ管理のためのコマンドは Linux ディストリビューションによって異なります。
ここでは RHEL/CentOS/Amazon Linux で使われる `yum` の使い方を解説します。

## yum info - パッケージの詳細情報を表示する

```
$ yum info git
```

## yum search - パッケージ情報を検索する

```
$ yum search git
```

## yum list - インストール可能なパッケージの一覧を表示する

```bash
$ yum list

# インストール済みのパッケージのみを表示する
$ yum list installed

# grep を併用し、インストールされているかどうかを確認する
$ yum list installed | grep git
```

## yum install - パッケージをインストールする

```bash
$ yum install git

# サイレントインストールする
$ yum install git -y
```

## yum update - パッケージを更新する

```bash
$ yum update git
```

## yum remove - パッケージを削除する

```bash
$ yum remove git
```
