@startuml

    title incident_bot テクニカルアーキテクチャ
    actor User

    cloud slack_team
    cloud heroku {
      node incident_bot_x
      note bottom of incident_bot_x
        herokuのpaasで
        自動並列化する
      end note
    }
    database report
    note bottom of report
      postgresqlを利用
      　
      レコードに対して
      多重更新は行われない
    end note


    User --> slack_team
    slack_team --> incident_bot_x
    incident_bot_x --> slack_team
    report --- incident_bot_x
    

/'

保存先はpostgresqlで、channel-category-messageのリレーションを作成する。
active-jobの実装であるsuccer-punchを使って遅延ジョブ実行を行えば良い。herokuではredisは使わなくても遅延ジョブは実行できるとのこと。

reportの保存先として、redisかpostgresqlか悩んでいる。
redisは応答性に富み、postgresqlは暗号性に富む。
プロトコルはHTTPSを使えるので、通信から漏洩はしない。
redis, postgresqlに直接接続された場合、漏洩するリスクを考える。

- redisはstunnel buildpackで、dynoとredisをつなぐ想定
  - https://devcenter.heroku.com/articles/securing-heroku-redis
- postgresqlは、private spaceでdynoとpostgresqlをWAFでつなぐが、コストが１０倍なので現実的ではない
  - ハットさん曰く

redisを使いたいと思う理由は、incident_bot自体を特定用途に限定しないと考えた場合、書き込み・参照で発生する膨大な遅延を回避できるのではないか？という打算から。

取り急ぎは１チーム：１インスタンス：ｎチャンネルのセットにして各チャンネルからの書き込み・参照を捌こうと考えている。書き込み・参照ならpostgresqlでもレプリケーションを行えるので300人程度の書き込み・参照なら、おそらく十分に耐えられるのではないか。

- HA構成(premium)が用意されているメリットもある。
- 用途上の都合からストレージ暗号化(premium)が用意されているメリットも高い。
- スナップショットに対するロールバック(standard)も復旧性の面でも心強い。
- レプリケーション(standard)は、[follower](https://devcenter.heroku.com/articles/heroku-postgres-follower-databases)という名前で作成可能。
- railsとは従来通りにActiveModelで操作可能。
- データの永続性については、ディスク容量に直接依存するので、ディスクフル時はアプリケーション側で対処する必要がある。

postgresqlの代わりにredisの利用を考えた場合、書き込み・参照の負荷耐性については速度計測を行っているブログ記事を見る限り、１万行・１０万行コミットにかかる時間は、postgresqlに較べて半分程。postgresqlと同等の環境であれば同等以上の性能を引き出せるのではないか。

- HA構成(premium)が用意されている。
- x 逆にストレージの暗号化は用意されていない。
- スナップショットに対するロールバック(premium)はこちらも用意されている。
- レプリケーションは？
  - HA構成(premium)の場合、`support@redistogo.com`にredis sentinelについて問い合わせれば詳細が得られる。
- railsとは[redis-objects](https://github.com/nateware/redis-objects)で間接的に操作可能。
- データの永続性については、メモリ容量に直接依存するが、既存データを削除して新規データを書き込む流れになる

'/

@enduml
