# 関数

一度の定義だけで、プログラムから何度も呼び出し実行することができるコードを関数と呼びます。
他の言語では「サブルーチン」や「プロシージャ」とも呼ばれます。

## 関数の定義

`function` キーワードを使って、名前を指定して定義します。
`()` の中には、関数が受け付ける引数をリストで定義することが可能です。

```javascript
function hello(name) {
  console.log('Hello, ' + name);
}
```

名前を指定せずに、変数に代入することで定義することも可能です。
このような関数を無名関数と呼びます。

```javascript
var hello = function(name) {
  console.log('Hello, ' + name);
}
```

`return` 文を指定すると、そこで関数の実行を中断し、式の値が関数の戻り値として返されます。

```javascript
function add(a, b) {
  return a + b;
}
```

関数内では引数の他に `this` キーワードで呼び出しコンテキストという値にアクセスできます。
これは関数の呼び出し方によって中身が異なるため、次項以降で説明していきます。

```javascript
function debug_this() {
  console.log(this);
}
```

## 関数の呼び出し

関数の呼び出し方法には、大きく4つの方法があります。

### 関数呼び出し

`()` キーワードで関数を呼び出します。

```javascript
hello('yamada'); // Hello, yamada
```

この時 `this` には、ECMAScript バージョン及び strict モードかどうかによって
グローバルオブジェクトまたは undefined が定義されます。
このような形で呼び出される関数内では、通常 `this` に対するアクセスは行いません。

### メソッド呼び出し

オブジェクトのプロパティに定義された関数のことをメソッドと呼びます。
`オブジェクトの変数名`.`プロパティ名` という形式で呼び出します。

```javascript
var obj = {
  name: '',
  hello: function() {
    console.log('Hello, ' + this.name);
  }
}

obj.name = 'yamada';
obj.hello(); // Hello, yamada
```

この時 `this` には、呼び出したオブジェクト自体が格納されます。
`this` と `obj` は同じオブジェクトとなるため、上記の例のように `this.name` とアクセスすることで `obj.name` の値を取得することができます。

### コンストラクタ呼び出し

`new` キーワードを使って、関数をコンストラクタ (初期化を行う関数) としてオブジェクトを生成することができます。

```javascript
var User = function(name, mailAddress) {
  // this には新たに生成されたオブジェクトが格納されている
  this.name = name;
  this.mailAddress = mailAddress;
}
Foo.prototype.say = function() {
  console.log('Hello, ' + this.name);
}

// user = {name: name, mailAddress: mailAddress}; とは書かない
var user = new Foo('yamada');
user.say(); // Hello, yamada
```

コンストラクタ内の `this` に新たに生成されるオブジェクトが格納されているため、オブジェクトの初期化処理を実装することができます。
`{}` リテラルでオブジェクトを生成するのではなく、コンストラクタを用いることで、よりオブジェクト指向なコーディングが可能です。

`prototype` に関しては次章以降で説明していきます。

### call/apply での呼び出し

JavaScript では、関数を `Function` というオブジェクトとして扱います。
`Function` には、`call` と `apply` という2つの関数自体を実行するメソッドが定義されています。
どちらも第1引数に `this` に格納するオブジェクトを指定することができます。

```javascript
var hello = function(name) {
  console.log('Hello, ' + name);
}

// call は関数の引数をベタに指定
hello.call(this, 'yamada');

// apply は関数の引数を配列で指定
hello.apply(this, ['yamada']);
```

## 関数の引数

関数の引数は `Arguments` オブジェクトとして `arguments` 変数に格納されます。
引数が可変である場合に利用します。

配列のように見えますが、実際には配列とは異なるオブジェクトであることに注意して下さい。

```javascript
var hello = function() {
  console.log(typeof arguments); // 'object'
  console.log(arguments[0]); // 'yamada'
}

hello('yamada');
```
