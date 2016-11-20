# 横断操作

本章では取得した jQuery オブジェクトを起点とした横断操作 (Traversing) を説明します。

## each

取得した要素に対して関数を実行します。

```html
<div id="section">
  <div>
    <ul>
      <li>A</li>
      <li>
        B
        <ul>
          <li>b1</li>
          <li>b2</li>
        </ul>
      </li>
      <li>C</li>
    </ul>
  </div>
</div>
```

```javascript
$('ul > li').each(function() {
  // `this` には対象の要素自体が格納されており、必要に応じて jQuery オブジェクトに変換する必要がある
  console.log($(this));
});
```

## find

取得した要素を起点に、配下の要素を検索します。

```javascript
console.log($('#section').find('ul'));
```

## first/last

取得した要素を起点に、先頭または末尾の要素を取得します。

```javascript
console.log($('ul > li').first());
console.log($('ul > li').last());
```

## prev/next/siblings

取得した要素を起点に、兄弟要素の要素を取得します。
要素の並びが早い方を兄、遅い方を弟と呼びます。

```javascript
console.log($('ul > li:eq(1)').prev());     // 前の要素 (兄) を取得
console.log($('ul > li:eq(1)').next());     // 次の要素 (弟) を取得
console.log($('ul > li:eq(1)').siblings()); // 自身を除いた兄弟要素のリストを取得
```

## closest/parent/parents

取得した要素を起点に、親要素を取得します。

```javascript
console.log($('ul').parent('div'));  // 直近の親要素を取得
console.log($('ul').parents('div')); // 親要素のリストを取得
console.log($('ul').closest('div')); // 起点から一番近い要素を取得
```

## has

取得した要素を起点に、セレクターに一致する要素を持つ要素を取得します。

```javascript
console.log($('div > ul > li').has('ul'));
```
