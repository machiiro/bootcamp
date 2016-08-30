# JavaScript とは

JavaScript は Netscape 社によって開発されたプログラミング言語です。
ブラウザには JavaScript インタプリタが搭載されており、主に Web サイトの振る舞いを記述するための言語として利用されてきました。

現在では、

- サーバーサイド (Node.js)
- タスクランナー (npm, gulp)
- デスクトップアプリケーション (Electron)

といったレイヤーでも使用されています。

- [Javascriptの歴史](http://qiita.com/a_rcsin/items/0a3c8c98c8d703c49a22)

## ECMAScript について

JavaScript の仕様は [Ecma International](http://www.ecma-international.org/default.htm) によって、ECMAScript として標準化されています。

現在の最新仕様は ECMAScript 2015 (通称 ES6) と呼ばれ、Chrome や Firefox といったモダンブラウザでは殆どの仕様が既に実装されています。
また、次の ECMAScript バージョンを ES.next と呼んだりします。

各環境における ECMAScript の実装状況については [ECMAScript compatibility table](http://kangax.github.io/compat-table/) で確認することができます。

ECMAScript は JavaScript のコア仕様であり、ここで定義されている API はどの環境でも利用することができます。
一方、ブラウザ環境のみでしか利用できない API もあるため注意が必要です。

- [ECMAScript の該当範囲](https://developer.mozilla.org/ja/docs/Web/JavaScript/JavaScript_technologies_overview)
- [ECMAScriptとは何か？](https://azu.github.io/slide-what-is-ecmascript/)

## 実行環境

JavaScript はエディタとブラウザさえあれば、実際に実行して確認してみることができます。
他にもオンラインで JavaScript を実行することができるサービスがあるので、本ブートキャンプの中でも利用してみてください。

- [JSFiddle](https://jsfiddle.net/)
- [repl.it](https://repl.it/languages/javascript)
