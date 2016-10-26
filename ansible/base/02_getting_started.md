# インストール〜基本操作

## Ansible をインストール

まずは Ansible をインストールしましょう。
Ansible 2.0 をインストールするため、`pip` を使ってインストールします。

なお、Ansible の実行には python が必要ですが、今回構築した実行環境には既にインストールされているため、インストール作業は不要です。

```bash
[vagrant]$ sudo yum install gcc python-devel -y
[vagrant]$ curl https://bootstrap.pypa.io/ez_setup.py -o - | sudo python
[vagrant]$ curl https://bootstrap.pypa.io/get-pip.py -o - | sudo python
[vagrant]$ sudo pip install ansible
```

`ansible --version` を実行し、2.0 がインストールされていることを確認してください。

```bash
[vagrant]$ ansible --version
ansible 2.0.0.2
  config file =
  configured module search path = Default w/o overrides
```

## inventory ファイルを作成する

Ansible の実行対象サーバーを定義した inventory ファイルを作成します。
inventory ファイルは ini 形式で作成します。

`/etc/ansible/hosts` に作成すると、実行時に自動的に読み込まれるのでそちらに作成しましょう。

```bash
[vagrant]$ sudo mkdir -p /etc/ansible
[vagrant]$ sudo vi /etc/ansible/hosts
```

ファイルの中身には、事前に配布された EC2 インスタンスのパブリック IP アドレスを記載します。

```/etc/ansible/hosts
xx.xx.xx.xx
```

## ansible コマンド

`ansible` コマンドを使って、簡単なシェルをサーバー上で実行してみましょう。

```bash
[vagrant]$ ansible all -m command -a "uptime" -u ec2-user --private-key machiiro-tools.pem
xx.xx.xx.xx | SUCCESS | rc=0 >>
 07:41:19 up 34 min,  1 user,  load average: 0.00, 0.01, 0.05
```

- `all` を指定したことで、inventory ファイルに記載された全サーバーが対象となります
    - `all` の代わりに IP アドレスを指定すると、対象サーバーのみに対して実行されます
- `-m` でモジュールを指定します。詳細は別章で説明します
- `-a` で実行シェルを指定します
- `-u` で実行ユーザーを指定します
- `--private-key` で SSH 秘密鍵を指定します

## ansible.cfg ファイルを作成する

毎回 `--private-key` を指定するのは煩雑なので、Ansible 設定ファイル `ansible.cfg` を作成しましょう。

```bash
[vagrant]$ sudo vi /etc/ansible/ansible.cfg
```

```/etc/ansible/ansible.cfg
[defaults]
private_key_file=./machiiro-tools.pem
```

`--private-key` を指定せずに、`ansible-playbook` が実行可能なことを確認してください。

```bash
[vagrant]$ ansible all -m command -a "uptime" -u ec2-user
xx.xx.xx.xx | SUCCESS | rc=0 >>
 07:41:19 up 34 min,  1 user,  load average: 0.00, 0.01, 0.05
```

ansible.cfg には他にも様々な設定項目があります。
http://docs.ansible.com/ansible/intro_configuration.html
