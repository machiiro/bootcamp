モジュールを用いることで、名前空間を衝突を防ぎながら、コードを分割することが可能です。2017年4月現在、ブラウザで利用するには Webpack 等のビルドツールが必要となります。

## export

モジュールを提供する側は、`export` キーワードで提供するインタフェースを定義します。

```javascript
// オブジェクトを提供
export default {
}

// 関数を提供
export default () => {
}

// クラスを提供
export default class Car {
}
```
## import

モジュールを利用する側は、`import` キーワードで提供するインタフェースを定義します。

```javascript
import './module';
```

読み込んだ関数やクラスを利用する場合は、以下のように変数に格納します。

```javascript
import Module from './module';
Module.run();
```
