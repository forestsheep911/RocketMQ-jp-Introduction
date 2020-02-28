# Apache RocketMQ 紹介
## 概要
> Apache RocketMQは、低レイテンシ、高パフォーマンスと信頼性、1兆規模の容量、柔軟なスケーラビリティを備えた分散メッセージングおよびストリーミングメディアプラットフォームです。その重要な機能は、非ログタイプの信頼性の高いメッセージングをサポートすることです。これは、金融および電子商取引の分野での使用に非常に適しています。彼は現在、Apacheコミュニティのトッププロジェクトであり、世界中の100社以上の企業がオープンソースバージョンのRocketMQをビジネスに使用しています。

Apache RocketMQは高パフォーマンス、高信頼性、兆規模の容量、柔軟なスケーラビリティを持つ分散メッセージングシステムおよびストリーミングメディアプラットフォームである。Apache RocketMQの重要な特徴の一つは、非ログタイプの信頼性の高いメッセージング転送で、金融および電子商取引の分野での応用に非常に適切している。現在、Apache Software Foundationのトッププロジェクトであり、世界中に100社以上企業がオープンソースバージョンのRocketMQを業務に使用している。

## 誕生
> RocketMQはアリババから発信されました。 アリババは当初、ビジネスニーズのためにメッセージングミドルウェアを必要としていました。以前に使用されたNotify、ActiveMQなど。ただし、需要が継続的に拡大する場合、ActiveMQ IOモジュールにボトルネックが発生し、いくつかの努力を重ねた結果、改善結果は良くありませんでした。当時、Kafkaは人気があったため、アリババ開発チームの注目を集め、Kafkaの無限のメッセージ蓄積と効率的な持続速度の機能を高く評価しました。残念ながら、Kafkaは、特に低レイテンシと高信頼性の点で、要件を満たすことができません。この場合、アリババは、従来のパブリッシュ/サブスクライブスキームから大量のリアルタイムゼロロストレラントトレーディングシステムまで、幅広いユースケースを処理する新しいメッセージングエンジンを発明することを決定しました。

RocketMQはアリババ社から発源されていた。 当初、アリババはビジネスニーズのためメッセージ指向ミドルウェアを要としていた。Notify、ActiveMQなどが使用されたが、ニーズが継続的に膨張しつつあり、ActiveMQ IOモジュールにボトルネックが発生していた。いくつかの努力を重ねたが著しい改善が認めされなかった。当時、Kafkaの流行度が高まっていることに気づき、アリババ開発チームがKafkaの無限のメッセージ蓄積と効率的な持続速度の機能を興味深く注目していた。残念ながら、そのままKafkaを使うことが不可能だと判断した。低遅延、高信頼性、そのに点の要求に満たすことができないのが致命的であった。いろいろ考えた上、アリババ開発チームが従来のパブリッシュ/サブスクライブ解決策から大量のリアルタイムゼロトレランストレーディングシステムまで、幅広いユースケースを処理する新しいメッセージ指向ミドルウェアを発明することを決定した。

## マイルストーン
> 2012年、アリババはRocketMQの開発を開始し、いくつかの二重11コアトランザクションリンクインスペクションを実施しました。

> 2016年11月11日に、Rocketはアリババ Global Shopping Festivalで1.2兆の同時オンラインメッセージ送信を再び処理し、アリババはRocketMQをApache Incubatorに寄付しました。

> 2017年9月25日-Apache Software Foundationは、350を超えるオープンソースプロジェクトのすべてのボランティア、開発者、マネージャー、およびインキュベーションプロジェクト組織とともに、Apache IncubatorからトップレベルプロジェクトへのApache®RocketMQ™の卒業を発表しました。プロジェクトのコミュニティと製品は、ASFのエリートプロセスと原則に従って適切に管理されています。 [参照]（https://blogs.apache.org/foundation/entry/the-apache-software-foundation-announces18）

> 今日、Apache RocketMQはコミュニティのあらゆる努力で繁栄しており、多くの機能が強化されています。

2012年、アリババはRocketMQの開発を開始し、何回も「天猫ダブルイレブン」ショッピングフェスティバル(以下「ダブルイレブン」)を完璧に乗り越えた。

