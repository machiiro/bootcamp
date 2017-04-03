## クラス構文

ES5 でオブジェクト指向プログラミングを実現するのは面倒で直感的ではありませんでしたが、ES2015 では新たにクラス構文が追加され、以下のように簡単にクラスを定義することが可能となりました。

```javascript
class Car {

  run() {
    console.log('running!');
  }

}
```

`Car` のインスタンスを生成するには `new` キーワードを使用します。

```javascript
new Car().run();
```

インスタンスの初期化処理を定義するには `constructor` 関数を定義します。`this` はインスタンス自体を指します。

```javascript
class Car {

  constructor(name) {
    this.name = name;
  }

  run() {
    console.log(`${this.name} is running!`);
  }

}

new Car('porsche').run();
```

## アクセサプロパティ

`get`、`set` キーワードを用いて、クラスのフィールドにアクセスするためのアクセサプロパティを定義することができます。

```javascript
class Car {
  constructor(name) {
    this._name = name;
  }

  get name() {
    console.log('get');
    return this._name;
  }

  set name(name) {
    console.log('set');
    this._name = name;
  }
}

const car = new Car('porsche');
console.log(car.name);
car.name = 'benz';
console.log(car.name);
```

- getter/setter

## 継承

`extends` キーワードを用いてクラスの継承を行うことができます。同一の名称のメソッドが定義されている場合はオーバーライドされます。

```javascript
class Vehicle {
  run() {
    console.log('running');
  }
}

class Car extends Vehicle {
  run() {
    console.log('Car is running.');
  }
}

class MotorCycle extends Vehicle {
}

new Car().run();
new MotorCycle().run();
```
