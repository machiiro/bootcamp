# データ操作

本章では jQuery オブジェクトに割り当て可能なデータの操作方法を説明します。

- [Data](http://api.jquery.com/category/data/)

## HTML5 独自データ属性 (data-*) を参照する

HTML5 から、要素に対して独自の属性 (独自データ属性) を定義可能となりました。
Bootstrap 等の CSS フレームワークでも多用されています。

独自データ属性の情報を参照する場合は、`data()` API を利用します。この時、返却値の型は暗黙的に変換されます。

```html
<div data-role="modal" data-type="1">
</div>
```

```javascript
var $modal = $('[data-role=modal]');
console.log($modal.data('role'));        // data-＊ で定義された属性の情報は `data()` で取得可能
console.log(typeof $modal.data('type')); // 数値として取得
console.log($modal.attr('data-role'));   // attr で取得することも可能
```

一見 `attr()` を使っても良さそうに見えますが、値を変更した場合の挙動が異なります。

`data()` を使って変更しても HTML 上の属性は変更されません。独自データ属性は対象要素の初期データとして扱われ、`data()` で変更を行っても属性値への反映は行われないためです。

```javascript
var $modal = $('[data-role=modal]');
console.log($modal.data('role'));      // 'modal'
$modal.data('role', 'button');
console.log($modal.data('role'));      // 'button'
console.log($modal.attr('data-role')); // 'modal'、変更されていない
```

あくまで属性値に対する操作を行いたい場合は、`attr()` を利用します。この場合はデータの方が変更されなくなります。

```javascript
var $modal = $('[data-role=modal]');
console.log($modal.data('role'));      // 'modal'
$modal.attr('data-role', 'button');
console.log($modal.data('role'));      // 'modal'、変更されていない
console.log($modal.attr('data-role')); // 'button'
```

## データに JavaScript オブジェクトを割り当てる

独自データ属性だけではなく、JavaScript のオブジェクトを割り当てることも可能です。

```javascript
$('body').data('value', {name: 'foo', num: 1});
console.log($('body').data('value'));
```
