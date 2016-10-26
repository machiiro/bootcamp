# playbook

## playbook とは

前章では、`ansible` コマンドを使ってサーバーに対して1つのモジュールを実行できることを確認できましたが、
実際に構成管理を行う場合、複数のモジュール・処理を実行する必要があります。

この `複数のモジュール・処理` を定義したファイルを playbook と呼びます。
`ansible-playbook` コマンドで、所定のサーバーに対して playbook を実行することが可能です。

## playbook の書き方

playbook は YAML 形式で記載し、大きく3つのセクションに別れます。

### target セクション

どのサーバーに対して、どのユーザーで実行するかどうかの設定を行います。

```yaml
- hosts: all # 対象サーバー
  remote_user: ec2-user # 実行ユーザー
  become: yes # sudo で実行するかどうか
  gather_facts: no # サーバーの基本情報を収集するかどうか、no にすると動作が多少早くなる
```

### vars セクション

playbook 内で使用する変数を定義します。
後述のタスク内で指定するモジュールのパラメータ等を変数に置き換えたい場合に定義します。

```yaml
  vars:
    foo: bar
    users:
      - yamada
      - tanaka
```

### tasks セクション

対象サーバーに実行するモジュールとロールを定義します。
モジュールは基本的に上から順番に実行されていきます。

```yaml
  # 読み込むロール
  roles:
    - nginx
    - mysql
    -
  # 実行するタスク
  tasks:
    - copy: ...
    - yum: ...
```

タスクには name を指定することが可能です。
指定しておくと、実行時の結果の表記がわかりやすくなります。

```
  tasks:
    - name: Copy xxx file
      copy: ...
```

タスク毎に実行ユーザーを切り替えることも可能です。

```
  tasks:
    - name: Copy xxx file
      copy: ...
      become: no
      become_user: ec2-user
```

## playbook を実行してみる

それでは、実際に playbook を作成して実行してみましょう。
サンプルとして、以下の操作を実行するための playbook `nginx.yaml` を作成します。

- nginx を yum でインストールする
- nginx を起動状態にする


```nginx.yml
- hosts: all
  remote_user: ec2-user
  become: yes
  gather_facts: no

  tasks:
    - name: Install nginx
      yum: name=nginx state=latest update_cache=yes

    - name: Enabled nginx service
      service: name=nginx state=started enabled=yes
```

`ansible-playbook` を実行し、nginx をインストールします。

```bash
[vagrant]$ ansible-playbook nginx.yml

PLAY ***************************************************************************

TASK [Install nginx] ***********************************************************
changed: [xx.xx.xx.xx]

TASK [Enabled nginx service] ***************************************************
changed: [xx.xx.xx.xx]

PLAY RECAP *********************************************************************
xx.xx.xx.xx                : ok=2    changed=2    unreachable=0    failed=0
```

ブラウザでアクセスし、nginx が起動していることを確認してください。

## モジュールの冪等性を確認する

nginx が既にインストールされている環境に再度 `ansible-playbook` を実行してみましょう。
今度は結果が `changed=0` と表示されるはずです。

```bash
[vagrant]$ ansible-playbook nginx.yml

PLAY ***************************************************************************

TASK [Install nginx] ***********************************************************
ok: [xx.xx.xx.xx]

TASK [Enabled nginx service] ***************************************************
ok: [xx.xx.xx.xx]

PLAY RECAP *********************************************************************
xx.xx.xx.xx                : ok=2    changed=0    unreachable=0    failed=0
```

これは実行したモジュール `yum` と `service` が再度処理を実行する必要があるかどうかを判断しているためで、
処理を行った場合のみ `changed` という判定で表示されます。

このように、操作を1回行っても複数回行っても結果が同じ結果を返す特性のことを冪等性と呼びます。
