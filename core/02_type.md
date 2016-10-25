# データ型

JavaScript には、プリミティブ型とオブジェクト型という2種類のデータ型があります。

## プリミティブ型

### 数値

JavaScript では整数と浮動小数点を区別せず、数値として統一的に扱います。

```javascript
12;
3.4;
```

### 文字列

文字列は、ダブルクォートかシングルクォートで囲んで表記します。

```javascript
"abcd";
'efgh';
```

### 真偽値

`true`、`false` という予約語を使って表現します。

```javascript
true
false
```

### null/undefined

`null` は "値が存在しない" ことを表します。
一方、`undefined` は "定義されていない" ことを表します。

## オブジェクト型

### Object

JavaScript においてあらゆるデータの基礎となるものがオブジェクトです。
オブジェクトには、キーと値を `key: value` 形式で表現することができます。
オブジェクトについては次章以降で説明します。

```javascript
{name: 'abc'}
```

### Array

`[]` リテラルで配列を表現することができます。
配列の要素にはプリミティブ型でもオブジェクト型でも指定することが可能です。
配列については次章以降で説明します。

```javascript
[1, 2, 3]
[{name: 'a'}, {name: 'b'}, {name: 'c'}]
```

### Date

日付と時刻を表現するオブジェクトを生成するために、`Date()` コンストラクタが用意されています。

```javascript
// 2010/1/1
new Date(2010, 0, 1);
```

### RegExp

正規表現を表すオブジェクトを生成するために、`RegExp()` コンストラクタが用意されています。

```javascript
new RegExp('abcd');
```

`/.../` リテラルを使って表現することも可能です。

```javascript
/abcd/;
```

### Function

関数オブジェクトを生成するために、`function` 文が用意されています。
関数については次章以降で説明します。

```javascript
function hello(name) {
  console.log('Hello, ' + name);
}
```

関数名を指定せず、関数オブジェクトを変数に代入することも可能です。
このような関数を無名関数と呼びます。

```javascript
var hello = function(name) {
  console.log('Hello, ' + name);
}
```

## typeof 演算子

値に対して typeof 演算子を指定することで、データ型を表す文字列を取得することが可能です。

```javascript
console.log(typeof 'abc'); // 'string'
```

| x | typeof x |
| --- | --- |
| undefined | "undefined" |
| null | "object" |
| true, false | "boolean" |
| 数値 | "number" |
| 文字列 | "string" |
| 関数 | "function" |
| Object | "object" |
| Array | "object" |
| Date | "object" |
| RegExp | "object" |
| Function | "function" |

## 型の変換

JavaScript では、if 文の条件式のような論理値が必要な場面などで、値の型を自動的に変換する動きをします。
特に値から論理値へ変換する動きは抑えておきましょう。

```javascript
var num = 2 * "3";
console.log(num);

if ("") {
  console.log('true');
} else {
  console.log('false');
}
```

| 値 | 論理値 |
| --- | --- |
| undefined | false |
| null | false |
| "" | false |
| "abc" | true |
| 0 | <font color="red">false</font> |
| -1 | true |
| 1 | true |
| {} | true |
| [] | true |
