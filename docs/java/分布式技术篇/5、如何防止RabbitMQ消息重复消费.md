# 5、如何防止 RabbitMQ 消息重复消费

保证消息幂等性。幂等性概念：一个请求，不管重复来多少次，结果是不会改变的。

RabbitMQ、RocketMQ、Kafka 等任何队列不保证消息不重复，如果业务需要消息不重复消费，则需要消费端处理业务消息要保持幂等性

方式一：Redis 的setNX() , 做消息id 去重java 版本目前不支持设置过期时间

//Redis 中操作，判断是否已经操作过TODO boolean flag = jedis.setNX(key);

if(flag){

//消费

}else{

//忽略，重复消费

}

方式二：redis 的Incr 原子操作：key 自增，大于0 返回值大于0 则说明消费过，

(key 可以是消息的md5 取值, 或者如果消息id 设计合理直接用id 做key) int num = jedis.incr(key);

if(num == 1){

//消费

}else{

//忽略，重复消费

}

方式三：数据库去重表

设计一个去重表，某个字段使用Message 的key 做唯一索引，因为存在唯一索引，所以重复消费会失败

CREATE TABLE `message_record` ( `id` int(11) unsigned NOT NULL AUTO_INCREMENT, `key` varchar(128) DEFAULT NULL, `create_time` datetime DEFAULT NULL, PRIMARY KEY (`id`), UNIQUE KEY `key` (`key`) ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

> 更新: 2024-05-01 16:32:35  
