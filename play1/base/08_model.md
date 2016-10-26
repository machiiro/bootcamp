# モデル

Play! では、O/R マッパーとして Java Persistence API (JPA) を採用しているため、
モデルクラスは JPA を用いて定義していきます。
なお、JPA 実装として Hibernate を採用しています。

## モデルクラスの要件

Play! におけるモデルは以下の要件を満たす必要があります。

- `@javax.persistence.Entity` アノテーションが付与されている
- `play.db.jpa.Model` を継承する
    - 厳密には必須要件ではない
    - ID フィールドが自動付与される、便利なヘルパーメソッドが使えるなどのメリットがあるので、基本は継承すること

## モデルクラスの定義

モデルクラスを定義する場合は、以下のように記述します。

```java
@Entity
public class User extends Model {

    public String name;
    public String email:

}
```

Play! では、フィールドの getter/setter を明示的に記述せず、public なフィールドとして定義しておくと、
実際に動作する際に、Play! が自動的に getter/setter を付与します。

つまり、実際に動作する場合は以下のコードの状態となっています。

```java
@Entity
public class User extends Model {

    public String name;
    public String email:

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name
    }

    ...

}
```

明示的に getter/setter を定義した場合、Play! は getter/setter を自動生成せず、そちらのメソッドを利用する動きになります。

## モデルの CRUD

`play.db.jpa.Model` を継承しておくことで、モデルの CRUD (Create, Read, Update, Delete) 操作を簡単に行うことが可能です、

```java
// 検索
User. findById(1L);
User.find("name", "yamada").fetch();

User user = new User();

// 登録 or 更新
user.save();

// 削除
user.delete();
```
