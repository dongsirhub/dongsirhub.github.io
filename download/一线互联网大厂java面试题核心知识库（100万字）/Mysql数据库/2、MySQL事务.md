# 2、MySQL 事务

**<font style="color:rgb(32,36,41);">事务的基本要素（ACID）</font>**

● 原子性（Atomicity）：事务开始后所有操作，要么全部做完，要么全部不做， 不可能停滞在中间环节。事务执行过程中出错，会回滚到事务开始前的状态，所有的操作就像没有发生一样。也就是说事务是一个不可分割的整体，就像化学中学过的原子，是物质构成的基本单位

● 一致性（Consistency）：事务开始前和结束后，数据库的完整性约束没有被破坏。比如A 向B 转账，不可能A 扣了钱，B 却没收到。

● 隔离性（Isolation）：同一时间，只允许一个事务请求同一数据，不同的事务之间彼此没有任何干扰。比如A 正在从一张银行卡中取钱，在A 取钱的过程结束前， B 不能向这张卡转账。

● 持久性（Durability）：事务完成后，事务对数据库的所有更新将被保存到数据库，不能回滚。

**MySQL**** ****事务隔离级别：**

****

| 事务隔离级别 | 脏读 | 不可重复读 | 幻读 |
| :--- | :--- | :--- | :--- |


  


****

|  |  |  |  |
| :--- | :--- | :--- | :--- |
| 读未提交（read-uncommitted） | 是 | 是 | 是 |
| 读提交（read-committed） | 否 | 是 | 是 |
| 可重复读（repeatable-read） | 否 | 否 | 是 |
| 串行化（serializable） | 否 | 否 | 否 |


****

**<font style="color:rgb(32,36,41);">事务的并发问题</font>**

● 脏读：事务A 读取了事务B 更新的数据，然后B 回滚操作，那么A 读取到的数据是脏数据

● 不可重复读：事务A 多次读取同一数据，事务B 在事务A 多次读取的过程中，对数据作了更新并提交，导致事务A 多次读取同一数据时，结果不一致

● 幻读：系统管理员A 将数据库中所有学生的成绩从具体分数改为ABCDE 等级，但是系统管理员B 就在这个时候插入了一条具体分数的记录，当系统管理员A 改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样，这就叫幻读。

如何解决脏读、幻读、不可重复读



● 脏读：隔离级别为读提交、可重复读、串行化可以解决脏读



● 不可重复读：隔离级别为可重复读、串行化可以解决不可重复读



● 幻读：隔离级别为串行化可以解决幻读、通过MVCC + 区间锁可以解决幻读**小结：**

不可重复读的和幻读很容易混淆，不可重复读侧重于修改，幻读侧重于新增或删除。

解决不可重复读的问题只需锁住满足条件的行，解决幻读需要锁表





> 更新: 2024-05-01 16:15:40  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/wc0mtpi8op0lch8d>