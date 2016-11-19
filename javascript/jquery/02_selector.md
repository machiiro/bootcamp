# セレクタ

jQuery で何かコードを書く場合、まずは操作したい DOM を取得する必要が出てくるでしょう。

`$` 関数にセレクタ文字列を渡すことで、条件に一致した要素を jQuery オブジェクトとして取得することが可能です。
DOM 要素そのものではなく、jQuery オブジェクトとして取得されることに注意が必要です。

jQuery オブジェクトは一見配列のように見えますが、実体はオブジェクトです。jQuery オブジェクトには DOM を操作するためのクロスブラウザに対応した様々な API が定義されています。

本章では代表的なセレクタを紹介します。
その他のセレクタについては jQuery の API ドキュメントを参照してください。

- [Selectors](http://api.jquery.com/category/selectors/)

## 基本セレクタ

基本的には `querySelector` や CSS で定義するセレクタと同じです。

```html
<form id="form">
  <input type="text" name="text">
  <select name="select">
    <option>A</option>
    <option selected>B</option>
    <option>C</option>
  </select>
  <input type="checkbox" name="checkbox" value="on" checked>
  <input type="radio" name="radio" value="1">
  <input type="radio" name="radio" value="2" checked>
  <button type="submit" class="btn">Go!</button>
</form>

<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
```

```javascript
console.log($('form')); // タグ名を指定
console.log($('#form')); // IDを指定
console.log($('.btn')); // クラス名を指定
console.log($('button[type=submit]')); // 属性を指定
```

## AND/OR 条件

連続でつなげると AND 条件、カンマで区切ると OR 条件となります。

```javascript
console.log($('button.btn')); // タグが button、かつクラス名が .btn
console.log($('input,button')); // タグが input または button
```

## 階層指定

```javascript
console.log($('form > button')); // form 直下の button
console.log($('body button')); // body 配下にある button
```

## フィルター

```javascript
console.log($('input[name=text]')); // name が text
console.log($('input[name^=text]')); // name が t で始まる
console.log($('input[name$=text]')); // name が t で終わる
console.log($('input[name*=text]')); // name に e が含まれる

console.log($('input[type=radio]')); // 全てのラジオボタン
console.log($('input[type=radio]:checked')); // 選択されているラジオボタン
console.log($('select > option:selected')); // 選択されているプルダウン要素
```
