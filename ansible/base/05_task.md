# タスクの制御

## with_items

シーケンスの数だけループさせてモジュールを実行したい場合、`with_items` を使用します。

```yaml
vars:
  packages:
    - git
    - mosh
tasks:
  - yum: name={{ item }} state=latest
    with_items: packages
```

他にもマップをループさせる `with_dict`、ファイルリストをループさせる `with_fileglob` があります。

## register

モジュールの実行結果を変数に定義したい場合、`register` を使用します。
変数の内容を確認するには `debug` モジュールを使用します。

```yaml
- command: date
  register: d

- debug: var=d
```

## when

モジュールを実行する条件を定義したい場合、`when` を使用します。

```yaml
- apt: name=apache2 state=latest
  when: ansible_os_family = "Debian"
- yum: name=httpd state=latest
  when: ansible_os_family = "RedHat"
```

## ignore_errors

タスクの実行結果がエラーとなると、Ansible の実行が停止します。
エラー発生時でも Ansible の実行を停止させたくない場合、`ignore_errors` を使用します。

```yaml
- command: somescript.sh
  ignore_errors: yes
```
