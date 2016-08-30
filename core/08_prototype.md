# プロトタイプ

Java や C++ 等ではクラスベースで継承をサポートしていますが、JavaScript にはクラスという概念がなくオブジェクトしか登場しません。
代わりに JavaScript ではプロトタイプをベースとした継承を行います。

プロトタイプとは、オブジェクトAが参照している別のオブジェクトBのことを指します。
オブジェクトAは、参照している別のオブジェクトAの特性 (メソッド) を利用することができます。

- [最強オブジェクト指向言語 JavaScript 再入門！](http://www.slideshare.net/yuka2py/javascript-23768378)

## プロトタイプチェーン

それでは具体的な例を見ていきます。

```javascript
var objA = {
  name: 'yamada',
  hello: function() {
    console.log('Hello, ' + this.name);
  }
};
objA.hello(); // 'Hello, yamada'

objB = {};
objB.__proto__ = objA;
objB.hello(); // 'Hello, yamada'
```

objB のプロパティ `__proto__` に objA を指定した結果、objA の `hello` メソッドを呼び出すことができました。
これは、objB にプロパティ `hello` が存在しない場合に `objA` のプロパティを探索する、という動きをしているためです。
この動きのことを `プロトタイプチェーン` と呼びます。

ちなみに `__proto__` という名称は標準化されている仕様ではありません。
この名称を前提としてコーディングすると特定の環境で動作しない可能性があります。

## コンストラクタを用いたプロトタイプ継承

コンストラクタを用いてオブジェクトを生成すると、`Function.prototype` に格納されたオブジェクトが生成されたオブジェクトの `__proto__` に格納されます。
結果として前述のプロトタイプチェーンが実現されます。


```javascript
var ObjBase = function(name) {
  this.name = name;
}
ObjBase.prototype = {
  hello: function() {
    console.log('Hello, ' + this.name);
  }
}

var obj = new ObjBase('yamada');
obj.hello(); // 'Hello, yamada'
console.log(obj.__proto__); // { hello: [Function: hello] }
```
