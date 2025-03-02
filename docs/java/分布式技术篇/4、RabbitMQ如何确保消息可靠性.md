# 4、RabbitMQ 如何确保消息可靠性

消息可靠性一般来说由3 方面来保证：

1) 生产者

RabbitMQ 提供transaction 事务和confirm 模式来确保生产者不丢消息；

Transaction 事务机制就是说：发送消息前，开启事务（channel.txSelect()）,然后发送消息，如果发送过程中出现什么异常，事务就会回滚

（channel.txRollback()）,如果发送成功则提交事务

（channel.txCommit()），然而，这种方式有个缺点：吞吐量下降。



confirm 模式用的居多：一旦channel 进入confirm 模式，所有在该信道上发布的消息都将会被指派一个唯一的ID（从1 开始），一旦消息被投递到所有匹配的队列之后；

rabbitMQ 就会发送一个ACK 给生产者（包含消息的唯一ID），这就使得生产者知道消息已经正确到达目的队列了；



如果rabbitMQ 没能处理该消息，则会发送一个Nack 消息给你，可以进行重试操作。

2) 消息队列本身



可以进行消息持久化, 即使rabbitMQ 挂了，重启后也能恢复数据如果要进行消息持久化，那么需要对以下3 种实体均配置持久化

a) Exchange

声明exchange 时设置持久化（durable = true）并且不自动删除(autoDelete

= false)

b) Queue

声明queue 时设置持久化（durable = true）并且不自动删除(autoDelete = false)

c) message

发送消息时通过设置deliveryMode=2 持久化消息



3) 消费者



消费者丢数据一般是因为采用了自动确认消息模式，消费者在收到消息之后，处理消息之前，会自动回复RabbitMQ 已收到消息；如果这时处理消息失败，就会丢失该消息；改为手动确认消息即可！手动确认模式下消费失败时，不将其重新放入队列

（确认重试也不会成功的情形），打印错误信息后，通知相关人员，人工介入处理。





> 更新: 2024-05-01 16:32:19  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/nghqixdlc711dlrh>