2016年11月11日当日、RocketMQは再度「ダブルイレブン」で1.2兆の並行性オンラインメッセージ送信を処理した。その後、アリババがRocketMQをApache Incubatorに寄付した。

2017年9月25日-Apache Software Foundation、及び350を超えたオープンソースプロジェクトのすべてのボランティア、開発者、マネージャー、Apache Incubator組織は、Apache®RocketMQ™がApache Incubatorからトップレベルプロジェクトへの卒業を発表した。該当プロジェクトとコミュニティは、ASFのエリートプロセスと原則に従って適切に管理されたことを表している。 [参照]（https://blogs.apache.org/foundation/entry/the-apache-software-foundation-announces18）

## RocketMQの技術概要
> 私たちの意見では、最大の革新は、絶妙な水平および垂直拡張により、高スループット、高信頼性、低遅延の要件を継続的に満たす能力にあります。

RocketMQ最大の革新は、巧妙な水平、垂直拡張を通し、日々増えていく高スループット、高信頼性、低遅延のニーズに継続的に満たすことである。

> 現在、RocketMQは、下図に示すように、主にNameServer、Broker、Producer、およびConsumerの4つの部分で構成されています。

RocketMQは、下図に示すように、主にNameServer、Broker、Producer、Consumer 4つの部分で構成されている。
![](http://img3.tbcdn.cn/5476e8b07b923/TB1FUR8PVXXXXbbXpXXXXXXXXXX)


>NameServerは、サービス検出およびルーティング機能を軽量に提供し、各NameServerは、すべてのルーティング情報を保存し、ピアツーピアの読み取りおよび書き込みサービスを提供し、迅速な拡張と縮小をサポートします。

NameServerは、発見とルーティングのライトサービスを提供する。各NameServerは、すべてのルーティング情報を保有し、読み、書きサービスを平等に提供する。容量を素早く拡張、縮小することをサポートしている。

>ブローカーはメッセージの格納を担当し、Topicを緯度として使用して軽量キューをサポートし、1台のマシンで数万のキューをサポートでき、メッセージのプッシュプルモデルをサポートします。 1億のメッセージスタッキング機能と、同時にメッセージの順序を厳密に保証できます。さらに、Brokerは、都市内の災害復旧機能、豊富なメトリック統計、およびアラームメカニズムも提供します。これらは、従来のメッセージングシステムとは比較になりません。

Brokerはメッセージの格納機能を果たしている。Topicを緯度として軽量キューを実現したり、シングルマシンで数万のキューを実現したり、メッセージのプッシュ、プルモデルを実現したりすることができる。さらに、バックアップでエラーから回復する仕組み、ピークカット仕組み、億桁のメッセージ蓄積能力も備えている。その上、メッセージの順序の厳密性を保証できる。それ以外、Brokerは、他所の災害復旧機能、充実なメトリック統計、および警報機能も提供している。これらは、従来のメッセージ指向ミドルウェアの能力に及べないといわれている。

> プロデューサーはユーザーによって分散方式でデプロイされ、プロデューサーはさまざまな負荷分散モードを介してブローカークラスターにメッセージを送信し、低遅延および高速障害サポートを提供します。

Producerはユーザーによって分散方式でデプロイされ、さまざまな負荷分散モードを介してBroker集群にメッセージを送信する。低遅延および高速失効機能サービスを提供している。

> 消費者もユーザーによって展開され、PUSHとPULLの2つの消費モードをサポートし、クラスター消費とブロードキャストメッセージをサポートし、ほとんどの消費シナリオに対応するリアルタイムメッセージサブスクリプションメカニズムを提供します。

Consumerもユーザーによってデプロイされ、PUSHとPULLの2つの消費モード、クラスター消費とブロードキャスト消費もサポートしている。リアルタイムのサブスクライブサービスを提供し、ほとんどの消費シーンに満足することができる。

## 長所
> * RocketMQは、非同期リアルタイムフラッシュディスク、同期フラッシュディスク、同期レプリケーション、非同期レプリケーションをサポートしています。高い信頼性。オペレーティングシステムのクラッシュによるデータの損失はありません。
* RocketMQは一連の実践と最適化を経ており、処理速度は最初の10,000TPSから50,000TPSを超えました。 TPSの比較はKafkaの100万レベルほどではありませんが、トランザクションをサポートするメッセージミドルウェアではすでに非常に優れています。
* RocketMQは長いポーリングを使用し、メッセージ配信の遅延は通常数ミリ秒程度です。
* RocketMQシングルマシンは最大50,000個のキューをサポートし、負荷はそれほど増加しません。
* RocketMQは、消費エラーの再試行をサポートしており、この機能は充電アプリケーションに非常に適しています。
* RocketMQは厳密なメッセージ順序をサポートします。ブローカーがダウンした場合でも、メッセージ配信は失敗しますが、順序が狂うことはありません。
* RocketMQはタイミングメッセージをサポートします
* RocketMQは分散トランザクションメッセージをサポートします
* RocketMQは、メッセージIDまたはコンテンツに基づいたクエリをサポートしています。
* RocketMQは、特定の時間、1分、および1秒前のメッセージの再消費など、ミリ秒の精度で、時間に応じた連続したメッセージをサポートします。

* 非同期リアルタイムフラッシュディスク、同期フラッシュディスク、同期レプリケーション、非同期レプリケーション機能を持っている。それに、高い信頼性のためオペレーティングシステムのクラッシュによるデータの損失はありません。
* 一連の実践と最適化を経て、処理速度は最初の10,000TPSから50,000TPSを超えた。 
* Long pollingを使用し、メッセージ配信の遅延は通常数ミリ秒程度。
* RocketMQシングルマシンは最大50,000個のキューをサポートし、負荷はそれほど増加しません。
* RocketMQは、消費エラーの再試行をサポートしており、この機能は充電アプリケーションに非常に適しています。
* RocketMQは厳密なメッセージ順序をサポートします。ブローカーがダウンした場合でも、メッセージ配信は失敗しますが、順序が狂うことはありません。
* RocketMQはタイミングメッセージをサポートします
* RocketMQは分散トランザクションメッセージをサポートします
* RocketMQは、メッセージIDまたはコンテンツに基づいたクエリをサポートしています。
* RocketMQは、特定の時間、1分、および1秒前のメッセージの再消費など、ミリ秒の精度で、時間に応じた連続したメッセージをサポートします。

## その他のメッセージングミドルウェア

> RabbitMQはAMQP仕様のリファレンス実装であり、AMQPは包括的で非常に体系的でわずかに複雑なラインレイヤープロトコルです。現在、RabbitMQはOpenStack Iaasプラットフォームに最適なメッセージングサービスになっており、その背後にあるサポートは自明です。

> ActiveMQは元々LogicBlazeによって開発されましたが、現在は主にRed Hatを開発しており、JMS仕様のリファレンス実装であり、Apacheの下での古いスタイルのメッセージングサービスエンジンです。 JMSはAPIレベルのプロトコルですが、まだいくつかの実装上の制約を定義していますが、多言語のサポートはありません。このApacheトップレベルプロジェクトには、HornetMQから進化したArtemisや、次世代AMQとして知られるScalaに基づくApolloなど、多くのサブプロジェクトがあります。

> Kafkaはもともとログ処理用に設計されたもので、妥協のない大きなデータチャネルであり、高いスループットとメッセージ損失の可能性を追求しています。また、その背後にある研究開発チームは、現在中小企業で広く使用されているカフカ周辺の商業パッケージを実施しています。

> 以下の表は、RocketMQとその最も一般的な代替品の違いをすばやく発見するためのクイックリファレンスです。

RabbitMQはAMQP仕様のリファレンス実装であり、AMQPは包括的で非常に体系的でわずかに複雑なラインレイヤープロトコルです。現在、RabbitMQはOpenStack Iaasプラットフォームに最適なメッセージングサービスになっており、その背後にあるサポートは自明です。

ActiveMQは元々LogicBlazeによって開発されましたが、現在は主にRed Hatを開発しており、JMS仕様のリファレンス実装であり、Apacheの下での古いスタイルのメッセージングサービスエンジンです。 JMSはAPIレベルのプロトコルですが、まだいくつかの実装上の制約を定義していますが、多言語のサポートはありません。このApacheトップレベルプロジェクトには、HornetMQから進化したArtemisや、次世代AMQとして知られるScalaに基づくApolloなど、多くのサブプロジェクトがあります。

Kafkaはもともとログ処理用に設計されたもので、妥協のない大きなデータチャネルであり、高いスループットとメッセージ損失の可能性を追求しています。また、その背後にある研究開発チームは、現在中小企業で広く使用されているカフカ周辺の商業パッケージを実施しています。

以下の表は、RocketMQとその最も一般的な代替品の違いをすばやく発見するためのクイックリファレンスです。



| Messaging Product | Client SDK           | Protocol and Specification                           | Ordered Message                                                 | Scheduled Message | Batched Message                                 | BroadCast Message | Message Filter                                          | Server Triggered Redelivery | Message Storage                                                                                         | Message Retroactive                          | Message Priority | High Availability and Failover                                                 | Message Track | Configuration                                                                                                             | Management and Operation Tools                                  |
|-------------------|----------------------|------------------------------------------------------|-----------------------------------------------------------------|-------------------|-------------------------------------------------|-------------------|---------------------------------------------------------|-----------------------------|---------------------------------------------------------------------------------------------------------|----------------------------------------------|------------------|--------------------------------------------------------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| ActiveMQ          | Java, .NET, C++ etc. | Push model, support OpenWire, STOMP, AMQP, MQTT, JMS | Exclusive Consumer or Exclusive Queues can ensure ordering      | Supported         | Not Supported                                   | Supported         | Supported                                               | Not Supported               | Supports very fast persistence using JDBC along with a high performance journal，such as levelDB, kahaDB | Supported                                    | Supported        | Supported, depending on storage,if using kahadb it requires a ZooKeeper server | Not Supported | The default configuration is low level, user need to optimize the configuration parameters                                | Supported                                                       |
| Kafka             | Java, Scala etc.     | Pull model, support TCP                              | Ensure ordering of messages within a partition                  | Not Supported     | Supported, with async producer                  | Not Supported     | Supported, you can use Kafka Streams to filter messages | Not Supported               | High performance file storage                                                                           | Supported offset indicate                    | Not Supported    | Supported, requires a ZooKeeper server                                         | Not Supported | Kafka uses key-value pairs format for configuration. These values can be supplied either from a file or programmatically. | Supported, use terminal command to expose core metrics          |
| RocketMQ          | Java, C++, Go        | Pull model, support TCP, JMS, OpenMessaging          | Ensure strict ordering of messages,and can scale out gracefully | Supported         | Supported, with sync mode to avoid message loss | Supported         | Supported, property filter expressions based on SQL92   | Supported                   | High performance and low latency file storage                                                           | Supported timestamp and offset two indicates | Not Supported    | Supported, Master-Slave model, without another kit                             | Supported     | Work out of box,user only need to pay attention to a few configurations                                                   | Supported, rich web and terminal command to expose core metrics |

## ドキュメント参照

* [RocketMQ与Kafka对比（18项差异）](http://jm.taobao.org/2016/03/24/rmq-vs-Kafka/)
* [技术选型：RocketMQ or Kafka](https://zhuanlan.zhihu.com/p/60196818)
* [Apache Kafkaに入門した](https://deeeet.com/writing/2015/09/01/apache-Kafka/)
* [解决KafKa数据存储与顺序一致性保证](https://www.cnblogs.com/sunsky303/p/9511839.html)
* [Kafka : Ordering Guarantees](https://medium.com/@felipedutratine/Kafka-ordering-guarantees-99320db8f87f)
* [Apache Kafka 从 0.7 到 1.0：那些年我们踩过的坑](https://www.infoq.cn/article/MLMyoWNxqs*MzQX7lvzO)
* [Apache Kafkaの概要とアーキテクチャ](https://qiita.com/sigmalist/items/5a26ab519cbdf1e07af3)
* [Apache RocketMQ](https://rocketmq.apache.org/docs/quick-start/)
* [专访RocketMQ联合创始人：项目思路、技术细节和未来规划](http://jm.taobao.org/2017/03/03/RocketMQ-future-idea/)
* [The Apache Software Foundation Announces Apache® RocketMQ™ as a Top-Level Project](https://blogs.apache.org/foundation/entry/the-apache-software-foundation-announces18)
* [Apache RocketMQ开发者指南](http://www.itmuch.com/books/rocketmq/)
* [阿里RocketMQ是怎样孵化成Apache顶级项目的？](https://yq.aliyun.com/articles/364394)