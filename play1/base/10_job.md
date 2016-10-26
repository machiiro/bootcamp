# ジョブ

## ジョブの要件

Play! におけるジョブは以下の要件を満たす必要があります。

- `play.jobs.Job` を継承する

## 起動・停止時に動作するジョブ

`@OnApplicationStart` アノテーションを付与することで、起動時に実行されるジョブを定義することができます。
データ初期化やセルフチェックなどを実装することが可能です。

```java
@OnApplicationStart
public class Bootstrap extends Job {

    public void doJob() {
        Logger.info("Application start.");
    }

}
```

`@OnApplicationStop` アノテーションを付与すると、停止時にジョブが実行されます。

## スケジューリングされたジョブ

ジョブを定期間隔で実行したい場合、`@Every` アノテーションを付与します。

```java
@Every("1h")
public class ScheduledJob extends Job {

    public void doJob() {
        Logger.info("Execute job.");
    }

}
```
