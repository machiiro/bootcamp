## Map

Map はキーと値をペアで持つオブジェクトです。ES5 まではオブジェクトで表現していましたが、ES2015 から正式に Map というオブジェクトが追加されました。

オブジェクトでマップを表現する場合、以下のような課題がありました。

- オブジェクトにはプロトタイプがあるため、意図しないマッピングが生じる危険性がある
- オブジェクトでは、キーと値のペアがいくつあるのか簡単にわからない
- オブジェクトでは、キーに文字列かシンボルしか利用できない

```javascript
const map = new Map();

map.set('a', 1);

const key = {};
map.set(key, 'abc');
console.log(map.get(key));

console.log(map.size);
```

## Set

Set はデータの集合で重複を許しません。ES5 までは Set のようなデータを表現する場合、オブジェクトの値にブール値を用いたりして表現していましたが、ES2015 から正式に Set というオブジェクトが追加されました。

```javascript
// 本来 Set のデータ構造では値は不要だが、
// オブジェクトでしか表現できないので boolean 値などを値として入れる
const set = {};
set.foo = true;
```

```javascript
const set = new Set();
set.add(1);
set.add(2);
set.add(2);
console.log(set.size);
```
