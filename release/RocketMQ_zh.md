# Apache RocketMQ 介绍

## 概要
Apache RocketMQ是一个分布式消息传递和流媒体平台，具有低延迟，高性能和可靠性，万亿级容量和灵活的可伸缩性。它的一个重要特性是支持非日志类型的可靠消息传送，非常适合运用在金融和电子商务领域。目前他是Apache社区的顶级项目，在全球有超过100家公司在其业务中使用RocketMQ的开源版本。

## 诞生
RocketMQ起源于阿里巴巴。阿里巴巴最初由于业务需求，需要使用消息中间件。早期使用过Notify，ActiveMQ等。但在需求不断膨胀的情况下，ActiveMQ IO模块遇到了瓶颈，几经努力但改善成果不佳。这时正值Kafka流行，于是引起了阿里巴巴开发团队的注意，对kafka的无限消息堆积，高效持久化速度等特性非常赞赏。但不幸的是，Kafka不能满足他们的要求，特别是在低延迟和高可靠性方面。在这种情况下，阿里巴巴决定发明一个新的消息传递引擎来处理更广泛的用例集，从传统的发布/订阅方案到大批量实时零损失容忍交易系统。

## 里程碑
2012年，阿里巴巴开始开发RocketMQ，经历了数次双11核心交易链路检验。

2016年11月11日，RocketMQ又一次在阿里巴巴全球购物节上处理了1.2万亿个并发在线消息传输，随后阿里巴巴将RocketMQ捐献给Apache Incubator。

