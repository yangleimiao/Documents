Kafka学习

---

##### Kafka目前有哪些内部topic，各自作用

__consumer_offsets：用来保存Kafka消费者的位移信息

__transaction_state：用来存储事务日志消息

##### 优先副本是什么？作用？

优先副本是指在AR集合列表中的第一个副本；

理想情况下优先副本是该分区的leader副本，也可以称之为preferred leader，Kafka要确保所有主题的优先副本在Kafka集群中均匀分布，这样就保证了所有分区的leader均衡分布，以此来促进集群的负载均衡；

##### Kafka有哪些分区分配的概念？

1. 生产者的分区分配是指为每条消息指定其所要发往的分区，可以编写一个具体的类实现`org.apache.kafka.clients.producer.Partitioner` 接口；
2. 消费者中的分区分配是指为消费者指定其可以消费消息的分区，Kafka提供了消费者客户端参数`partition.assignment.strategy` 来设置消费者与订阅主题之间的分区分配策略；
3. 分区副本中的分配是指为集群制定创建主题时的分区副本分配方案，即在哪个broker中创建哪些分区的副本，kafka-topics.sh脚本中提供了`replica-assignment`参数来手动指定分区副本的分配方案；

##### Kafka的日志目录结构



![kafka](./images/kafka.png)

Kafka中的消息是以主题为基本单位进行归类的，各个主题在逻辑上相互独立，每个主题可以分为一个或多个分区；不考虑多副本的情况，一个分区对应一个日志（Log），为了防止log过大，Kafka又引入了日志分段（LogSegment）的概念，将Log切分为多个LogSegment，相当于一个大文件被分为多个较小文件；

Log和LogSegment也不是纯粹物理意义的概念，Log在物理上以文件夹形式存储，而每个LogSegment对应于磁盘上一个日志文件和两个索引文件（.index，偏移量索引文件、.timeindex，时间戳索引文件）以及其他文件（比如以.txnindex为后缀的事务索引文件）；

##### Kafka中有哪些索引文件?

每个日志分段文件（LogSegment）对应于两个索引文件，主要用来提高查找消息的效率；

偏移量索引文件用来建立消息偏移量（offset）到物理地址之间的映射关系，方便快速定位消息所在物理位置；

时间戳索引文件则根据指定的时间戳（timestamp）来查找对应的偏移量信息；

##### Kafka怎么查找到指定offset对应的消息？

Kafka是通过seek()方法来指定消费的，在执行seek()方法之前要去执行一次poll()方法，等到分配到分区之后会去对应的分区的指定位置开始消费，如果指定的位置发生了越界，那么会根据`auto.offset.reset ` 参数设置的情况进行消费；



















































