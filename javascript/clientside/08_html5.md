# HTML5 API

HTML5 によって、これまでブラウザで実現できなかった様々な課題を解決するための API が追加されました。

- Canvas (グラフィック)
- Geolocation (位置情報)
- History (履歴操作)
- WebWorker (Worker)
- WebStorage (ストレージ)
- File (ファイル操作)
- Video (動画)
- Audio (音声)

この章では、中でも利用頻度の高い API について紹介します。

## Geolocation

Geolocation API を使って現在位置を取得する際は、ユーザーの許可が必要となります。

```javascript
// 現在の位置情報を取得する
navigator.geolocation.getCurrentPosition(function(pos) {
  console.log(pos);
});

// 現在の位置情報を取得する、現在位置が変化する度に実行される
var id = navigator.geolocation.watchPosition(function(pos) {
  console.log(pos);
});

// watchPosition を中止する
navigator.geolocation.clearWatch(id);
```

## File

File API を用いて、ファイルを読みこんだり書き出したりすることが可能です。
最も典型的な利用シーンは、`type="file"` 要素から選択されたファイルにアクセスすることです。

```html
<input type="file" name="file" multiple />
```

```javascript
var file = document.getElementsByName('file')[0];
file.addEventListener('change', function() {
  Array.from(file.files).forEach(function(f) {
    var reader = new FileReader();
    console.log(f);
    reader.onload = function(e) {
      console.log(e.target.result);
    };
    reader.readAsBinaryString(f)
  });
});
```
