# 自作モジュール

Ansible には 200 以上のライブラリが用意されていますが、
用途に合わせて自分でモジュールを作成することも可能です。

また、自作モジュールはどんなスクリプト言語で実装されても構いません。
bash でも python でも ruby でも、好きな言語で実装することができます。

http://docs.ansible.com/ansible/developing_modules.html

## 自作モジュールの配置先

自作モジュールは以下のパスに配置する必要があります。

- 実行したディレクトリ直下にある library ディレクトリ
- ansible.cfg の library に記載したパス
- 環境変数 ANSIBLE_LIBRARY
- ansible-playbook 実行時に指定した --module-path (--M) のパス
- role 内の library ディレクトリ

## 自作モジュールを作成してみる

今回は、指定したファイルのバックアップファイルを一度だけ作るモジュールを作成してみましょう。

まず、`/ansible-tutorial/library` ディレクトリを作成します。

```bash
[vagrant]$ mkdir library
```

次に `library/backup` ファイルを作成し、以下の内容をペーストします。
今回は python で記述しています。

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import re
import shutil

def main():
    # 引数を取得する
    module = AnsibleModule(
        argument_spec = dict(
            src = dict(required=True)
        )
    )

    src = os.path.expanduser(module.params['src'])
    dest = src + '.bak'

    # 自作モジュールでも冪等性を保つよう、changed を管理する
    changed = False

    # バックアップファイルが存在しない場合のみコピー
    if not os.path.exists(dest):
        shutil.copyfile(src, dest)
        changed = True

    module.exit_json(dest = dest, src = src, changed = changed)

# import module snippets
from ansible.module_utils.basic import *
main()
```

## 自作モジュールを使用してみる

`playbook.yml` で backup モジュールを使用するよう修正します。

```playbook.yml
- hosts: all
  remote_user: ec2-user
  become: yes
  gather_facts: no
  tasks:
    - backup: src=/etc/hosts
  # roles:
  #   - nginx
```

次に `backup` に実行権限を付与します。

```bash
[vagrant]$ chmod +x library/backup
```

playbook を実行してみましょう。
2回目の実行では `changed` ではなく `ok` となることを確認してください。
また実際にサーバーにログインし、`/etc/hosts.bak` が作成されていることも確認してください。

```bash
[vagrant]$ ansible-playbook nginx.yml

PLAY ***************************************************************************

TASK [backup] ******************************************************************
changed: [xx.xx.xx.xx]

PLAY RECAP *********************************************************************
xx.xx.xx.xx                : ok=1    changed=1    unreachable=0    failed=0
```
