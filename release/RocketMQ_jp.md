# Apache RocketMQ 紹介
## 概要

Apache RocketMQは高パフォーマンス、高信頼性、兆規模の容量、柔軟なスケーラビリティを持つ分散メッセージングシステムおよびストリーミングメディアプラットフォームである。Apache RocketMQの重要な特徴の一つは、非ログタイプの信頼性の高いメッセージング転送で、金融および電子商取引の分野での応用に非常に適切している。現在、Apache Software Foundationのトッププロジェクトであり、世界中に100社以上企業がオープンソースバージョンのRocketMQを業務に使用している。

## 誕生

RocketMQはアリババ社から発源されていた。 当初、アリババはビジネスニーズのためメッセージ指向ミドルウェアを要としていた。Notify、ActiveMQなどが使用されたが、ニーズが継続的に膨張しつつあり、ActiveMQ IOモジュールにボトルネックが発生していた。いくつかの努力を重ねたが著しい改善が認めされなかった。当時、Kafkaの流行度が高まっていることに気づき、アリババ開発チームがKafkaの無限のメッセージ蓄積と効率的な持続速度の機能を興味深く注目していた。残念ながら、そのままKafkaを使うことが不可能だと判断した。低遅延、高信頼性、そのに点の要求に満たすことができないのが致命的であった。いろいろ考えた上、アリババ開発チームが従来のパブリッシュ/サブスクライブ解決策から大量のリアルタイムゼロトレランストレーディングシステムまで、幅広いユースケースを処理する新しいメッセージ指向ミドルウェアを発明することを決定した。

## マイルストーン

2012年、アリババはRocketMQの開発を開始し、何回も「天猫ダブルイレブン」ショッピングフェスティバル(以下「ダブルイレブン」)の莫大送信量を完璧に乗り越えた。

2016年11月11日当日、RocketMQは再度「ダブルイレブン」で1.2兆の並行性オンラインメッセージ送信を処理した。その後、アリババがRocketMQをApache Incubatorに寄付した。

2017年9月25日-Apache Software Foundation、及び350を超えたオープンソースプロジェクトのすべてのボランティア、開発者、マネージャー、Apache Incubator組織は、Apache®RocketMQ™がApache Incubatorからトップレベルプロジェクトへの卒業を発表した。該当プロジェクトとコミュニティは、ASFのエリートプロセスと原則に従って適切に管理されたことを表している。 [参照]（https://blogs.apache.org/foundation/entry/the-apache-software-foundation-announces18）

## RocketMQの技術概要

RocketMQ最大の革新は、巧妙な水平、垂直拡張を通し、日々増えていく高スループット、高信頼性、低遅延のニーズに継続的に満たすことである。

RocketMQは、下図に示すように、主にNameServer、Broker、Producer、Consumer 4つの部分で構成されている。
![](http://img3.tbcdn.cn/5476e8b07b923/TB1FUR8PVXXXXbbXpXXXXXXXXXX)

NameServerは、発見とルーティングのライトサービスを提供する。各NameServerは、すべてのルーティング情報を保有し、読み、書きサービスを平等に提供する。容量を素早く拡張、縮小することをサポートしている。

Brokerはメッセージの格納機能を果たしている。Topicを緯度として軽量キューを実現したり、シングルマシンで数万のキューを実現したり、メッセージのプッシュ、プルモデルを実現したりすることができる。さらに、バックアップでエラーから回復する仕組み、ピークカット仕組み、億桁のメッセージ蓄積能力も備えている。その上、メッセージの順序の厳密性を保証できる。それ以外、Brokerは、他所の災害復旧機能、充実なメトリック統計、および警報機能も提供している。これらは、従来のメッセージ指向ミドルウェアの能力に及べないといわれている。

Producerはユーザーによって分散方式でデプロイされ、さまざまな負荷分散モードを介してBroker集群にメッセージを送信する。低遅延および高速失効機能サービスを提供している。

Consumerもユーザーによってデプロイされ、PUSHとPULLの2つの消費モード、クラスター消費とブロードキャスト消費もサポートしている。リアルタイムのサブスクライブサービスを提供し、ほとんどの消費シーンに満足することができる。

## 長所

* 非同期リアルタイムフラッシュディスク、同期フラッシュディスク、同期レプリケーション、非同期レプリケーション機能を持っている。それに、高い信頼性のためオペレーティングシステムのクラッシュによるデータを損失することはない。
* 一連の実践と最適化を経て、処理速度は最初の10,000TPSから50,000TPSを超えた。 
* Long pollingを使用し、メッセージ配信の遅延は通常数ミリ秒程度。
* シングルマシンでは最大50,000個のキューを蓄積しても、負荷はそれほど変化しない。
* 消費エラーの再試行機能はチャージ業務に非常に適切している。
* 厳密なメッセージ順序を守ることができる。Brokerがクラッシュしても、メッセージの配信が失敗するが、順序は乱れない。
* メッセージ配信の時間予約ができる。
* 分散トランザクションメッセージをサポートする。
* メッセージラベルまたは内容による検索ができる。
* 時間によるMessage Traceができる。精度はミリ秒。例えば、一日前の何時何分何秒から再度メッセージを消費するなど。

## その他のメッセージングミドルウェア

RabbitMQはAMQプロトコルでの実現であり、現在、OpenStack Iaasプラットフォームに最適なメッセージングサービスになっており、その背後にある支持はしっかりしている。

ActiveMQは元々LogicBlazeによって開発されたが、現在LogicBlazeは主にRed Hatを開発している。JMSプロトコルの実現で、Apacheのもとで高く評価されたメッセージングサービスエンジンである。 ActiveMQのエコシステムも豊富で、Apacheのトップレベルプロジェクトに、HornetMQから進化したArtemisや、次世代AMQとして知られるScalaに基づくApolloなど、多くのサブプロジェクトを持っている。

Kafkaはもともとログ処理用に設計されたもので、妥協のない大きなデータチャネルであり、高いスループットを求めている。開発チームは、現在中小企業をターゲットにしてビジネス用のバージョンの開発や宣伝に力を入れている。

以下の表は、RocketMQと人気あるな代替品の違いを比較するもの。

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