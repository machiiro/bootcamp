# コントローラ

## コントローラクラスの要件

Play! におけるコントローラは以下の要件を満たす必要があります。

- `controllers` パッケージ配下にクラスが存在する
- `play.mvc.Controller` を継承する

## HTTP リクエストパラメータの取得

Play! ではコントローラ側で HTTP リクエストパラメータを取得する方法として、大きく2つの方法があります。

### Request オブジェクトから生のパラメータを取得する

Controller からアクセス可能な `request` オブジェクトから取得可能です。

```java
Map<String, String[]> allParams = request.params.all();
Map<String, String> allSimpleParams = request.params.allSimple();
```

### コントローラの引数と紐付ける

例えば Play! では以下のように記述することが可能です。
引数の変数名はそのままリクエストパラメータの名称として使用されます。

```java
public static void someMethod(String name, String email) {
    User user = new User();
    user.name = name;
    user.email = email;
    renderJSON(user);
}
```

この場合、以下の URL でリクエストパラメータを渡すことが出来ます。
http://localhost:9000/someMethod?name=yamada&email=yamada@machiiro.jp

引数にはクラスを指定することも可能です。

```java
public static void someMethod(User user) {
    renderJSON(user);
}
```

この場合、リクエストパラメータの名前に `user.` プレフィックスを付ける必要があります。
http://localhost:9000/someMethod?user.name=yamada&user.email=yamada@machiiro.jp

## レンダリング

コントローラは HTTP レスポンスとして何らかの結果を返す必要があります。

テンプレートを介して HTML を返す場合、`render` メソッドを実行します。
この時コントローラクラスのパッケージ構成に合わせて自動的に HTML ファイルが選択されます。
例えば、`controllers/Users/show` というコントローラメソッドの場合、`views/Users/show.html` が選択されます。

```java
render();
```

使用するテンプレートファイルを明示的に指定する場合は、`render` の第1引数に `@` 付きでパスを指定します。

```java
render("@show_another_template");
```

テンプレートに値を渡したい場合は、render の引数に追加するか、renderArgs メソッドを利用します。
この時定義した変数名が、そのままテンプレートで参照可能な変数の名称となります。

```java
// renderArgs を使うパターン、テンプレート側では ${user2} でアクセス可能となる
renderArgs.put("user2", new User());

// render の引数に指定するパターン、テンプレート側では ${user} でアクセス可能となる
User user = new User();
render(user);
```

その他の render メソッドは以下の通りです。
全て HTTP ステータス 200 で返します。

| メソッド | 説明 |
| --- | --- |
| renderText | 平文を返す |
| renderHTML | HTMLを返す |
| renderXml | XML を返す |
| renderJSON | JSONを返す、RESTful API 等で使用 |
| renderBinary | バイナリを返す、ファイルダウンロードで使用 |

また、各 HTTP ステータスコードで返却するためのメソッドも用意されています。

| メソッド | 説明 |
| --- | --- |
| error | HTTP 500 で返す |
| redirect | HTTP 302 で返し、指定URLにリダイレクトする |
| unauthorized | HTTP 401 で返す |

## コントローラメソッドのチェーン

コントローラメソッド内で、別の `public static void` メソッドを実行すると、HTTP Redirect として処理されます。
例えば、保存後に詳細画面を再度開き直すには、単に詳細画面を表示するためのメソッドを実行するだけで済みます。

```java
public static void show(String code) {
    User user = ...
    render(user);
}

public static void save(User user) {
    user.save();
    show(user.code);
}
```

## インターセプション

コントローラメソッド実行の前後に処理を追加することが可能です。

```java
// メソッド実行前に動作する
@Before
public static void before() {
}

// メソッド実行後に動作する
@After
public static void after() {
}

// 例外発生時に動作する
@Catch(IllegalStateException.class)
public static void logIllegalState(Throwable throwable) {
    Logger.error("Illegal state %s…", throwable);
}

// メソッド実行後に例外発生有無に関わらず動作する
@Finally
public static void finallyAt() {
}
```

コントローラは `play.mvc.Controller` を継承する必要があるため、一部のコントローラに対して共通的なインターセプションを追加する、といったことができません。
その場合は `@With` アノテーションを利用します。

```java
// 認証チェックをしたいコントローラにだけ @With を付ける
@With(Authentication.class)
public class SomeController extends Controller {
}
```

例えば、`Authentication` には以下の様な認証チェックのロジックを記述しておくイメージです。

```java
public class Authentication extends Controller {
    @Before
    static void checkAuthenticated() {
        if(!session.containsKey("user")) {
            unAuthorized();
        }
    }
}    
```
