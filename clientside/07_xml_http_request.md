# XMLHttpRequest

JavaScript から HTTP リクエストを送信するための API として XMLHttpRequest が提供されています。

名称に [XML](https://ja.wikipedia.org/wiki/Extensible_Markup_Language) という名前を含んでいますが、XML のみしか扱えないわけではありません。

また [Ajax](https://ja.wikipedia.org/wiki/Ajax) と混同しがちですが、Ajax は XMLHttpRequest API を用いたプログラミング手法のことを指します。

## GET リクエスト

```javascript
var request = new XMLHttpRequest();

// HTTP メソッド、URL を指定
request.open('GET', 'data.csv');

// GET はリクエストボディが無いため null を指定
request.send(null);
```

## POST リクエスト

POST リクエストの場合、リクエストパラメータを `application/x-www-form-urlencoded` 形式でエンコードする必要があります。  
エンコードには `encodeURIComponent` 関数を利用します。

```javascript
// エンコード処理を行う関数を定義
var encodeFormData = function(data) {
  if (!data) return '';
  var params = [];
  for (var name in data) {
    var key = encodeURIComponent(name.replace(' ', '+'));
    var value = encodeURIComponent(data[name].toString().replace(' ', '+'));
    params.push(key + '=' + value);
  }
  console.log(params.join('&'));
  return params.join('&');
}

var request = new XMLHttpRequest();

// HTTP メソッド、URL を指定
request.open('POST', 'login.php');

// リクエストヘッダ Content-Type を指定
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

// エンコードした文字列を send に指定
request.send(encodeFormData({name: 'foo'}));
```

## レスポンスのハンドリング

`send` する前に `onreadystatechange` にイベントハンドラを登録することで、HTTP レスポンスをハンドリングすることができます。
readyState の値によって、HTTP リクエストの状態を検知することができます。

```javascript
var request = new XMLHttpRequest();
request.open('GET', 'data.csv');

request.onreadystatechange = function() {
  // リクエストが完了し、HTTP ステータスコードが 200 の場合
  if (request.readyState === 4 && request.status === 200) {
    console.log(request.responseText);
  }
}
```

| readyState値 | 説明 |
| ------------ | --- |
| 0 | open が呼び出されていない |
| 1 | open が呼び出された |
| 2 | ヘッダを受け取った |
| 3 | レスポンスボディを受信中 |
| 4 | レスポンスの受信が完了した |
