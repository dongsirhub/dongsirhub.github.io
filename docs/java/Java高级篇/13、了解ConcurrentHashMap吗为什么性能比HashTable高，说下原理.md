# 13、了解 ConcurrentHashMap 吗 为什么性能比HashTable 高，说下原理

ConcurrentHashMap 是线程安全的Map 容器，JDK8 之前，ConcurrentHashMap 使用锁分段技术，将数据分成一段段存储，每个数据段配置一把锁，即segment 类，这个类继承ReentrantLock 来保证线程安全，JKD8 的版本取消Segment 这个分段锁数据结构，底层也是使用Node 数组+链表+红黑树，从而实现对每一段数据就行加锁，也减少了并发冲突的概率。

hashtable 类基本上所有的方法都是采用synchronized 进行线程安全控制，高并发情况下效率就降低，ConcurrentHashMap 是采用了分段锁的思想提高性能，锁粒度更细化

> 更新: 2024-04-30 18:28:51  
