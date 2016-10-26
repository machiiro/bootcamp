# モジュール

Ansible でよく利用される代表的なモジュールを紹介します。

## user

ユーザー追加やパスワード設定など、ユーザー操作を行うためのモジュールです。
http://docs.ansible.com/ansible/user_module.html

```yaml
# ユーザーを追加する
- user: name=johnd comment="John Doe" uid=1040 group=admin
```

## command

任意のコマンドを実行するためのモジュールです。
http://docs.ansible.com/ansible/command_module.html

```yaml
- command: /usr/bin/make_database.sh arg1 arg2
```

## shell

任意のコマンドを実行するためのモジュールです。
`command` とは異なり、`> (リダイレクト)` や `| (パイプ)` を使用することができます。
http://docs.ansible.com/ansible/shell_module.html

```yaml
- shell: somescript.sh >> somelog.txt
```

## stat

ファイルの状態を取得するためのモジュールです。
`register` を併用することで、ファイルの状態を変数として定義することができるため、
ファイルが存在しない場合のみタスクを実行する、といった制御が可能となります。

```yaml
# 変数 p に stat の結果を格納
- stat: path=/path/to/something
  register: p

# ディレクトリが存在する場合のみ実行
- debug: msg="Path exists and is a directory"
  when: p.stat.isdir is defined and p.stat.isdir
```

## file

ファイル・ディレクトリの作成、owner/group の変更、シンボリックリンクの作成等を行うためのモジュールです。
http://docs.ansible.com/ansible/file_module.html

```yaml
# ディレクトリを作成
- file: path=/etc/some_directory state=directory mode=0755
```

## copy

Ansible 実行ホストに配置されているファイルを対象ホストにコピーするためのモジュールです。
http://docs.ansible.com/ansible/copy_module.html

```yaml
- copy: src=/srv/myfiles/foo.conf dest=/etc/foo.conf owner=foo group=foo mode=0644
```

## template

変数が埋め込まれたテンプレートファイルの変数を解決し、ファイルを対象ホストにコピーするためのモジュールです。
テンプレートエンジンには Python の Jinja2 が使用されています。
http://docs.ansible.com/ansible/template_module.html

```yaml
- template: src=/mytemplates/foo.j2 dest=/etc/file.conf owner=bin group=wheel mode=0644
```

## get_url

指定 URL からファイルをダウンロードするためのモジュールです。
http://docs.ansible.com/ansible/get_url_module.html

```yaml
- get_url: url=http://example.com/path/file.conf dest=/etc/foo.conf mode=0440
```

## yum

yum でパッケージをインストールするためのモジュールです。
http://docs.ansible.com/ansible/yum_module.html

```yaml
- yum: name=nginx state=latest
```

## service

サービスの起動状態、再起動設定を行うためのモジュールです。
http://docs.ansible.com/ansible/service_module.html

```yaml
- service: name=nginx state=started
```
