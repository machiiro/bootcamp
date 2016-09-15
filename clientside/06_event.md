# イベント

ドキュメントやブラウザ、要素に対して何か注目すべきことが発生した場合、ブラウザがイベントを生成します。  
このタイミングで任意の関数が実行されるよう定義することができます。この関数のことをイベントハンドラと呼びます。

イベントには様々な種類があり、発生したイベントの種類を表す文字列をイベントタイプと呼びます。  
例えば、要素をクリックした時のイベントタイプは `click` です。

## イベントタイプの種類

代表的なイベントタイプは以下の通りです。

|オブジェクト|イベントタイプ|説明|
|----------|------------|----|
|window|load|ページの読み込みが完了した時|
|window|DOMContentLoaded|HTML ドキュメントの解析が完了した時|
|Element|click|要素がクリックされた時|
|Element|change|要素の値が変更された時|
|Element|focus|要素にフォーカスが当たった時|
|Element|mouseover|要素にマウスが乗った時|
|Element|submit|フォーム送信が行われた時|

- [イベントリファレンス](https://developer.mozilla.org/ja/docs/Web/Reference/Events)

## イベントハンドラプロパティの設定

これまでの説明で以下のようなコードが出てきました。

```
window.onload = function() {
  ...
};
```

このような `onload`、`onclick` といったイベントハンドラプロパティに対して関数を代入することができます。

ただし、この方法ではイベントタイプ毎に1つしかイベントハンドラを定義することはできません。  
そのため、後述の `addEventListener` メソッドを使ってイベントハンドラを定義するのが一般的です。


## イベントハンドラの登録・破棄

`addEventListener` メソッドでイベントハンドラを定義することができます。

第1引数にイベントタイプ、第2引数にイベントハンドラを指定します。
イベントハンドラの引数にはイベントオブジェクトが渡されます。

```html
<section id="section">test</section>
```

```javascript
var handler = function(event) {
  // イベントタイプを取得
  console.log(event.type);
  // イベント発生の起点となったオブジェクトを取得
  console.log(event.target);
};

document.getElementById('section').addEventListener('click', handler, false);
```

登録したイベントハンドラを破棄する場合は、`removeEventListener` メソッドを使用します。

```javascript
document.getElementById('section').removeEventListener('click', handler, false);
```

## イベントの伝播

マウスイベントやクリックイベントなどは、内包する要素間でイベントが伝播します。これをイベントバブリングと呼びます。

[W3C](https://www.w3.org/TR/DOM-Level-3-Events/) の図がわかりやすいので貼っておきます。

![](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)

キャプチャリングフェーズでは、イベントが発生した要素を起点にツリー構造のルートまで辿り、起点の要素までイベントを発生させます。
その後、バブリングフェーズでは起点の要素からルート要素までイベントを発生させます。

先ほどの `addEventListener` の第3引数に指定していた論理値は、キャプチャリングフェーズで実行するか、バブリングフェーズで実行するかを指定するものでした。
一般的にはバブリングフェーズで実行させるため `false` と指定していましたが、キャプチャリングフェーズで実行させたい場合は `true` を指定します。


```html
<section>
  <div>test</div>
</section>
```

以下のコードの場合、バブリングフェーズで動作します。

```javascript
document.getElementsByTagName('section')[0].addEventListener('click', function() {
  console.log('section click!');
}, false);

document.getElementsByTagName('div')[0].addEventListener('click', function() {
  console.log('div click!');
}, false);
```

以下のコードの場合、キャプチャリングフェーズで動作します。

```javascript
document.getElementsByTagName('section')[0].addEventListener('click', function() {
  console.log('section click!');
}, true);

document.getElementsByTagName('div')[0].addEventListener('click', function() {
  console.log('div click!');
}, true);
```

## イベントのキャンセル

フォームの送信処理など、イベントにはデフォルトで操作が定義されているものがあります。
デフォルトの操作をキャンセルしたい場合は、イベントオブジェクトの `preventDefault` メソッドを使用します。

```html
<form action="http://www.google.co.jp" method="POST">
  <input type="text" name="q">
  <input type="submit">
</form>
```

```javascript
var form = document.getElementsByTagName('form')[0];
form.addEventListener('submit', function(event) {
  console.log('stop submit');
  event.preventDefault();
});
```
