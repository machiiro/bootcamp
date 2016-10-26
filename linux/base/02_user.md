# ユーザー操作

## sudo - 別のユーザーとしてコマンドを実行する

```bash
# root のみ許可されているコマンドを実行する
$ sudo service nginx restart

# 指定したユーザーで実行する
$ sudo -u user xxx.sh
```
## su - 別のユーザーに切り替える

```bash
# root に切り替える、環境変数は元のユーザーのまま
$ su
# root に切り替える、環境変数は root のものになる
$ su -
# 指定したユーザーに切り替える
$ su - user
```

## env - ログインユーザーの環境変数を確認する

```bash
$ env
HOSTNAME=ip-10-0-0-151
LESS_TERMCAP_md=
LESS_TERMCAP_me=
TERM=xterm-256color
SHELL=/bin/bash
HISTSIZE=1000
EC2_AMITOOL_HOME=/opt/aws/amitools/ec2
SSH_CLIENT=211.129.113.68 62600 22
LESS_TERMCAP_ue=
...
```
