# DOM

DOM (Domain Object Model) とは、HTML や XML 文書の構造を表したり操作したりするための API です。

- [Domain Object Model](https://ja.wikipedia.org/wiki/Document_Object_Model)

HTML の構造はドキュメントツリーと呼ばれるツリー構造で表現されます。  
DOM では、HTML 上の要素・属性・テキスト...全てを「ノード」と呼称します。

- [ドキュメントツリー](http://image.itmedia.co.jp/l/im/ait/articles/0803/12/l_r5gazo01s.jpg)

## ドキュメント要素の選択

Document オブジェクトから、ドキュメント内の要素にあたる Element オブジェクトを選択することができます。

### ID 属性による要素の選択

`getElementById` メソッドで、指定 ID 属性を持つ Element オブジェクトを取得することができます。

```html
<section id="section"></section>
```

```javascript
console.log(document.getElementById('section'));
```

### name 属性による複数要素の選択

`getElementsByName` メソッドで、name 属性を持つ Element オブジェクトの配列を表す NodeList オブジェクトを取得することができます。

```html
<input type="radio" name="gender" value="男性"> 男性
<input type="radio" name="gender" value="女性"> 女性
```

```javascript
console.log(document.getElementsByName('gender'));
```

### タグ名による要素の選択

`getElementsByTagName` メソッドで、指定したタグ名持つ Element オブジェクトの配列を表す NodeList オブジェクトを取得することができます。

```html
<div>
  <span>1</span><span>2</span>
</div>
```

```javascript
console.log(document.getElementsByTagName('span'));
```

### CSS クラスによる選択

`getElementsByClassName` メソッドで、指定したクラス名持つ Element オブジェクトの配列を表す NodeList オブジェクトを取得することができます。

```html
<button class="btn btn-default">ボタン</button>
```

```javascript
console.log(document.getElementsByClassName('btn'));
```

### CSS セレクタ書式による選択

`querySelector`、`querySelectorAll` メソッドで、指定したCSS セレクタ書式にマッチする要素を取得することができます。  
`querySelector` は Element を、`querySelectorAll` は NodeList を返します。

```javascript
querySelectorAll('#id');
querySelectorAll('div');
querySelectorAll('.class');
querySelectorAll('[type]');
querySelectorAll('[type=text]');
```

## ドキュメント構造と探索


### Node オブジェクト

Document オブジェクト、Element オブジェクト、ドキュメント中のテキストを表す Text オブジェクトは、全て Node オブジェクトとして表されます。

Node オブジェクトには以下の重要なプロパティが定義されています。

```html
<body>
  <section>
    <div id="1"></div>
    <div id="2"></div>
    <div id="3"></div>
  </section>
</body>
```

```javascript
var section = document.getElementsByTagName('section')[0];

// ノードの種類を表すタイプを取得
// 1: Element 3: Text 8: Comment 11: Document Fragment
console.log(section.nodeType);
// 親ノードを取得
console.log(section.parentNode);
// 子ノードを取得
console.log(section.childNodes);
// 最初の子ノードを取得
console.log(section.firstChild);
// 最後の子ノードを取得
console.log(section.lastChild);
// 1つ先のノードを取得
console.log(section.childNodes[1].nextSibling);
// 1つ前のノードを取得
console.log(section.childNodes[1].previousSibling);
```

Text ノードを無視して Element ノードを取得するためのプロパティも定義されています。

```javascript
// 子要素の数を取得
console.log(section.childElementCount);
// 最初の子要素を取得
console.log(section.firstElementChild);
// 最後の子要素を取得
console.log(section.lastElementChild);
// 1つ先の要素を取得
console.log(section.childNodes[1].nextElementSibling);
// 1つ前の要素を取得
console.log(section.childNodes[1].previousElementSibling);
```

### 属性

要素の属性はプロパティにアクセスすることで取得可能です。
プロパティを変更することで、属性も変更されます。

```html
<img src="test.png" width="100" height="200" data-type="logo">
```

```javascript
var img = document.getElementsByTagName('img')[0];

// プロパティとして取得
console.log(img.src);
// 属性をまとめて取得
console.log(img.attributes);
// data-xxx 属性をまとめて取得
console.log(img.dataset);
// プロパティを変更
img.src = 'test2.png';
```

## ノードの作成・挿入・削除

### ノードの作成・挿入

`appendChild` メソッドで、指定したノードを挿入します。

```javascript
// Element、Text ノードを作成
var element = document.createElement('div');
var text = document.createTextNode('test');

// ノードを挿入
element.appendChild(text);
document.body.appendChild(element);
```

### ノードの削除

`removeChild` メソッドで、指定したノードを削除します。

```html
<section>
  <div>test1</div>
  <div>test2</div>
</section>
```

```javascript
var div = document.getElementsByTagName('div')[1];
div.parentNode.removeChild(div);
```
