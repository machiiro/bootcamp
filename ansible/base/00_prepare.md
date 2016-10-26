# 事前準備

## Vagrant をインストールする

Ansible 実行環境として Vagrant を利用します。
ローカル環境に Vagrant がインストールされていない場合はインストールしてください。

https://www.vagrantup.com/docs/installation/

- VirtualBox をインストール
- Vagrant をインストール

## Ansible 実行環境を構築する

任意のディレクトリを作成します。

```bash
$ mkdir ansible-tutorial
```

ディレクトリ配下に、新規に `Vagrantfile` ファイルを作成し、以下の内容をペーストします。

```Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-7.2"
  config.vm.hostname = "vagrant-ansible"

  config.vm.network "private_network", ip: "192.168.33.10"
  config.ssh.forward_agent = true
  config.vm.synced_folder "./", "/ansible-tutorial", mount_options: ['dmode=777','fmode=755']
end
```

ディレクトリ配下に、Ansible 実行対象のサーバーに接続するための鍵を配置します。  
以下からダウンロードしてください。

https://git.machiiro.jp:2443/machiiro/machiiro-tools-env/raw/master/files/machiiro-tools.pem

```bash
$ ansible-tutorial  ls
Vagrantfile         machiiro-tools.pem
```

<font color="red">※ Windows ユーザーの方へ
Windows の場合、共有ディレクトリ配下で chmod が効かないようなので、
pem ファイルを共有ディレクトリ外に配置してください</font>

次に `vagrant up` を実行します。
初回実行時は少し時間がかかります。

```bash
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'bento/centos-7.1' is up to date...
==> default: A newer version of the box 'bento/centos-7.1' is available! You currently
==> default: have version '2.2.1'. The latest is version '2.2.2'. Run
==> default: `vagrant box update` to update.
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 22 => 2222 (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection timeout. Retrying...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: /vagrant => /Users/mkudo/dev/sandbox/ansible-tutorial
    default: /ansible-tutorial => /Users/mkudo/dev/sandbox/ansible-tutorial
```

`vagrant ssh` で SSH 接続し、鍵ファイルが存在することを確認してください。

```bash
$ vagrant ssh
Last login: Mon Feb  8 07:20:17 2016 from 10.0.2.2
[vagrant@vagrant-ansible ~]$ cd /ansible-tutorial/
[vagrant@vagrant-ansible ansible-tutorial]$ ls
Vagrantfile  machiiro-tools.pem
```

## Windows での確認手順

vagrant の ssh 接続情報を~/.ssh/config に追加後

```bash
$ vagrant ssh-config --host ansible >> ~/.ssh/config
```

`ssh ansible` で SSH 接続し、鍵ファイルが存在することを確認してください

```bash
$ ssh ansible
Last login: Mon Feb  8 07:20:17 2016 from 10.0.2.2
[vagrant@vagrant-ansible ~]$ cd /ansible-tutorial/
[vagrant@vagrant-ansible ansible-tutorial]$ ls
Vagrantfile  machiiro-tools.pem
```

※ 追記  
以下の様に vagrant ssh コマンドを叩けば、上記の手順を踏まずに確認できます。

```bash
$ vagrant ssh -- -t -t
```