2017年9月25日 – Apache软件基金会，连同350多个开源项目的全体志愿者、开发人员、管理人员、和孵化项目组织，宣布Apache®RocketMQ™从Apache孵化器毕业成为顶级项目，这表明该项目的社区和产品已根据ASF的精英流程和原则得到了很好的管理。[参见](https://blogs.apache.org/foundation/entry/the-apache-software-foundation-announces18)

现今，Apache RocketMQ在社区各方面的努力下，茁壮发展，很多功能都得到了加强。

## RocketMQ的技术概览
在我们看来，它最大的创新点在于能够通过精巧的横向、纵向扩展，不断满足与日俱增的海量消息在高吞吐、高可靠、低延迟方面的要求。

目前RocketMQ主要由NameServer、Broker、Producer以及Consumer四部分构成，如下图所示。
![](http://img3.tbcdn.cn/5476e8b07b923/TB1FUR8PVXXXXbbXpXXXXXXXXXX)

NameServer以轻量级的方式提供服务发现和路由功能，每个NameServer存有全量的路由信息，提供对等的读写服务，支持快速扩缩容。

Broker负责消息存储，以Topic为纬度支持轻量级的队列，单机可以支撑上万队列规模，支持消息推拉模型，具备多副本容错机制（2副本或3副本）、强大的削峰填谷以及上亿级消息堆积能力，同时可严格保证消息的有序性。除此之外，Broker还提供了同城异地容灾能力，丰富的Metrics统计以及告警机制。这些都是传统消息系统无法比拟的。

Producer由用户进行分布式部署，消息由Producer通过多种负载均衡模式发送到Broker集群，发送低延时，支持快速失败。

Consumer也由用户部署，支持PUSH和PULL两种消费模式，支持集群消费和广播消息，提供实时的消息订阅机制，满足大多数消费场景。

## 特点
* RocketMQ支持异步实时刷盘，同步刷盘，同步复制，异步复制。具有高可靠性。不会因为操作系统的崩溃而导致数据丢失。
* RocketMQ经过一系列的实践和优化，处理速度从最初的10,000TPS到目前已经超过50,000TPS。单纯比较TPS的话虽然还不如Kafka的百万级别，但在支持事务的消息中间件来说已经是非常优秀了。
* RocketMQ采用长轮询，消息投递延迟通常在几个毫秒左右。
* RocketMQ单机最高支持5万个队列，且负载不会发生明显递增。
* RocketMQ支持消费失败重试，这个特性非常适合运用在充值方面的应用。
* RocketMQ支持严格的意义上的消息顺序。即时在一台Broker宕机后，消息发送会失败，但是不会乱序。
* RocketMQ支持定时消息
* RocketMQ支持分布式事务消息
* RocketMQ支持根据消息标识或内容查询。
* RocketMQ支持按照时间来回溯消息，精度毫秒，例如从一天之前的某时某分某秒开始重新消费消息。


## 其他消息中间件

RabbitMQ是AMQP规范的参考实现，AMQP是一个线路层协议，面面俱到，很系统，也稍显复杂。目前RabbitMQ已经成为OpenStack Iaas平台首选的消息服务，其背后的支持力度不言而喻。

ActiveMQ最初主要的开发者在LogicBlaze，现在主要开发红帽，是JMS规范的参考实现，也是Apache旗下的老牌消息服务引擎。JMS虽说是一个API级别的协议，但其内部还是定义了一些实现约束，不过缺少多语言支撑。ActiveMQ的生态堪称丰富多彩，在该Apache顶级项目下，拥有不少子项目，包括由HornetMQ演变而来的Artemis，基于Scala号称下一代AMQ的Apollo等。

而Kafka最初被设计用来做日志处理，是一个不折不扣的大数据通道，追求高吞吐，存在丢消息的可能。其背后的研发团队也围绕着Kafka进行了商业包装，目前在一些中小型公司被广泛使用。

下表是一目了然的快速参考，可快速发现RocketMQ及其最受欢迎的替代产品之间的差异。

| Messaging Product | Client SDK           | Protocol and Specification                           | Ordered Message                                                 | Scheduled Message | Batched Message                                 | BroadCast Message | Message Filter                                          | Server Triggered Redelivery | Message Storage                                                                                         | Message Retroactive                          | Message Priority | High Availability and Failover                                                 | Message Track | Configuration                                                                                                             | Management and Operation Tools                                  |
|-------------------|----------------------|------------------------------------------------------|-----------------------------------------------------------------|-------------------|-------------------------------------------------|-------------------|---------------------------------------------------------|-----------------------------|---------------------------------------------------------------------------------------------------------|----------------------------------------------|------------------|--------------------------------------------------------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| ActiveMQ          | Java, .NET, C++ etc. | Push model, support OpenWire, STOMP, AMQP, MQTT, JMS | Exclusive Consumer or Exclusive Queues can ensure ordering      | Supported         | Not Supported                                   | Supported         | Supported                                               | Not Supported               | Supports very fast persistence using JDBC along with a high performance journal，such as levelDB, kahaDB | Supported                                    | Supported        | Supported, depending on storage,if using kahadb it requires a ZooKeeper server | Not Supported | The default configuration is low level, user need to optimize the configuration parameters                                | Supported                                                       |
| Kafka             | Java, Scala etc.     | Pull model, support TCP                              | Ensure ordering of messages within a partition                  | Not Supported     | Supported, with async producer                  | Not Supported     | Supported, you can use Kafka Streams to filter messages | Not Supported               | High performance file storage                                                                           | Supported offset indicate                    | Not Supported    | Supported, requires a ZooKeeper server                                         | Not Supported | Kafka uses key-value pairs format for configuration. These values can be supplied either from a file or programmatically. | Supported, use terminal command to expose core metrics          |
| RocketMQ          | Java, C++, Go        | Pull model, support TCP, JMS, OpenMessaging          | Ensure strict ordering of messages,and can scale out gracefully | Supported         | Supported, with sync mode to avoid message loss | Supported         | Supported, property filter expressions based on SQL92   | Supported                   | High performance and low latency file storage                                                           | Supported timestamp and offset two indicates | Not Supported    | Supported, Master-Slave model, without another kit                             | Supported     | Work out of box,user only need to pay attention to a few configurations                                                   | Supported, rich web and terminal command to expose core metrics |

## 文献参照

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