## let / const

これまで変数の宣言には `var` を用いましたが、新たに `let` と `const` が追加されました。

`let` で宣言した変数は再代入を許可しますが、`const` は禁止します。そのため通常は `const` を利用していきます。


```javascript
let a = 1;
const b = 2;

a = 3;
b = 4; // Error
```

## テンプレートリテラル

これまで文字列と変数を連結したい場合は `+` 演算子で結合していましたが、新たにテンプレートリテラルが追加されました。バッククォートで囲んだ文字列はテンプレートとして処理されます。

```javascript
const name = 'taro';
console.log(`Hello, ${name}`);
```
