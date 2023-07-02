# ==-----------------------------------------------------------------------------Kafka==

https://www.51cto.com/article/637229.html  讲解kafka宕机 是因为_consumer_offset 只保存一个副本

https://blog.csdn.net/weixin_44052055/article/details/103726373  log日志满和jre内存满了 当值宕机

https://juejin.cn/post/6844904094021189639

https://new.qq.com/omn/20210609/20210609A07ETR00.html   消费者只消费一次消息 非常漂亮 实现幂等

# kafka基础概念和知识

## kafka 基本结构？问什么选择Kakfa



>
>
>![图片](https://mmbiz.qpic.cn/mmbiz_png/iaIdQfEric9Tw5HhjBWfamF35XaNsxW3GH7CcZ39jmlbghrJ6qF7fUFFIoAia2xGQaNia0a4JtMmIrpWoib79wkPVXg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
>
>kafka发布订阅模型呗 
>
>![3.1、初识Kafka 的逻辑结构和物理结构_༺ bestcxx的专栏༻-CSDN博客](https://img-blog.csdnimg.cn/20191212232001964.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Jlc3RjeHg=,size_16,color_FFFFFF,t_70)



## kafka对比其他mq优势

>使用 mq 做一些异步的操作 ， 比如说我们这个接口是属于http协议接口 是同步调用过程中相应比较慢的情况下 会导致我们的客户端比较超时 ， 比如说某些业务接口确实比较耗时，相应比较满的情况下， 那么我们客户端他会同步进行阻塞等待，容易引发我们客户端超时，客户端一旦发生超时会出发重试的策略过程中会导致我们的业务可能重复执行， 所以我们需要去注意一些幂等性，执行耗时的接口使用mq异步的去实现，能够提高我们http接口相应的速度。比如说异步发优惠券、异步发库存。
>
>----
>
>应用解耦、异步处理、流量消费、日志处理。 相比于其他mq发送速度更快 
>
>RocketMQ 选择了 mmap + write 这种零拷贝方式，适用于业务级消息这种小块文件的数据持久化和传输；**而 Kafka 采用的是 sendfile 这种零拷贝方式，适用于系统日志消息这种高吞吐量的大块文件的数据持久化和传输。但是值得注意的一点是，Kafka 的索引文件使用的是 mmap + write 方式，数据文件使用的是 sendfile 方式。**
>
>![preview](https://pic3.zhimg.com/v2-da99a5a5b027c7f374186b55919b0f0e_r.jpg)





## Kafka为什么分区？分区策略？

>https://blog.csdn.net/qq_38262266/article/details/107356824  
>
>**为什么要分区patition？**
>
>（1）方便在集群中扩展，每个 Partition 可以通过调整以适应它所在的机器，而一个 topic又可以有多个 Partition 组成，因此整个集群就可以适应任意大小的数据了；
>
>（2）可以提高并发，因为可以以 Partition 为单位读写了。
>
>
>-----
>
>**分区策略？**
>
>Producer发送数据封装成对象时的参数，根据参数设定，我们就能将数据放在对应的partition中。
>
>1. 指明 partition 的情况下，直接将数据放在对应的 partiton ；
>2. 没有指明 partition 值但有 key 的情况下，将 key 的 hash 值与 topic 的 partition 数进行取余得到 partition 值；
>3. 既没有 partition 值又没有 key 值的情况下，第一次调用时随机生成一个整数（后面每次调用在这个整数上自增），将这个值与 topic 可用的 partition 总数取余得到 partition 值，也就是常说的 round-robin 算法。



## [kafka如何保证消息得顺序性](https://www.cnblogs.com/yfb918/p/12192857.html)？

>**保证消费消息的顺序性？**
>
>1. 比如说我们建了一个 topic，有三个 partition。
>
>2. 生产者在写的时候，其实可以指定一个 key，比如说我们指定了某个订单 id 作为 key，那么这个订单相关的数据，一定会被分发到同一个 partition 中去，而且这个 partition 中的数据一定是有顺序的。
>
>3. 消费者从 partition 中取出来数据的时候，也一定是有顺序的。到这里，顺序还是 ok 的，没有错乱。
>
>
>
> 接着，我们在消费者里可能会搞多个线程来并发处理消息。因为如果消费者是单线程消费处理，而处理比较耗时的话，比如处理一条消息耗时几十 ms，那么 1 秒钟只能处理几十条消息，这吞吐量太低了。而多个线程并发跑的话，顺序可能就乱掉了。
>
>​       II. 解决方案
>
>一个 topic，一个 partition，一个 consumer，内部单线程消费，单线程吞吐量太低，一般不会用这个。
>写 N 个内存 queue，具有相同 key 的数据都到同一个内存 queue；然后对于 N 个线程，每个线程分别消费一个内存 queue 即可，这样就能保证顺序性。
>
><img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2ktYmV0YS8xNjA4MTA0LzIwMjAwMS8xNjA4MTA0LTIwMjAwMTE0MTY0OTA0NTkyLTk0NjMzNzA4My5wbmc?x-oss-process=image/format,png" alt="img" style="zoom:80%;" />





## kafka是如何消费的？

>Kafka 是支持订阅/发布模式的，生产者发送数据给 Kafka Broker，那么消费者是如何知道生产者发送了数据呢？其实生产者产生的数据消费者是不知道的，KafkaConsumer 采用轮询的方式定期去 Kafka Broker 中进行数据的检索，如果有数据就用来消费，如果没有就再继续轮询等待，下面是轮询等待的具体实现
>
>```java
>try {
>while (true) {
>ConsumerRecords<String, String> records = consumer.poll(Duration.ofSeconds(100));
>for (ConsumerRecord<String, String> record : records) {
>int updateCount = 1;
>if (map.containsKey(record.value())) {
>updateCount = (int) map.get(record.value() + 1);
>}
>map.put(record.value(), updateCount);
>}
>}
>}finally {
>consumer.close();
>}
>```
>
>- 这是一个无限循环。消费者实际上是一个长期运行的应用程序，它通过轮询的方式向 Kafka 请求数据。
>- 第三行代码非常重要，Kafka 必须定期循环请求数据，否则就会认为该 Consumer 已经挂了，会触发重平衡，它的分区会移交给群组中的其它消费者。传给 `poll()` 方法的是一个超市时间，用 `java.time.Duration` 类来表示，如果该参数被设置为 0 ，poll() 方法会立刻返回，否则就会在指定的毫秒数内一直等待 broker 返回数据。
>- poll() 方法会返回一个记录列表。每条记录都包含了记录所属主题的信息，记录所在分区的信息、记录在分区中的偏移量，以及记录的键值对。我们一般会遍历这个列表，逐条处理每条记录。
>- 在退出应用程序之前使用 `close()` 方法关闭消费者。网络连接和 socket 也会随之关闭，并立即触发一次重平衡，而不是等待群组协调器发现它不再发送心跳并认定它已经死亡。











## kafka如何保证消息不丢失

>**broker**:    kafka生产者提交消息到broker, 对于集群模式下会有多个`broker`, 我们如果设置`ack=1`就是代表一个broker收到消息就会保存该消息代表成功。也可以另所有Broker保存消息才算提交成功，但是无论哪种提交 最后都会进行持久化操作。
>
>**生产者**： 1.  send()方法是异步发送，在调用send()方法的时候可以采用添加回调函数的用法。如果发送失败，检查发送失败的原因。
>
>```java
>ListenableFuture<SendResult<String, Object>> future = kafkaTemplate.send(topic, o);
>future.addCallback(result -> logger.info("生产者成功发送消息到topic:{} partition:{}的消息", result.getRecordMetadata().topic(), result.getRecordMetadata().partition()),
>      ex -> logger.error("生产者发送消失败，原因：{}", ex.getMessage()));
>
>```
>
>​            	 2.   推荐为 Producer 的`retries`（重试次数）设置一个比较合理的值，一般是 3 ，但是为了保证消息不丢失的话一般会设置比较大一点。设置完成之后，当出现网络问题之后能够自动重试消息发送，避免消息丢失。另外，建议还要设置重试间隔，因为间隔太小的话重试的效果就不明显了，网络波动一次你3次一下子就重试完了
>
>-----
>
>
>
>**消费者**：
>
>         1. 如果kafka自动帮消费者提交某个分区的`offset` ，如果消费者突然挂掉，实际上并没有被消费，但是却自动提交了offset.
>         1. 如果关闭kakfa自动提交`offset`改成消费者来控制`offset`，消费者消费完消息在提交`offset`，但是这里会导致重复消费信息。
>
>------



## 如何保证消费者消费信息不丢失

>
>
>手动提交Offset   如果说在提前之前宕机， 会产生重复消费， 如果产生重复消费 。为每个消息加一个标志ID
>
>手动存储offset 到redis        重启kafka 指定redis 当中存储的offset开始进行消费

## kafka 1.0版本 offset存储在哪

>Kafka offset是在broker当中  

## kafka如何保证消息消费的幂等性

>幂等，就是指多接口的多次调用所产生的结果和只调用一次是一致的。没有幂等性的情况下就会重复发送数据。
>
>Kafka的幂等性机制能保证单个分区不会重复写入数据，多分区的话需要实现事务，而实现幂等性的核心就是引入了producer id 和 sequence number序列号字段 这两个概念。对于新接受到的消息，broker端会进行如下判断：
>
>1. 如果新消息的sequence number正好是broker端维护的<PID,Partition> -> sequence number大1，说broker会接受处理这条消息。
>2. 如果新消息的sequence number比broker端维护的sequence number要小，说明时重复消息，broker可以将其直接丢弃
>3. 如果新消息的sequence number比broker端维护的sequence number要大过1，说明中间存在了丢数据的情况，那么会响应该情况，对应Producer会抛出OutOfOrderSequenceException。
>
>Properties.put(“enable.idempotence”,true);   开启幂等性。  就是主要防止生产者 生产重复消息。
>
>
>
>**kafka事务特性**
>
>Kafka事务性主要是为了解决幂等性无法跨Partition运作的问题，事务性提供了多个Partition写入的原子性，即写入多个Partition要么全部成功，要么全部失败，不会出现部分成功部分失败这种情况
>
>---------
>
>https://new.qq.com/omn/20210609/20210609A07ETR00.html   
>
>**实现消费者只消费一次  非常之重点：**
>
>**生产者**可以增加幂等性：来保证不发送重复消息。   Properties.put(“enable.idempotence”,true);   开启幂等性。  就是主要防止生产者 生产重复消息。
>
>在消费者当中： 1. 在消费者消费的时候引入事务的方案，例如入库操作，保证消息处理和写入数据库必须同时成功或者同时失败。
>
>​							2. 业务层进行处理： 其中有一种是增加乐观锁的方式。比如，你的消息处理程序需要给一个人的账号加钱，那么你可以通过乐观锁的方式来解决。具体的操作方式是这样的：你给每个人的账号数据中增加一个版本号的字段，在生产消息时先查询这个账户的版本号，并且将版本号连同消息一起发送给消息队列。消费端在拿到消息和版本号后，在执行更新账户金额 SQL 的时候带上版本号，类似于执行：你看，我们在更新数据时给数据加了乐观锁，这样在消费第一条消息时，version 值为 1，SQL 可以执行成功，并且同时把 version 值改为了 2；在执行第二条相同的消息时，由于 version 值不再是 1，所以这条 SQL 不能执行成功，也就保证了消息的幂等性。



## kafka 消息堆积  如何解决

>https://blog.csdn.net/qq_16681169/article/details/101081656
>
>max.poll.records       一次poll返回的最大记录数默认是500
>max.poll.interval.ms   两次poll方法最大时间间隔这个参数，默认是300s
>
>这次问题出现的原因为由于业务上下方的消息增量变多，导致堆积的消息过多，每一批poll()的处理都能达到500条消息，导致poll之后消费的时间过长。 服务端约定了和客户端max.poll.interval.ms，两次poll最大间隔。如果客户端处理一批消息花费的时间超过了这个限制时间，broker可能就会把消费者客户端移除掉，提交偏移量又会报错。所以拉取偏移量没有提交到broker，分区又rebalance，下一次重新分配分区时，消费者会从最新的已提交偏移量处开始消费，这里就出现了重复消费的问题
>
>
>
>
>1. 防止消费者挂掉的 需要设置消费者消费能力 设置kakfa配置参数 ，消费者每次poll的数据业务处理时间不能超过kafka的max.poll.interval.ms，可以考虑调大超时时间或者调小每次poll的数据量。增加max.poll.interval.ms处理时长(默认间隔300s)
>2. 可以考虑增强消费者的消费能力，做消费者集群， 使用线程池消费或者将消费者中耗时业务改成异步，并保证对消息是幂等处理
>3. 不但要有消息积压的监控，还可以考虑做消息消费速度的监控（前后两次offset比较）





## kafka 消息队列方式有什么优缺点

>**优点：解耦、异步、削峰**
>
>缺点：
>
>**系统可用性降低**：系统引入的外部依赖越多，越容易挂掉，本来你就是A系统调用BCD三个系统的接口就好了，人ABCD四个系统好好的，没啥问题，你偏加个MQ进来，万一MQ挂了咋整？MQ挂了，整套系统崩溃了，你不就完了么。
>
>**系统复杂性提高**：硬生生加个MQ进来，你怎么保证消息没有重复消费？怎么处理消息丢失的情况？怎么保证消息传递的顺序性？头大头大，问题一大堆，痛苦不已
>
>**一致性问题**：A系统处理完了直接返回成功了，人都以为你这个请求就成功了；但是问题是，要是BCD三个系统那里，BD两个系统写库成功了，结果C系统写库失败了，咋整？你这数据就不一致了。







## kafka produce生产一条消息流程

>1. 包装key value信息 经过封装发送给broker 
>2. 如果存在 `key` 会通过映射到 `broker` 映射到某一个`topic`特定的分区呗  
>3. 如果 `keu==null`  会顺序存放在分区当中呗   
>4. 还有就是生产者  在这里就是指定分区呗  分发到特定的分区当中呗 对吧哈呢  



## kafka consumer只能消费一个分区么

>先说结论： 如果消费者数量小于分区数量  那么就是利用负载均衡算法来分配消费者消费那个分区呗
>
>但是消费者是如何跟分区绑定的呢？ 在这里就是如何进行通信的呢 
>
>----------
>
>1. 在分配消费者数量的时候  尽量须要分分区数量一致。 这样就是一一对应关系
>
>2. 如果消费者数量多， 那么会存在多出来的消费者不会进行消费呗  因为这里边可能存在多个消费者消费同一个分区可能存在锁的性能损耗，例如就是一个客服来接听消费者电话， 无需多个客户来同时接听消费者电话。 
>3. 如果消费者数量少于分区数 ， 那么就是会通过负载轮训算法来进行分配呗。



## kafka 宕机原因分析

>客观原因： kafka日志满了。 导致节点宕机
>
>或者就是在创建集群的时候 可能配置文件没有配置好  例如_consumer_offset 全局只保存一份在`broker` 主节点里边  如果主节点宕机了， 那么就是即便从节点上任 集群还是处于宕机状态。





# ==----------------------------------------------------------------------------Flink==

>注意事项：  
>
>**代码编写注意事项：**
>
>1. 在 flink、kafka数据源模式下，需要对数据源、算子、聚合、下沉 这几个操作分别设置并行度，并且在web ui 界面上查看flink的实时动态来优化能，使其高吞吐、低延迟。
>2.  算子操作并行度设置理念： 如果是要连接kafka数据源 在这里对应算子操作的并行度设置上需要跟kafka分区数目保持一直呗 
>
>
>
>**提交flink程序jar包 注意事项：**
>
>1. 确定好flink版本号
>2. 确定好kafka版本号
>3. 上传jar包到web ui界面的时候， 需要在flink lib 目录下上传程序所需要的jar包  例如程序用到kafka 就要把kafka jar包上传到flink lib目录下， 或者例如需要log4j 需要把log4j jar上传到flink lib当中。 如果没有上传 在web ui界面启动flink 会发生报错  

# Flink基础架构

## Flink简介

>Flink是一个以 **流** 为核心的高可用、高性能的分布式计算引擎。具备 **流批一体，**高吞吐、低延迟，容错能力，大规模复杂计算等特点，在数据流上提供 **数据分发**、通信等功能。

## 数据流、流批一体、容错能力等概念

>**数据流：**
>
>所有产生的 **数据** 都天然带有 **时间概念**，把 事件 按照时间顺序排列起来，就形成了一个事件流，也被称作数据流。
>
>
>
>**流批一体：**
>
>**有界数据**，就是在一个确定的时间范围内的数据流，有开始，有结束，一旦确定就不会再改变，一般 **批****处理** 用来处理有界数据，如上图的 bounded stream。
>
>**无界数据**，就是持续产生的数据流，数据是无限的，有开始，无结束，一般 **流处理** 用来处理无界数据。如图 unbounded stream。
>
>Flink的设计思想是以 **流** 为核心，批是流的特例，擅长处理 无界 和 有界 数据， Flink 提供 精确的时间控制能力 和 有状态 计算机制，可以轻松应对无界数据流，同时 提供 **窗口** 处理有界数据流。所以被成为流批一体。
>
>
>
>**容错能力：**
>
>在分布式系统中，硬件故障、进程异常、应用异常、网络故障等异常无处不在，Flink引擎必须保证故障发生后 不仅可以 **重启** 应用程序，还要 **确保** 其内部状态保持一致，从最后一次正确的时间点重新出发





## Flink运行时架构

>![The processes involved in executing a Flink dataflow](https://nightlies.apache.org/flink/flink-docs-master/fig/processes.svg)

>Flink 集群采取 Master - Slave 架构，Master的角色为 **JobManager**，负责集群和作业管理，Slave的角色是 **TaskManager**，负责执行计算任务，同时，Flink 提供客户端 Client 来管理集群和提交任务，**JobManager** 和 **TaskManager** 是集群的进程。
>
>**client:**
>
>`client`： Flink 客户端是F1ink 提供的 CLI 命令行工具，用来提交 Flink 作业到 Flink 集群，在客户端中负责 StreamGraph (流图)和 Job Graph (作业图)的构建。
>
>**JobManager**
>
>`JobManager `:根据并行度将 Flink 客户端提交的Flink 应用分解为子任务，从资源管理器 ResourceManager 申请所需的计算资源，资源具备之后，开始分发任务到 TaskManager 执行 Task，并负责应用容错，跟踪作业的执行状态，发现异常则恢复作业等。
>
>**TaskManager**
>
>TaskManager 接收 JobManage 分发的子任务，根据自身的资源情况 管理子任务的启动、 停止、销毁、异常恢复等生命周期阶段。Flink程序中必须有一个TaskManager。



## flink并行度

>Flink程序在执行的时候，会被映射成一个**Streaming Dataflow。**一个Streaming Dataflow是由一组Stream和Transformation Operator组成的。在启动时从一个或多个Source Operator开始，结束于一个或多个Sink Operator。 **Flink程序本质上是并行的和分布式的**，在执行过程中，**一个流(stream)包含一个或多个流分区**，而每一个operator包含一个或多个operator子任务。操作子任务间彼此独立，在不同的线程中执行，甚至是在不同的机器或不同的容器上。**operator子任务的数量是这一特定operator的并行度**。相同程序中的不同operator有不同级别的并行度。
>
>-----------
>
>在实际生产中可以从四个不同的维度分别设置并行度
>
>- 操作算子层面(Operator Level)
>- 执行环境层面(Execution Environment Level)
>- 客户端层面(Client Level)
>- 系统层面(System Level)
>
>需要注意的优先级：算子层面>环境层面>客户端层面>系统层面。

## Flink作业中的DataStream，Transformation

>Flink作业中，包含两个基本的块：**数据流（DataStream）**和 **转换（Transformation）**。
>
>DataStream是逻辑概念，为开发者提供API接口，**Transformation**是处理行为的抽象，包含了数据的读取、计算、写出。所以Flink 作业中的DataStream API 调用，实际上构建了多个由 Transformation组成的数据处理流水线（Pipeline）



## Flink常用算子

>1. **数据读取**，这是Flink流计算应用的起点，常用算子有：
>
>从内存读：fromElements、从文件读：readTextFile、Socket 接入 ：socketTextStream、自定义读取：createInput
>
>2. 处理数据的算子，主要用于 **转换** 过程
>
>常用的算子包括：Map（单输入单输出）、FlatMap（单输入、多输出）、Filter（过滤）、KeyBy（分组）、Reduce（聚合）、Window（窗口）、Connect（连接）、Split（分割）等。







# Flink窗口

**窗口概念：**将无界流的数据，按时间区间，划分成多份数据，分别进行统计**(聚合)**

## Flink 窗口划分模式

>![img](https://oss-emcsprod-public.modb.pro/wechatSpider/modb_20210911_9a434b7a-1257-11ec-948d-00163e068ecd.png)
>
>Flink支持两种划分窗口的方式(time和count)，第一种，**按时间驱动进行划分**、另一种按**数据驱动进行划分**。
>
>1、按时间驱动Time Window 划分可以分为 滚动窗口 Tumbling Window 和滑动窗口 Sliding Window。
>
>2、按数据驱动Count Window也可以划分为滚动窗口 Tumbling Window 和滑动窗口 Sliding Window。
>
>3、Flink支持窗口的两个重要属性(**窗口长度size和滑动间隔interval**)，通过窗口长度和滑动间隔来区分滚动窗口和滑动窗口。





# Flink部署

## Standalone模式

>`TaskMannager` 与 `slot` 联系
>
>1. Flink 中每一个 TaskManager 都是一个JVM进程，它可能会在独立的线程上执行一个或多个 subtask
>2. 为了控制一个 TaskManager 能接收多少个 task， TaskManager 通过 task slot 来进行控制（一个 TaskManager 至少有一个 slot）
>3. 每个task slot表示TaskManager拥有资源的一个固定大小的子集。假如一个TaskManager有三个slot，那么它会将其管理的内存分成三份给各个slot(注：这里不会涉及CPU的隔离，slot仅仅用来隔离task的受管理内存)
>4. 可以通过调整task slot的数量去自定义subtask之间的隔离方式。如一个TaskManager一个slot时，那么每个task group运行在独立的JVM中。而**当一个TaskManager多个slot时，多个subtask可以共同享有一个JVM,而在同一个JVM进程中的task将共享TCP连接和心跳消息，也可能共享数据集和数据结构，从而减少每个task的负载**。
>
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20200428203404161.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM5NjU3OTA5,size_16,color_FFFFFF,t_70#pic_center)

>启动Flink后,在flink里边直接就是可以执行默认集群就是`standalone`模式  可以在[Web UI](lcoalhost:8081)的`Submit New Job`提交jar包，然后指定Job参数。
>
>- Entry Class
>
>  程序的入口，指定入口类（类的全限制名）
>
>- Program Arguments
>
>  程序启动参数，例如`--host localhost --port 7777`
>
>- Parallelism
>
>  设置Job并行度。
>
>  Ps：并行度优先级（从上到下优先级递减）



## yarn模式

```markup
 以Yarn模式部署Flink任务时，要求Flink是有 Hadoop 支持的版本，Hadoop 环境需要保证版本在 2.2 以上，并且集群中安装有 HDFS 服务。
```



 Flink提供了两种在yarn上运行的模式，分别为Session-Cluster和Per-Job-Cluster模式。

**Session-Cluster模式**

 Session-Cluster 模式需要先启动集群，然后再提交作业，接着会向 yarn 申请一块空间后，**资源永远保持不变**。如果资源满了，下一个作业就无法提交，只能等到 yarn 中的其中一个作业执行完成后，释放了资源，下个作业才会正常提交。**所有作业共享 Dispatcher 和 ResourceManager**；**共享资源；适合规模小执行时间短的作业。**

![img](https://img-blog.csdnimg.cn/20201228202616146.png)

 **在 yarn 中初始化一个 flink 集群，开辟指定的资源，以后提交任务都向这里提交。这个 flink 集群会常驻在 yarn 集群中，除非手工停止。**

**Per Job Cluster 模式**

 一个 Job 会对应一个集群，每提交一个作业会根据自身的情况，都会单独向 yarn 申请资源，直到作业执行完成，一个作业的失败与否并不会影响下一个作业的正常提交和运行。**独享 Dispatcher 和 ResourceManager**，按需接受资源申请；适合规模大长时间运行的作业。

 **每次提交都会创建一个新的 flink 集群，任务之间互相独立，互不影响，方便管理。任务执行完成之后创建的集群也会消失。**

![img](https://img-blog.csdnimg.cn/20201228202718916.png)

## Kubernetes部署

> 容器化部署时目前业界很流行的一项技术，基于Docker镜像运行能够让用户更加方便地对应用进行管理和运维。容器管理工具中最为流行的就是Kubernetes（k8s），而Flink也在最近的版本中支持了k8s部署模式。







# 参考githun && 博客 链接

https://nightlies.apache.org/flink/flink-docs-master/zh/docs/concepts/flink-architecture/  官方网站



https://blog.csdn.net/boling_cavalry/article/details/105598224    flink sink kafka 操作



https://iter01.com/567533.html     flink与spring生态体系 



http://smartsi.club/parse-and-pass-arguments-in-flink.html  flink参数传递



https://blog.csdn.net/wangpei1949/article/details/101625394  flink算子操作



https://github.com/nexmark/nexmark   github flink压力测试



https://github.com/CheckChe0803/flink-recommandSystem-demo  flink+redis推荐系统



https://ashiamd.github.io/docsify-notes/#/study/BigData/Flink/%E5%B0%9A%E7%A1%85%E8%B0%B7Flink%E5%85%A5%E9%97%A8%E5%88%B0%E5%AE%9E%E6%88%98-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0?id=_124-%e7%aa%97%e5%8f%a3    尚硅谷
