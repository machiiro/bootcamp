# テンプレート

Play! ではテンプレートエンジンとして Groovy を採用しています。

## 基本構文

値の評価は ${...} 構文を使用します。メソッドを実行することも可能です。
また、`.` でフィールドアクセスする場合に `?` を付けることで、オブジェクトが Null の場合でもエラーが発生しないよう制御することが可能です。

```
${user.name}
${user.someMethod()}
${user?.someMethod()}
```

条件分岐は if, elseif, else 構文を使用します。

```
#{if user.isSales}
    sales.
#{/if}
#{elseif user.isDeveloper}
    developer.
#{/elseif}
#{else}
    other.
#{/else}
```

ループ処理は list 構文を使用します。

```
#{list items: users, as: 'user'}
    ${user.name}
#{/list}
```

別のテンプレートを読み込む場合は include 構文を使用します。
読み込み元と読み込み先のテンプレートでスコープは同一となります。

```
#{include 'another.html' /}
```

テンプレート上にコントローラの URL を展開したい場合は `@{}` 構文を使用します。
メソッドの引数は省略可能です。

```
<a href="@{Users.show(user.id)}">${user.name}</a>
```

## エラーメッセージの表示

Play! では、コントローラ側でエラーが発生した場合に、テンプレート上でエラーメッセージを表示させるための標準的なアプローチが用意されています。

まず、コントローラ側でエラー情報をセットします。
`validation` オブジェクトを使用して、入力チェック処理を行うか、独自にエラーメッセージを追加します。

```java
// 必須チェック
validation.required(user.name);

// 独自にエラーメッセージを追加、第1引数は同一エラーメッセージを追加しないよう制御するためのキー文字列
validation.addError("errorMessage", "error!");
```

テンプレート側では `ifErrors` タグ、`errors` タグを使用します。

```html
#{ifErrors}
   <h1>Oops…</h1>
   #{errors}
       <li>${error}</li>
   #{/errors}
#{/ifErrors}
```
## テンプレートの継承

ヘッダやサイドバーなどのサイト全体の共通部分と、ページ毎に変化するコンテンツエリアを分割したいような場合、テンプレートの継承機能を利用します。

```parent.html
<html>
<body>
    <head>...</head>

    <section id="container">
        #{doLayout /}
    </section>

    <footer></footer>
</body>
</html>
```

```child.html
#{extends 'parent.html' /}

<h1>child contents.</h1>
```

## カスタムテンプレートタグ

独自のタグを定義したい場合、`app/views/tags` 配下にテンプレートファイルを配置します。

```app/views/tags/hello.html
Hello, World!
```

カスタムテンプレートタグを呼び出すには以下のように記述します。

```
#{hello /}
```

パラメータを受け取ることも可能です。
渡すパラメータが1つの場合は以下のように記述します。

```app/views/tags/hello.html
Hello, ${_arg}!
```

呼び出し側でパラメータを付与します。

```
#{hello "yamada" /}
```

パラメータが複数の場合、明示的にパラメータ名を記述する必要があります。
パラメータ名の先頭には必ず `_ (アンダースコア)` が付きます。

```app/views/tags/hello.html
Hello, ${_name} a.k.a ${_nickname}!
```

呼び出し側でもパラメータ名を指定します。

```
#{hello name: "yamada", nickname: "da-yama" /}
```

## カスタム Java タグ

カスタムテンプレートタグを Java で実装することも可能です。
`play.templates.FastTags` を継承したクラスを用意しておくだけで、Play! が自動的に認識してタグを使用することができます。

```java
public class PlayFastTags extends FastTags {
    // #{empty list}#{/empty} タグを定義
    public static void _empty(Map<?, ?> args, Closure body, PrintWriter out, ExecutableTemplate template, int fromLine) {
        Collection<?> collection = (Collection<?>) args.get("arg");
        if (collection != null && collection.isEmpty()) {
            out.println(JavaExtensions.toString(body));
        }
    }
}
```

## Java オブジェクトの拡張

テンプレート内で扱う Java オブジェクトに、動的にメソッドを拡張することが出来ます。
`play.templates.JavaExtensions` を継承したクラスを用意しておくだけで、Play! が自動的にメソッド拡張を行ってくれます。

例えば、`java.util.Date` をフォーマットするメソッドを追加する場合、以下のように定義します。

```
public class PlayJavaExtensions extends JavaExtensions {

    public static String formatDate(Date date) {
        return FormatUtil.formatDate(date);
    }

}
```

テンプレート側で、予め定義されたメソッドのように呼び出すことが出来ます。

```
${user.createdAt.formatDate()}
```

## 暗黙オブジェクト

テンプレート内で既に定義されているオブジェクトがあります。
これらは予約語となるため、変数名に使用しないよう注意しましょう。

| 変数名 | 説明 |
| --- | --- |
| errors | play.data.validation.Validation.errors() から返却されたエラーメッセージのリスト |
| flash | play.mvc.Scope.Flash オブジェクト |
| lang | 現在の言語 |
| messages | メッセージのマップ |
| out | 出力ストリーム |
| params | 現在のパラメータ |
| play | play.Play オブジェクト |
| request | play.mvc.Request オブジェクト |
| session | play.mvc.Scope.Sessionオブジェクト |
