# 文法

## 変数の宣言

`var` キーワードを指定して宣言します。
行の最後には必ずセミコロンを付ける必要があります。

```javascript
// 値は undefined となる
var str1;

// 初期化
var str2 = 'abcd';
```

## 算術演算子

```javascript
// 加算
1 + 2;

// 減算
3 - 4;

// 乗算
5 * 6;

// 除算
7 / 8;

// 余り
9 % 2;

// インクリメント
i++;
++i; // 式評価より先にインクリメントが評価される

// デクリメント
i--;
--i; // 式評価より先にデクリメントが評価される
```

## 比較演算子

JavaScript では、等価演算子による比較を行うと、暗黙的に型変換が行われます。

```javascript
0 == "0" // true
1 == true // true
null == undefined // true
```

暗黙的な型変換を行わず、厳密に比較を行う場合は 厳密等価演算子(`===` `!==`) を指定します。
型変換を行わない分パフォーマンスにも優れるため、基本的には厳密等価演算子を利用することが推奨されます。

```javascript
0 === "0" // false
1 === true // false
null === undefined // false
```

また、等価演算子は論理を返すため、変数の代入にも使用できます。

```javascript
var bool = 1 == true;
```

## 論理演算子

```javascript
// AND
a === 1 && b === 2;

// OR
a === 1 || b === 2;
```

## 条件分岐

### if/elseif/else

```javascript
if (...) {

} else if (...) {

} else {

}
```

### switch/case

`break;` を指定しないと、次の case 文が評価されます。

```javascript
switch (...) {
case 'a':
  break;
case 'b':
  break;
default:
  break;
}
```

## ループと反復処理

### for

`for (初期化式; 条件式; 増分式)` というフォーマットで記述します。

for ループ内で `continue` が実行されると、ループ内の処理がスキップされて条件式が評価されます。
処理を中断して次のループ処理を行わせたい場合に指定します。

`break` が実行されると for ループを抜けて次の文に移行します。

```javascript
for (var i = 0; i < 10; i++) {
  if (...) {
    continue;
  }
  if (...) {
    break;
  }
}
```

オブジェクトのプロパティをループさせる場合は、`for-in` ループ文を使用します。

```javascript
var obj = {name: 'abcd'};
for (var name in obj) {
  console.log(name + ' = ' + obj[name]);
}
```

### while

条件式の評価が true となる場合、ループ処理が実行され続けます。

```javascript
var i = 0;
while (i < 10) {
  i++;
}
```

## コメント

```javascript
// コメント

/* コメント */

/*
 * コメント
 */
```

## Strict モード

ECMAScript 5 から、Strict モード という JavaScript コードをより厳格にチェックするための機能が追加されました。
有効にするには以下のコードを記述します。

```javascript
"use strict";
```

strict モードにおける制約については、以下の URL を参考にしてください。

- [Strict モード](https://developer.mozilla.org/ja/docs/Web/JavaScript/Strict_mode)
