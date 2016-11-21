# イベント

本章では jQuery オブジェクトに対してイベントを定義する方法を説明します。

## $([function])

jQuery を使って何か処理をしたい場合、ほとんどのケースで `DOMContentLoaded` イベント (ページの読み込みが完了した際に発火するイベント) のタイミングに何かしらの処理を実行することになります。

jQuery では `$()` というショートハンドが用意されており、簡単にイベントの登録が可能です。

```javascript
$(function() {
  console.log('loaded');
});
$(document).ready(function() {
  console.log('ready');
});
```

ちなみに `$(document).ready([function])` と記述する方法もありますが、現在は非推奨です。

## .on([type], [function])

`.on([type], [function])` でjQuery オブジェクトに対してイベントを割り当てることができます。

```html
<button type="button">Go!</button>
```

```javascript
$('button').on('click', function() {
  console.log('click!');
});
```

`click` や `change` といった代表的なイベントについては専用の API も用意されています。

```javascript
$('button').click(function() {
  console.log('click!');
});
```

## .on([type], [selector], [function])

`.on` にセレクタを指定することで、セレクタに一致する要素に対してイベントを割り当てることができます。
対象要素が動的に変化するようなケースで有効です。

ちなみにこの機能、以前のバージョンでは `.live()` という別の API として用意されていましたが、現在では全て `.on()` に統合されています。

```html
<button type="button">Append</button>
<div>A</div>
<div>B</div>
```

以下のコードでは、追加された要素はイベントが動作しません。

```javascript
$('button').click(function() {
  $('body').append('<div>appended</div>')
});

$('div')
  .on('mouseover', function() {
    $(this).css({'background-color': '#00ccff'});
  })
  .on('mouseout', function() {
    $(this).css({'background-color': ''});
  });
```

以下のように記述すると、body 配下でセレクタに一致する要素に対してイベントハンドラを登録することが可能です。

```javascript
$('button').click(function() {
  $('body').append('<div>appended</div>')
});

$(document.body)
  .on('mouseover', 'div', function() {
    $(this).css({'background-color': '#ffcc00'});
  })
  .on('mouseout', 'div', function() {
    $(this).css({'background-color': ''});
  });
```

### .off([type])

イベントハンドラを破棄したい場合は、`.off([type])` を利用します。

```html
<div style="height: 300px; background-color: #ffcc00;"></div>
```

```javascript
$('div').click(function() {
  console.log('click');
});

// jQuery が登録したイベントハンドラを記憶しているので指定不要
$('div').off('click');
```

複数のライブラリを利用していたりすると、イベントハンドラの登録・破棄処理が被ってしまうケースがあります。

```javascript
// あるライブラリが click イベントハンドラを登録
$('div').click(function() {
  console.log('click1');
});

// 別のライブラリが click イベントハンドラを登録、登録前に破棄している
$('div').off('click').click(function() {
  console.log('click2');
});
```

このようなケースでは、イベントタイプの後ろに `.xxx` といった形式で名前空間を指定します。

```javascript
// あるライブラリが click イベントハンドラを登録
$('div').on('click.1', function() {
  console.log('click1');
});

// 別のライブラリが click イベントハンドラを登録、登録前に破棄している
$('div').off('click.2').on('click.2', function() {
  console.log('click2');
});
```

## カスタムイベント

`click` や `change` といった標準的なイベントタイプではなく、独自に定義したカスタムイベントを定義することが可能です。
また、`.trigger()` を使って独自のタイミングでイベントを発火させることが可能です。

後述の jQuery プラグインを開発する際などに利用されます。

```html
<div data-role="select-block">
  <div>A</div>
  <div>B</div>
  <div>C</div>
</div>
```

```javascript
var $selectBlock = $('[data-role="select-block"]');
$selectBlock.children('div').on('click', function() {
  var $this = $(this);
  $selectBlock.data('current', $this.text());
  $selectBlock.trigger('changeBlock');
});

$selectBlock.on('changeBlock', function() {
  console.log('change: ' + $(this).data('current'));
});
```
