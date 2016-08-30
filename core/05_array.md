# 配列

値を順序付けてまとめたものを配列と呼び、個々の値を配列の要素と呼びます。

## 配列の生成

配列を生成する場合、基本的には `[]` リテラルを使用します。
`Array` コンストラクタで生成することも可能ですが、`[]` リテラルで生成した場合と同じ結果となります。

```javascript
var array1 = [];
var array2 = new Array();
```

配列の長さだけがあらかじめ決められる場合は、`Array` コンストラクタを使用します。

```javascript
var array = new Array(5);
```

配列の長さと要素があらかじめ決められる場合は、`[]` コンストラクタを使用します。

```javascript
var array = [1, 2, 3, 4, 5];
```

## 配列を参照

配列の長さを取得する場合は、`length` プロパティを参照します。

```javascript
console.log(array.length);
```

配列の要素を巡回する場合は、`forEach` メソッドを使用します。

```javascript
var array = [1, 2, 3, 4, 5];

// 以前の書き方
for (var i = 0; i < array.length; i++) {
  console.log(array[i]);
}

// forEach を使った書き方
array.forEach(function(item, index) {
  console.log('index: ' + index);
  console.log('item: ' + item);
});
```

## 要素の読み書き

特定の位置 (インデックスと呼ぶ) の要素に対して読み書きする場合は、`[]` 演算子を使用します。
インデックスは 0 からスタートします。

```javascript
var array = [1, 2, 3, 4, 5];

// 先頭の要素を取得
console.log(array[0]);

// 2番目の要素を変更
array[1] = 6;
console.log(array[1]);
```

## 要素の追加

配列の末尾に要素を追加する場合は `push` メソッドを使用します。

```javascript
var array = [];

array.push(1);
console.log(array);
```

## 要素の削除

配列の要素を削除する場合は、`delete` 演算子を使用します。
ただし、`delete` 演算子を実行しても配列の長さは変わらないことに注意しましょう。

```javascript
var array = [1, 2, 3];

delete array[1];
console.log(array.length);
console.log(array);
```

## 主要なメソッド

### join

配列の要素を、指定した文字列で連結します。

```javascript
var array = [1, 2, 3, 4, 5];

console.log(array.join(',')); // 1, 2, 3, 4, 5
```

### concat

指定した要素、配列を結合した新しい配列を生成します。
元の配列は変更されない点に注意して下さい。

```javascript
var array = [1, 2, 3];

console.log(array.concat(4, 5)); // 1, 2, 3, 4, 5
console.log(array.concat([4, 5])); // 1, 2, 3, 4, 5
```

### push/pop

`push` メソッドは、配列の末尾に要素を追加します。
`pop` メソッドは、配列の末尾の要素を削除し、要素を戻り値として返します。
これらのメソッドを使って、「先入れ後出し (first in, last out) スタック」を実現することができます。

- [スタック](https://ja.wikipedia.org/wiki/%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF)

```javascript
var array = [];

array.push(1, 2);
console.log(array.pop()); // 2
array.push(3);
console.log(array); // [1, 3]
console.log(array.pop()); // 3
console.log(array.pop()); // 1
```

### unshift/shift

`unshift` メソッドは、配列の先頭に要素を追加します。
`shift` メソッドは、配列の先頭の要素を削除し、要素を戻り値として返します。
前述の `push` と `shift` を利用して、「先入れ先出し (first in, first out) キュー」を実現することができます。

- [キュー](https://ja.wikipedia.org/wiki/%E3%82%AD%E3%83%A5%E3%83%BC_(%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF)

```javascript
var array = [];

array.push(1, 2);
console.log(array.shift()); // 1
array.unshift(3);
console.log(array); // [3, 2]
console.log(array.shift()); // 3
console.log(array.shift()); // 2
```

### slice

配列から、指定したインデックスの要素を抜き出します。
第1引数に開始インデックス、第2引数に終了インデックスを指定します。
引数を1つだけ指定した場合は、終了インデックスが配列の末尾となります。
元の配列は変更されない点に注意して下さい。

```javascript
var array = [1, 2, 3, 4, 5];

console.log(array.slice(0, 3)); // [1, 2, 3]
console.log(array.slice(3)); // [4, 5]
```
