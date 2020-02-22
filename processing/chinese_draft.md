# RocketMQ 介绍

## 概要
Apache RocketMQ is a distributed messaging and streaming platform with low latency, high performance and reliability, trillion-level capacity and flexible scalability.

RocketMQ最初由阿里根据自身需求而打造，后捐献给了Apache。经过社区的发展成为了Apache的顶级项目。

~~RocketMQ是由阿里开发的消息中间件，开发灵感受到了Kafka的影响，吸取了很多Kafka的优点，并根据自身需求进行了改造和优化。RocketMQ的一个重要特性是支持非日志类型的可靠消息传送。目前广泛应用于阿里集团下各类产品中，在订单，交易，充值，流计算，消息推送等场景中起到了重要作用。~~

## RocketMQ开发动机
根据我们的研究，在使用越来越多的队列和虚拟主题的情况下，ActiveMQ IO模块遇到了瓶颈。我们尽力通过节流，断路器或降级来解决此问题，但效果不佳。因此，我们那时开始关注流行的消息传递解决方案Kafka。不幸的是，Kafka不能满足我们的要求，特别是在低延迟和高可靠性方面，请参阅此处以了解详细信息。

在这种情况下，我们决定发明一个新的消息传递引擎来处理更广泛的用例集，从传统的发布/订阅方案到大批量实时零损失容忍交易系统。

## 为什么选择RocketMQ？
RocketMQ具有低延迟，高性能，为电商金融领域添加了可靠重试、基于文件存储的分布式事务等特性，并做了大量优化。从2012年开始，经历了历次双11核心交易链路检验。2016年11月，阿里将RocketMQ捐献给Apache软件基金后，又经历数代社区发展壮大，在各项性能上又有很大提升，如今已成为Apache的顶级项目。现在，有超过100家公司在他们的业务中使用开源版的RocketMQ。

~~阿里集团下的淘宝原先就使用自己开发的Notify消息中间件，使用的是Mysql作为存储手段，但希望进一步优化存储部分。2011年初，Linkin开源了Kafka这个优秀的消息中间件，淘宝中间件团队在对Kafka做过充分Review之后，认为Kafka的无限消息堆积，高效持久化速度等特性非常优秀。但另一方面，Kafka主要定位于日志传输，但淘宝最常用的是和交易相关的一系列对事务完整性要求很高的业务。Kafka并不擅长这方面，所以阿里决定重新用Java编写一套新的中间件，命名为RocketMQ。~~

~~对于Kafka无法照搬和开发新中间件的具体考量如下：
* Kafka的业务应用场景主要定位于日志传输；对于复杂业务支持不够。
* 阿里很多业务场景对数据可靠性、数据实时性、消息队列的个数等方面的要求很高。
* Kafka针对海量数据，但是对数据的正确度要求不是十分严格。而阿里巴巴中用于交易相关的事情较多，对数据的正确性要求极高，Kafka不合适。~~
* ~~当业务成长到一定规模，采用开源方案的技术成本会变高.~~
* ~~开源方案无法满足业务的需要；旧版本、自开发代码与新版本的兼容都可能是问题；运维角度，Kafka使用 scala 编写，而阿里是java系。Kafka的后续维护是个问题。~~
* ~~阿里在团队、成本、资源投入等方面约束性条件几乎没有。~~

## 开源
~~这些年开源氛围越来越好，各大IT公司都纷纷将一些自研代码开源出来。2012年，阿里巴巴开源其自研的第三代分布式消息中间件——RocketMQ。经过几年的技术打磨，阿里称基于RocketMQ技术，目前双十一当天消息容量可达到万亿级。
2016年11月，阿里将RocketMQ捐献给Apache软件基金会，正式成为孵化项目。~~

RocketMQ于2012年起源于阿里巴巴，在11月11日阿里巴巴全球购物节上处理了1.2万亿个并发在线消息传输后，于2016年11月捐赠给Apache Incubator。ApacheRocketMQ v4.0.0于2017年2月发布。

Forest Hill, MD –25 September 2017– The Apache Software Foundation (ASF), the all-volunteer developers, stewards, and incubators of more than 350 Open Source projects and initiatives, announced today that Apache® RocketMQ™ has graduated from the Apache Incubator to become a Top-Level Project (TLP), signifying that the project's community and products have been well-governed under the ASF's meritocratic process and principles.

 2017年9月25日 – Apache软件基金会（ASF）是350多个开源项目和计划的全志愿者开发人员，管理人员和孵化器，宣布Apache®RocketMQ™从Apache孵化器毕业成为顶级项目（TLP），这表明该项目的社区和产品已根据ASF的精英流程和原则得到了很好的管理。
 
