# aug.github.io
MQ设计：
## <font size="3">MQ 消息顺序消费</font><br />
 **Activemq处理方案：**
 
* 独有消费者，只有一个消费者消费消息
* `messageGroups`负载均衡机制（个人理解：消息设置`messageGroups`,但还在一个队列中, 发送给对应的包含`message group`的消费者）

**Rocketmq解决方案：**

* 保证消息发送到同一台`broker server`下的同一个队列

**总结：** 无论`Activemq`还是`Rocketmq`都要想办法让有顺序的消息被同一消费者消费

## <font size="3">MQ 保证消息不丢失</font>
**生产者处理方案：**

* 阻塞式发送，确认返回状态。失败重试
* 事物式发送

**Broker处理方案：**

* 消息持久化
* 同步刷盘、异步刷盘，保证消息一定存储成功
* `master-slave`模式，支持同步和异步复制，解决单点问题

**消费者处理方式：**

* `ack`机制
* 消费者维护自己的`offset`，消费成功后在更新自己的`offset`
