# window オブジェクト

クライアントサイド JavaScript では、ブラウザウィンドウを表す `window` というオブジェクトがグローバル変数として定義されています。

```javascript
console.log(window);
```

`window` オブジェクトはスコープチェーンの先頭に存在するため、`window` オブジェクトが持つプロパティ・メソッドはグローバル変数・グローバル関数として参照することが可能です。

```javascript
console.log(window.document);
console.log(document);
console.log(window.document === document);

console.log(window.setTimeout);
console.log(setTimeout);
console.log(window.setTimeout === setTimeout);
```

つまり、`var` 無しで変数宣言すると、`window` オブジェクトのプロパティとして代入されます。(非推奨ですが)

```javascript
name = 'abcd';
console.log(window.name);
```

## Document オブジェクト

`window` オブジェクトのプロパティの中で非常に重要なものが `document` です。

`document` プロパティは、ウィンドウ中に表示されているコンテンツを表す `Document` オブジェクトを参照します。
`Document` オブジェクトには、HTML ページの情報を検索・更新するための様々なメソッド (DOM API) が用意されていますが、それらのメソッドの詳細については後述の章で説明します。

```javascript
// ページタイトルを表示
console.log(document.title);
```

- [document](https://developer.mozilla.org/ja/docs/Web/API/document)

## Location オブジェクト

`Location` オブジェクトは、ウィンドウ中に表示されているドキュメントの現在の URL を表します。

以下のプロパティにアクセスすることで、現在の URL の構成要素を取得できます。

```javascript
console.log(location.protocol);
console.log(location.port);
console.log(location.host);
console.log(location.hostname);
console.log(location.pathname);
console.log(location.search);
console.log(location.hash);
console.log(location.origin);
```

ページを遷移する場合は `location` または `location.href` に URL を代入するか、`location.assign` メソッドを使用します。

```javascript
location = 'http://www.google.co.jp';
location.href = 'http://www.google.co.jp';
location.assign('http://www.google.co.jp');
```

ブラウザの履歴に追加せずに遷移したい場合は `replace` メソッドを使用します。

```javascript
location.replace('http://www.google.co.jp');
```

ページをリロードする場合は `reload` メソッドを使用します。

```javascript
location.reload();
```

- [location](https://developer.mozilla.org/ja/docs/Web/API/location)

## History オブジェクト

`History` オブジェクトには、ウィンドウの閲覧履歴情報が格納されています。

```javascript
// 履歴の件数
console.log(history.length);
```

以下のメソッドを利用することで、履歴を元にページを操作することができます。

```javascript
// 1つ前に進む
history.forward();

// 1つ前に進む
history.back();

// 指定位置まで戻る。この場合は2つ前に戻る
history.go(-2);
```

これらの API を元に独自に履歴をアプリケーションを開発しようとすると、実際にはとても複雑になります。
そこで現在では HTML5 History API が追加されています。詳細については後述の章で紹介します。

- [history](https://developer.mozilla.org/ja/docs/Web/API/history)

## Navigator オブジェクト

`Navigator` オブジェクトには、ブラウザの種類・ベンダー・バージョン情報等が格納されています。
ユーザーエージェントを取得したい場合には `userAgent` プロパティを参照します。

```javascript
console.log(navigator.appName);
console.log(navigator.appVersion);
console.log(navigator.userAgent);
console.log(navigator.platform);
```

- [navigator](https://developer.mozilla.org/ja/docs/Web/API/navigator)
