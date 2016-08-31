# タイマー

タイマー関数を使用することで、指定した時間経過後に任意の関数を実行することができます。

## setTimeout - 指定時間経過後に一度だけ呼び出される

`setTimeout` の第1引数に関数、第2引数に経過時間 (ms) を指定します。

```JavaScript
// 2秒後に実行
var timerId = setTimeout(function() {
  // 処理を記述...
}, 2000);

// 実行をキャンセル
clearTimeout(timerId);
```

ちなみに経過時間を `0` にしても、関数は即時実行されるわけではありません。  
タイマー関数に指定した関数は、実行キューに「できるだけ早く」実行されるよう配置されます。

## setInterval - 指定時間経過の度に関数が呼び出される

引数の指定方法は `setTimeout` と同様です。

```JavaScript
// 5秒間隔で実行
var timerId = setInterval(function() {
  // 処理を記述...
}, 5000);

// 実行をキャンセル
clearInterval(timerId);
```
