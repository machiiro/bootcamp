# 依存性管理

Play! アプリケーションの依存性は全て `conf/dependencies.yml` で管理されます。
`play dependencies` コマンドを実行することで、`conf/dependencies.yml` を元に依存ライブラリのインストールが行われます。

## ライブラリへの依存

依存するライブラリは `lib/` に格納されます。
例えば、Commons Collection 4 系を利用したい場合、以下の設定を行います。

```conf/dependencies.yml
# Application dependencies

require:
    - play
    - org.apache.commons -> commons-collections4 4.1
```

次に `play dependencies` コマンドを実行します。
正常に終了すると、`lib/` に `commons-collections4-4.1.jar` がインストールされます。

```
$ play dependencies
~        _            _
~  _ __ | | __ _ _  _| |
~ | '_ \| |/ _' | || |_|
~ |  __/|_|\____|\__ (_)
~ |_|            |__/
~
~ play! 1.2.7.2, http://www.playframework.org
~
~ Resolving dependencies using /Users/mkudo/dev/sandbox/play-tutorial/conf/dependencies.yml,
~
~ 	org.apache.commons->commons-collections4 4.1 (from mavenCentral)
~
~ Downloading required dependencies,
~
~ 	downloaded http://repo1.maven.org/maven2/org/apache/commons/commons-collections4/4.1/commons-collections4-4.1.jar
~ 	downloaded http://repo1.maven.org/maven2/org/apache/commons/commons-collections4/4.1/commons-collections4-4.1-sources.jar
~
~ Installing resolved dependencies,
~
~ 	lib/commons-collections4-4.1.jar
~
~ Done!
~
```

なお、Eclipse 上ではビルドパスに  `lib/commons-collections4-4.1.jar` が追加されていません。
手動で追加するか、再度 `play eclipsify` を実行してください。

## モジュールへの依存

Play! にはモジュールという概念があり、アプリケーションをいくつかのモジュールを構成して開発することが可能です。
Play! には様々なモジュールが公開されており、以下のサイトから確認することが可能です。

自分でモジュールを作成する場合は、`play new-module` コマンドを使用します。

例えば、Google Guice を Play! で利用するためのモジュール `guice` を利用する場合は、以下のように dependencies.yml を定義します。

```conf/dependencies.yml
# Application dependencies

require:
    - play
    - play -> guice 1.2
```

次に Play! モジュールをインストールします。

```
$ play install guice-1.2
```

次に `play dependencies` コマンドを実行します。
正常に終了すると、`modules/` に `guice-1.2` がインストールされます。

```
~        _            _
~  _ __ | | __ _ _  _| |
~ | '_ \| |/ _' | || |_|
~ |  __/|_|\____|\__ (_)
~ |_|            |__/
~
~ play! 1.2.7.2, http://www.playframework.org
~
~ Resolving dependencies using /path-to-path/play-tutorial/conf/dependencies.yml,
~
~ 	play->guice 1.2 (from playLocalModules)
~ 	com.google.inject->guice 4.0 (from mavenCentral)
~ 	aopalliance->aopalliance 1.0 (from mavenCentral)
~
~ Some dynamic revisions have been resolved as following,
~
~	com.google.inject->guice [2.0,) will use version 4.0
~
~ Installing resolved dependencies,
~
~ 	modules/guice-1.2 -> /path-to-path/dev/play/1.2.7/modules/guice-1.2
~ 	lib/guice-4.0.jar
~ 	lib/aopalliance-1.0.jar
~
~ Done!
~
```

Eclipse 上で `modules/` をビルドパスに含めるため、再度 `play eclipsify` を実行してください。
