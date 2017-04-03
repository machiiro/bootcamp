## アロー関数

ES2015 では、アロー関数というシンタックスで無名関数を定義することが可能です。

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/arrow_functions

```javascript
// ES5
var add = function(a, b) {
  return a + b;
};

// ES2015
const add = (a, b) => {
  return a + b;
};

console.log(add(1, 2));
```

引数が1つの場合、括弧を省略することも可能です。

```javascript
const hello = name => {
  console.log(`Hello, ${name}`);
}
hello('taro');
```

通常の無名関数の場合、関数内の `this` の参照先は、「関数がどのようにして呼ばれたか」によって変化しますが、アロー関数では関数定義時の `this` を常に束縛します。

```javascript
'use strict';

const obj = {
  show: function () {
    console.log(this); //Object

    const funcA = function () {
      console.log(this); //undefined
    };

    funcA();

    const funcB = () => {
      console.log(this); //Object
    };

    funcB();
  }
};

obj.show();
```

## 引数

引数に関する様々な指定が可能となりました。

### デフォルト引数

```javascript
const add = (a, b = 2) => {
  return a + b;
}
console.log(add(1));
```

### 可変引数

```javascript
const add = (...v) => {
  return v.reduce((a, b) => { return a + b }, 0);
}
console.log(add(1, 2, 3));
```

### キーワード引数

```javascript
const add = ({x, y}) => {
  return x + y;
}
console.log(add({x: 1, y: 2}));
```

## 分割代入

関数の戻り値を複数返したり、戻り値の一部を受け取ったりすることが可能となりました。

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

```javascript
const func = () => {
  return [1, 2];
}

let a, b, c;

[a] = func();
console.log(a);

[b, c] = func();
console.log(b);
console.log(c);
```

オブジェクトのフィールドを変数として受け取ることも可能です。この書き方はライブラリの import などでよく見かけます。

```javascript
const func = () => {
  return {a: 1, b: 2};
}

let a, b, c;

({b, c} = func());
console.log(b);
console.log(c);
```

## 即時関数 (IIFE: Immediately invoked function expression)

ES5 で定義した関数を即時実行し、かつ変数スコープを限定させたい場合、以下のようなコードを記述していました。

```javascript
var a = 'foo';
var b = 'bar';

(function() {
  var a = 1;
  var b = 2;

  console.log(a + b); // 3
})();

console.log(a + b); // foobar
```

ES2015 では `{}` を使うことでブロックスコープを定義することが可能です。これで多くのケースで即時関数を利用せず書くことができます。

ただし、クロージャを戻り値として返したいケースなどでは、まだ即時関数を利用するケースはあります。

```javascript
const a = 'foo';
const b = 'bar';

{
  const a = 1;
  const b = 2;

  console.log(a + b); // 3
}

console.log(a + b); // foobar
```
