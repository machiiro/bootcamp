# Deferred

jQuery には非同期処理を扱うための Deferred というモジュールが用意されています。  

非同期処理が複数連結されるようなケースでは、いわゆるコールバック地獄と呼ばれるコーディングが必要となりますが、Deferred を利用することでシンプルに記述することが可能です。

前章で学んだ `$.get`、`$.post`、`$.ajax` は実はこの Deferred が利用されています。

- [Deferred Object](http://api.jquery.com/category/deferred-object/)

## 利用方法

`Deferred#promise` で Promise オブジェクトを返却し、呼び出し側に処理成功・失敗時に実行したい関数を登録してもらいます。

非同期処理が完了したら `Deferred#resolve` や `Deferred#reject` を実行すると、Promise オブジェクトの状態が変化し、登録されていたコールバック関数が呼び出される、という仕組みです。

```javascript
var func = function() {
  var deferred = $.Deferred();

  // setTimeout で非同期処理をエミュレート
  // 実際には $.ajax などの処理を行う
  setTimeout(function() {
    if (Math.random() > 0.5) {
      // 非同期処理を成功扱いとする
      deferred.resolve();
    } else {
      // 非同期処理を失敗扱いとする
      deferred.reject();
    }
  }, 1000);

  // Promise オブジェクトを返却 = 非同期処理の結果を返すことを約束する.
  return deferred.promise();
}

func()
  .then(function() {
    console.log('処理完了時に実行');
  })
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

## 直列実行

非同期処理を直列実行する場合、Deferred を利用しないとコールバック処理がネストしてしまいます。
このようなコーディングをコールバック地獄と呼びます。

```javascript
var func = function(callback) {
  setTimeout(function() {
    callback.call(this);
  }, 1000);
};

func(function() {
  console.log('success 1');
  func(function() {
    console.log('success 2');
    func(function() {
      console.log('success 3');
    });
  });
});
```

Deferred を利用すると以下のように記述することができます。

```javascript
var func = function(callback) {
  var deferred = $.Deferred();

  setTimeout(function() {
    deferred.resolve();
  }, 1000);

  return deferred;
};

func()
  .then(function() {
    console.log('success1');
    return func();
  })
  .then(function() {
    console.log('success2');
    return func();
  })
  .then(function() {
    console.log('success3');
  });
```

## 並列実行

`$.when` を利用すると、非同期処理を並列実行することが可能です。

```javascript
var func = function(callback) {
  var deferred = $.Deferred();

  setTimeout(function() {
    console.log('success');
    deferred.resolve();
  }, 1000);

  return deferred;
};

$.when(
  func(),
  func()
).done(function() {
  console.log('end');
});
```
