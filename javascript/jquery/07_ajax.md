# Ajax

jQuery には`XMLHttpRequest` を利用した通信処理をラップした API が用意されています。
これらを利用することで、簡単に非同期通信を行うことが可能です。

- [Ajax](http://api.jquery.com/category/ajax/)

## $.get / $.getJSON / $.post

GET リクエストを行う場合は `$.get`、POST リクエストを行う場合は `$.post` をを利用します。
第1引数に URL、第2引数にリクエストパラメータを指定します。

`$.get` や `$.post` を実行すると、通信完了時に実行したい関数を登録するためのオブジェクトが返却されます。
成功時は `done`、失敗時は `fail` を利用します。詳細は次章で説明します。

```javascript
$.get('https://www.google.co.jp', {q: 'machiiro'})
  .done(function() {
    console.log('処理成功時のみ実行');
  })
  .fail(function() {
    console.log('処理失敗時のみ実行');
  })
  .always(function() {
    console.log('常に実行');
  });
```

サーバーからのレスポンスが JSON の場合、`$.get` の代わりに `$.getJSON` を利用すると、レスポンスが JavaScript オブジェクトに変換されます。

```javascript
$.getJSON('https://www.google.co.jp').done(function(response) {
  console.log(typeof response); // object
});
```

## $.ajax

先ほど紹介した `$.get` 等はショートハンドと呼ばれ、リクエストに関する複雑な設定を行うことができません。

リクエストヘッダを指定するなど、細かな設定を行いたい場合は `$.ajax` を利用します。

```javascript
$.ajax({
  type: 'GET',
  url: 'https://www.google.co.jp',
  data: {q: 'machiiro'},
  headers: {
    'X-Requested-With': 'XMLHttpRequest'
  }
}).done(function() {
  console.log('success');
});
```

`$.ajaxSetup` を利用すると、`$.ajax` での指定を省略することができます。
どのリクエストでも指定する項目については `$.ajaxSetup` を利用すると良いでしょう。

```javascript
$.ajaxSetup({
  headers: {
    'X-Requested-With': 'XMLHttpRequest'
  }
});
```
