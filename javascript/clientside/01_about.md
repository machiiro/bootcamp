# クライアントサイド JavaScript とは

Web ブラウザで使用する JavaScript を `クライアントサイド JavaScript` と呼びます。

クライアントサイド JavaScript では、ブラウザウィンドウ自体を表す `window` オブジェクトや、現在のサイトの URL を表す `location` オブジェクト等が、グローバル変数として定義されています。
また、HTML の構造を検索・変更するための API、外部のサーバーへ HTTP リクエストを送るための API などが用意されています。

## JavaScript コードの埋め込み

Web ページから JavaScript コードを読み込む方法は大きく 2 種類あります。

### `<script>` 要素

`<script>` 要素内に JavaScript コードを記述することができます。

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <script>
    window.onload = function() {
      console.log('loaded');
    }
  </script>
</head>
<body>
  <h1>title</h1>
  <p>text...</p>
</body>
</html>
```

### 外部ファイルの読み込み

`<script>` 要素に `src` 属性があり、外部ファイル化した JavaScript の URL を指定すると、ページロード時に読み込んでくれます。

この方法のメリットとして、

- HTML ファイル自体のコードの簡略化
- JavaScript コードの共有
- JavaScript ファイルのブラウザキャッシュの適用、それに伴う Web ページのパフォーマンス向上

が挙げられます。

```javascript
window.onload = function() {
  console.log('loaded');
}
```

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <script type="text/javascript" src="app.js"></script>
</head>
<body>
  <h1>title</h1>
  <p>text...</p>
</body>
</html>
```

### HTML 中のイベントハンドラ

HTML の要素に対してイベントハンドラを記述可能です。
イベントについては後述の章で説明します。

```html
<input type="button" value="button" onclick="clickButton">
```

このような記述方法は、HTML と JavaScript コードを混在させてしまい、ページのコンテンツと振る舞いが分離できないため、現在は推奨されないプログラミングスタイルとなっています。
