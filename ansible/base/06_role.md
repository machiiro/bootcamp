# ロール

playbook による一連の task を共有する仕組みを`ロール`と呼びます。

## ロールのディレクトリ構成

ロールのディレクトリ構成は以下の通りです。
実行する playbook.yml と同階層に `roles` というディレクトリを配置し、その中にロールを定義していきます。

```
roles/
    role-name/
        meta/                     # メタ情報
            main.yml
        defaults/                 # 上書き可能な変数
            main.yml
        vars/                     # 固定となる変数
            main.yml
        files/                    # コピー用のファイル
            main.yml
        templates/                # コピー用のテンプレートファイル
            virtualhost.conf.j2
        handlers/                 # ハンドラー
            main.yml
        tasks/                    # タスク
            main.yml
```

## ロールを作成してみる

先ほど実行した nginx のインストールタスクをロールにしてみましょう。
まず、以下のディレクトリ構成を作成します。

```bash
[vagrant]$ mkdir -p roles/nginx/tasks
[vagrant]$ vi roles/nginx/tasks/main.yml
```

```
roles/
    nginx/
        tasks/
            main.yml
```

`roles/nginx/tasks/main.yml` に以下の内容をペーストします。

```yaml
- name: Install nginx
  yum: name=nginx state=latest update_cache=yes

- name: Enabled nginx service
  service: name=nginx state=started enabled=yes
```

次に nginx.yml に `roles` を定義します。

```yml
- hosts: all
  remote_user: ec2-user
  become: yes
  gather_facts: no
  roles:
    - nginx
```

修正した playbook を実行してみましょう。
変更前と同様に nginx インストール処理が動作することを確認してください。

```bash
[vagrant]$ ansible-playbook nginx.yml

PLAY ***************************************************************************

TASK [nginx : Install nginx] ***************************************************
ok: [xx.xx.xx.xx]

TASK [nginx : Enabled nginx service] *******************************************
ok: [xx.xx.xx.xx]

PLAY RECAP *********************************************************************
xx.xx.xx.xx                : ok=2    changed=0    unreachable=0    failed=0
```

## ロールの実行順序

`roles` と `tasks` が両方定義されている場合、roles が先に実行されます。
