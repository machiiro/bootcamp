# スコープ

変数や関数を利用できる範囲 (有効範囲) のことをスコープと呼びます。

## スコープの種類

- グローバル変数
    - プログラム内のどこからでも使用できる変数や関数
- ローカル変数
    - プログラム内の限られた範囲内でしか使用できない変数や関数

例えば、関数内で宣言された変数はローカル変数となり、同一名称のグローバル変数に存在していても、関数内ではローカル変数が参照されます。

```javascript
var scope = 'global scope';
var func = function() {
  var scope = 'local scope';
  console.log(scope); // 'local scope'
}

func();
console.log(scope); // 'global scope'
```

また、関数内に変数が見つからなかった場合は外側のスコープに変数を探しにいく動きをします。
この仕組みをスコープチェーンと呼びます。

```javascript
var scope = 'global scope';
var func = function() {
  console.log(scope); // 'global scope'
}

func();
console.log(scope); // 'global scope'
```

また、`func` のような定義した時点のスコープ (静的スコープ・レキシカルスコープと呼ぶ) を持った関数のことを `クロージャ` と呼びます。
JavaScript において、関数は全てクロージャと捉えることができます。

クロージャの例は、jQuery のイベント操作などでよく見かけます。

```javascript
var $this = $(this);
$this.click(function() {
  // $this への参照を持ったクロージャ
});
```

## 変数宣言時に var を用いなかった場合

変数宣言時に `var` キーワードをしていない場合、その変数はスコープチェーン上の開始のスコープに割り当てられます。
つまり通常はグローバル変数として宣言されます。
そのため、`var` 無しでの変数宣言は通常利用されません。

## 即時関数

以下のように記述することで、定義した関数をすぐに実行することができます。
関数内で参照する変数を、後続処理に影響を与えないようローカル変数として宣言するテクニックです。
jQuery プラグインのようなライブラリで利用されます。

```javascript
;(function() {
  var hello = function(name) {
    console.log('Hello, ' + name);
  }
  hello('yamada'); // 'Hello, yamada'
})();

hello('tanaka'); // ReferenceError: hello is not defined
```

## 変数のホスティング (巻き上げ)

JavaScript では、関数内で宣言される変数はスコープ内で宣言前に参照することが可能です。値は `undefined` となります。
このような動きをホスティングと呼びます。

```javascript
var scope = 'global';
var func = function() {
  console.log(scope); // undefined
  var scope = 'local';
  console.log(scope); // 'local'
}
func();
```

上記コードは下記コードと同じ意味になります。

```javascript
var scope = 'global';
var func = function() {
  var scope;
  console.log(scope); // undefined
  scope = 'local';
  console.log(scope); // 'local'
}
func();
```
