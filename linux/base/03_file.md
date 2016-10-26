# ファイル操作

## pwd - 現在のディレクトリを確認する

```bash
$ pwd
/home/ec2-user
```

## cd - ディレクトリを移動する

```bash
$ cd /etc

# 何も指定しないとホームディレクトリに移動する
$ cd
```

## ls - ファイル・ディレクトリ一覧を表示する

```bash
# カレントディレクトリ配下のファイル・ディレクトリを表示する
$ ls

# ファイル・ディレクトリの詳細を表示する
$ ls -l

# ドットファイルも合わせて表示する
$ ls -al

# 指定ディレクトリ配下のファイル・ディレクトリを表示する
$ ls /etc
```

## mkdir - ディレクトリを作成する

```bash
$ mkdir foo

# サブディレクトリまで作成する
$ mkdir -p foo/baar
```

## rmdir - ディレクトリを削除する

```bash
# foo 配下にファイルが何もない状態でなければ削除できない
$ rmdir foo
```

## rm - ファイルを削除する

```bash
$ rm hoge.txt

# ディレクトリと中身を丸ごと削除する
$ rm -R foo

# 警告メッセージを出さず削除する
$ rm -Rf foo
```

## cat - ファイルの中身を表示する

```bash
$ cat /etc/hosts
```

## cp - ファイルをコピーする

```bash
$ cp foo.txt foo.txt.bak

# ディレクトリを丸ごとコピーする
$ cp -R foo bar
```

## touch - ファイルのタイムスタンプを更新する

```bash
$ touch foo.txt

# ファイルが存在しない場合は空のファイルが作成される
$ touch foo2.txt
```

## mv - ファイル・ディレクトリを移動する (＝リネームする)

```bash
$ mv foo bar
```

## ln - シンボリックリンクを作成する

```bash
$ ln -s /usr/local/bin ~/bin

# 作成したシンボリックリンクは ls で確認可能
$ ls -l
lrwxrwxrwx 1 ec2-user ec2-user 14  3月 10 19:38 bin -> /usr/local/bin

# rm で削除可能
$ rm bin
```

## chown - ファイルのオーナー情報を変更する

```bash
# ユーザー nginx 、グループ nginx に変更する
$ chown nginx:nginx foo.txt

# ディレクトリ配下を一括で変更する
$ chown -R nginx:nginx foo/
```

## chmod - ファイル・ディレクトリのアクセス権を変更する

```bash
# シェルに実行権限を付与する
$ chmod +x foo.sh

# ディレクトリ配下を一括で変更する
$ chmod -R 755 foo/
```

## find - ファイル・ディレクトリを検索する

```bash
# ホームディレクトリ配下の html ファイルを検索
$ find ~/ -name *.html
```

## tar - アーカイブを作成・展開する

```bash
# アーカイブを作成する
$ tar czvf foo/ foo.tar.gz

# アーカイブを展開する
$ tar xzvf foo.tar.gz
```

## tail - ファイルの末尾を表示する

```bash
$ tail /var/log/maillog

# ファイルの内容を監視し、表示を更新する
$ tail -f /var/log/maillog
```
