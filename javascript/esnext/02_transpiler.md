## トランスパイラとは

<img src="img/02_01.png" width="300">

ES5 しかサポートされない環境でも ES2015 でコーディングするために、ES2015 のコードを ES5 で動作するコードに変換する「トランスパイラ」と呼ばれるツールが登場しました。

最も広く利用されているトランスパイラとして、Babel というツールがあります。

https://babeljs.io/

## Babel 環境のセットアップ

Babel を使って ES2015 のコードを ES5 のコードに変換しましょう。

以下のコマンドを実行し、Babel の実行に必要なライブラリをインストールします。
`babel-cli` は本来必須ではありませんが、動作確認用にインストールします。

```bash
$ npm init
$ npm install --save-dev babel-cli babel-preset-es2015 babel-plugin-transform-runtime
```

package.json の `scripts` に babel を実行するための定義を追記します。

```javascript
{
  ...

  "scripts": {
    "babel": "babel"
  }

  ...
}
```

Babel の設定ファイル `.babelrc` を `package.json` と同階層に配置して、ES2015 から ES5 に変換するためのの定義を記述します。

```javascript
{
  "presets": ["es2015"],
  "plugins": ["transform-runtime"]
}
```

次に ES2015 で記述した JS ファイル `index.js` を追加します。

```javascript
() => {
  Object.entries({foo: 'bar'})

  console.log('Hello world.');
}
```

Babel を実行し、ES5 のコードに変換されることを確認しましょう。

```bash
$ npm run babel index.js

> babel@1.0.0 babel /Users/mkudo/dev/sandbox/babel
> babel "test.js"

'use strict';

var _entries = require('babel-runtime/core-js/object/entries');

var _entries2 = _interopRequireDefault(_entries);

function _interopRequireDefault(obj) { return obj && obj.__esModule ? obj : { default: obj }; }

(function () {
  (0, _entries2.default)({ foo: 'bar' });

  console.log('Hello world.');
});
```

## その他のプリセット・ライブラリ

### babel-preset-latest

ES2015 だけではなく、ES2016 や ES2017 ... などの最新仕様を利用することが可能です。

### babel-preset-env

実行環境を定義するだけで、環境で利用可能な仕様を自動判定してライブラリを選定・コード変換を行ってくれます。

### babel-polyfill

`babel-plugin-transform-runtime` は、ES5 では本来利用できない Promise などのオブジェクトや Object#entries などのメソッドを、ES5 のコードで定義することで利用可能としています。

一方 `babel-polyfill` を利用すると、各オブジェクト・メソッドの実装自体を読み込むことで利用可能とします。
また、実行ブラウザが対象オブジェクト・メソッドを既に実装済みである場合、ネイティブ実装を利用してくれます。

そのため、`babel-plugin-transform-runtime` と比較するとパフォーマンスが高くなります。
