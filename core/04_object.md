# オブジェクト

JavaScript の基本となるデータ型がオブジェクトです。
複数のデータ値を1つにまとめて、名前によってデータ値を読み出したり書き換えたりできるようにするものです。

## オブジェクトの生成

オブジェクトを生成するための書き方には幾つかの種類があります。
特別な理由がない限り `{}` リテラルを使用しましょう。

```javascript
var obj1 = {};
var obj2 = new Object();
var obj3 = Object.create(Object.prototype);
```

## オブジェクトの読み書き

オブジェクトが持つプロパティに対して読み書きする場合は、ドット演算子または角括弧演算子を使用します。
他の言語を学んだことがある方は、これを見てオブジェクトがハッシュ・マップ・辞書・連想配列と呼ばれるものと同じものだと気付くかもしれません。

```javascript
var obj = {name: 'abcd'};

// 読み取り
console.log(obj.name);
console.log(obj['name']);

// 書き込み
obj.name = 'efgh';
obj['name'] = 'efgh';
```

## オブジェクトのプロパティの削除

オブジェクトのプロパティを削除する場合は、`delete` 演算子を使用します。

```javascript
var obj = {name: 'abcd'};

delete obj.name;
console.log(obj.name); // undefined
```

よくある勘違いとして、null を代入してもプロパティが削除されないので注意して下さい。

```javascript
var obj = {name: 'abcd'};

obj.name = null;
console.log(obj.name); // null
```