此条新闻具体参见：
[The Apache Software Foundation Announces Apache® RocketMQ™ as a Top-Level Project](https://blogs.apache.org/foundation/entry/the-apache-software-foundation-announces18)
 
>目前国内外有很多公司会把一些通用问题的解决方案，尤其是那些久经考验、愈久弥坚的产品开源出来，以期望在品牌宣传、人才引进方面有所建树。把RocketMQ开源出来，甚至捐赠给Apache，内部也是经过了深思熟虑，层层审批与讨论，期望能够在生态化、规范化、国际化、商业化方面深耕细作。

>开源捐赠的想法实际上始于2014年。当时，我们甄选了几位Apache社区权威人士，遗憾的是反复沟通不断修改草案之后突然间失去了联系。2015年，我们有幸结识了Kylin Principal Architect蒋旭和VP Luke以及RedHat Principal Software Engineer姜宁，请教了一些Apache禁忌事项，重新活跃起来了捐赠进程。接下来，最重要的是征集champion候选人，很开心的是ActiveMQ VP Bruce爽快地接收了我们的邀请，经过前前后后接近100封邮件来往，我们终于正式开启了Apache之旅。捐赠投票是在双十一当天，我们准备充分很好地回答了评委会的犀利问题。不过，面对“中国开发者不喜欢邮件沟通”突然刁难，还要感谢社区华人的防御性声明回应。经过很多磨难，投票结果总算出来了：还不算坏10票赞同，带binding（IPMC成员的有效投票）的+1，无反对票，正式进入孵化期。孵化成功后有望成为国内首个互联网中间件在Apache上的顶级项目，成为全球继ActiveMQ，Kafka之后，分布式消息引擎家族中的重要成员。

>接下来，我们想强调下知识产权这个对大多数工程师来说陌生的领域，尤其是专利权、著作权、商标权。在国外，每年因为这些问题导致的侵权官司不在少数。而我们在开源之初，对这块的选择、保护也是极其谨慎，包括开源许可协议的选择、授权方面，代码署名权等，这些都是很好的智力保护，也是我们产品的核心竞争力之一。尊重知识，尊重产权，才能构建一个和谐积极向上的开源氛围，打造真正的自主知识产权品牌产品。

>在Alibaba，我们基于开源引擎的RocketMQ，为云上用户提供了商业化版本的Aliware MQ。两个产品都是由阿里中间件消息团队出品。商业版Aliware MQ 在支持 TCP 、HTTP 和MQTT 协议接入，功能方面增强了运维管控方面，生态集成的能力（包括可视化的消息轨迹、资源报表统计以及监控报警、Kafka集成等）。它在公有云上本身具备多机房部署同城高可用容灾特性，目的是满足企业级要求。

>关于社区的运营，我们采取了和Apache顶级项目基本相似的策略。首先，必须立足于高质量产品本身，从版本规划开始，我们建立了里程碑讨论，Features设计，编码自测，结对Review，集成测试，Release讨论，Release公告等等一系列规范且高效的软件研发流程。其次，在社区运营层面，则有一系列与社区互动的活动，如线下meetup、workshop、ApacheCon、不定期的编程马拉松等，吸纳新的Contributor和Committer进来。
 

## 使用企业
除了阿里巴巴集团，Apache RocketMQ还被滴滴出行，SF Express，WeBank，北京大学和中国科学院等数百家公司和研究/教育机构使用。

## RocketMQ的技术概览
在我们看来，它最大的创新点在于能够通过精巧的横向、纵向扩展，不断满足与日俱增的海量消息在高吞吐、高可靠、低延迟方面的要求。

目前RocketMQ主要由NameServer、Broker、Producer以及Consumer四部分构成，如下图所示。
![](http://img3.tbcdn.cn/5476e8b07b923/TB1FUR8PVXXXXbbXpXXXXXXXXXX)

NameServer以轻量级的方式提供服务发现和路由功能，每个NameServer存有全量的路由信息，提供对等的读写服务，支持快速扩缩容。

Broker负责消息存储，以Topic为纬度支持轻量级的队列，单机可以支撑上万队列规模，支持消息推拉模型，具备多副本容错机制（2副本或3副本）、强大的削峰填谷以及上亿级消息堆积能力，同时可严格保证消息的有序性。除此之外，Broker还提供了同城异地容灾能力，丰富的Metrics统计以及告警机制。这些都是传统消息系统无法比拟的。

Producer由用户进行分布式部署，消息由Producer通过多种负载均衡模式发送到Broker集群，发送低延时，支持快速失败。

Consumer也由用户部署，支持PUSH和PULL两种消费模式，支持集群消费和广播消息，提供实时的消息订阅机制，满足大多数消费场景。

## 特点
RocketMQ具有很多优秀的性能，尤其适应那些需要严格事务运用的场合。下面通过几个方面进行介绍。

> ~~注：因为RocketMQ和Kafka有着一定的渊源，而且Kafka也是目前运用较为广泛的，所以我们在讲述时K有时需要用Kafka作为对比，来更好的帮助读者了解RocketMQ。~~

### 数据可靠性
RocketMQ支持异步实时刷盘，同步刷盘，同步复制，异步复制。具有高可靠性。不会因为操作系统的崩溃而导致数据丢失。

### 性能
~~RocketMQ单机写入TPS单实例约7万条/秒，单机部署3个Broker，可以跑到最高12万条/秒，消息大小10个字节
低于Kafka的百万条/秒。但是RocketMQ在队列数上有很大提升。Kafka在64个队列以上就会明显增加响应时间，RocketMQ单机最高支持5万个队列，且负载不会发生明显变化。~~

RocketMQ经过一系列的实践和优化，处理速度从最初的10,000TPS到目前已经超过50,000TPS。单纯比较TPS的话虽然还不如Kafka的百万级别，但在支持事务的消息中间件来说已经是非常优秀了。

### 消息投递实时性
RocketMQ采用长轮询，消息投递延迟通常在几个毫秒左右。
Kafka0.8版本后也支持长轮询了。


### 支持的队列数
RocketMQ单机最高支持5万个队列，且负载不会发生明显递增。

### 消费失败重试
RocketMQ支持消费失败重试，这个特性非常适合运用在充值方面的应用。
Kafka则不支持。

### 严格的消息顺序
RocketMQ支持严格的意义上的消息顺序。即时在一台Broker宕机后，消息发送会失败，但是不会乱序。

### 定时消息
RocketMQ支持定时消息

### 分布式事务消息
RocketMQ支持定时消息

### 消息查询
RocketMQ支持根据消息标识或内容查询。

### 消息回溯
RocketMQ支持按照时间来回溯消息，精度毫秒，例如从一天之前的某时某分某秒开始重新消费消息。


## RocketMQ与ActiveMQ与Kafka

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