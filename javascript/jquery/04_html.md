# HTML 操作

本章では取得した jQuery オブジェクトから HTML 上の情報を取得・変更するための API を説明します。

- [Attributes](http://api.jquery.com/category/attributes/)
- [CSS](http://api.jquery.com/category/css/)
- [Manipulation](http://api.jquery.com/category/manipulation/)
- [Properties](http://api.jquery.com/category/properties/)

## DOM 操作

要素を追加・削除します。

```html
<ul>
  <li>A</li>
  <li>B</li>
  <li>C</li>
</ul>
```

```javascript
$('ul').prepend('<li>append</li>');           // 配下の先頭に要素を追加
$('ul').append('<li>append</li>');            // 配下の末尾に要素を追加

$('ul > li:eq(1)').before('<li>append</li>'); // 前に要素を追加
$('ul > li:eq(1)').after('<li>append</li>');  // 後ろに要素を追加

$('ul > li:eq(1)').remove();                  // 要素を削除
```

## コンテンツ操作

HTML やテキストを取得・変更します。

```html
<div>
  <h1>TITLE</h1>
  hogehoge

  <input type="text" value="foo">
</div>
```

```javascript
console.log($('div').html());      // HTML を取得
$('div').html('abc');              // HTML を変更

console.log($('div > h1').text()); // テキストを取得
$('div > h1').text('def');         // テキストを変更

console.log($('input').val());     // 値を取得
$('input').val('bar');             // 値を変更
```

## 属性操作

要素の属性を取得・変更します。

```html
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/89/JJF-_Norwegian_in_the_snow.jpg/200px-JJF-_Norwegian_in_the_snow.jpg">
```

```javascript
// src を取得
console.log($('img').attr('src'));

// src を変更
$('img').attr('src', 'https://upload.wikimedia.org/wikipedia/ja/thumb/5/50/Americanshorthair.JPG/200px-Americanshorthair.JPG');

// オブジェクトを渡して一括変更
$('img').attr({src: 'https://upload.wikimedia.org/wikipedia/ja/thumb/5/50/Americanshorthair.JPG/200px-Americanshorthair.JPG', alt: 'ねこ'});
```

## プロパティ操作

要素のプロパティを取得・変更します。

属性 (attr) との混同しがちですが、以下の通り違いがあります。`attr` はあくまで属性を扱う API であるため、`tagName` のような要素自体の情報を参照する場合などは `prop` を利用する必要があります。

- attr: HTML 上の要素の属性を操作する
- prop: JavaScript 上の HTML Element オブジェクトのプロパティを操作する

```html
<input type="checkbox" value="1">
```

```javascript
var $checkbox = $('input[type=checkbox]');
console.log($checkbox.prop('checked')); // プリパティを取得
console.log($checkbox.attr('checked')); // 属性を取得

$checkbox.prop('checked', true);        // プロパティを変更

console.log($checkbox.prop('checked')); // プリパティを取得
console.log($checkbox.attr('checked')); // 属性を取得
```


## CSS 操作

CSS スタイルを取得・変更します。

```html
<div class="container">
</div>
```

```css
.container {
  height: 100px;
  background-color: #ffcc00;
}
.container.open {
  background-color: #00ffcc;
}
```

```javascript
console.log($('div').css('background-color'));  // CSS プロパティを取得
console.log($('div').hasClass('container'));    // CSS クラスが定義されているかどうかを取得
console.log($('div').addClass('open'));         // CSS クラスを追加
console.log($('div').removeClass('container')); // CSS クラスを削除
console.log($('div').toggleClass('open'));      // CSS クラスが定義されていない場合は追加、定義されている場合は削除
console.log($('div').position());               // 親要素からの相対位置を取得
console.log($('div').offset());                 // 表示位置を取得
```
