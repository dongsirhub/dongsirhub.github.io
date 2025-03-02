# 12、synchronized 底层实现是什么 lock 底层是什么 有什么区别

**Synchronized 原理：**

**方法级的同步是隐式，即无需通过字节码指令来控制的，它实现在方法调用和返回操****作之中。**JVM 可以从方法常量池中的方法表结构(method_info Structure) 中的ACC_SYNCHRONIZED 访问标志区分一个方法是否同步方法。当方法调用时，调用指令将会检查方法的ACC_SYNCHRONIZED 访问标志是否被设置，如果设置了，执行线程将先持有monitor（虚拟机规范中用的是管程一词），然后再执行方法，最后再方

法完成(无论是正常完成还是非正常完成)时释放monitor。

**代码块的同步是利用****monitorenter**** ****和****monitorexit**** ****这两个字节码指令。它们分别位于****同步代码块的开始和结束位置**。当jvm 执行到monitorenter 指令时，当前线程试图获取monitor 对象的所有权，如果未加锁或者已经被当前线程所持有，就把锁的计数

器+1；当执行monitorexit 指令时，锁计数器-1；当锁计数器为0 时，该锁就被释放了。如果获取monitor 对象失败，该线程则会进入阻塞状态，直到其他线程释放锁。

<font style="color:rgb(0,0,255);">参考：</font>[https://blog.csdn.net/ben040661/article/details/125697819](https://blog.csdn.net/ben040661/article/details/125697819)

**Lock****原理：**

1. Lock 的存储结构：一个int 类型状态值（用于锁的状态变更），一个双向链表

（用于存储等待中的线程）



2. Lock 获取锁的过程：本质上是通过CAS 来获取状态值修改，如果当场没获取到，会将该线程放在线程等待链表中。

3. Lock 释放锁的过程：修改状态值，调整等待链表。



4. Lock 大量使用CAS+自旋。因此根据CAS 特性，lock 建议使用在低锁冲突的情况下。

**Lock****与****synchronized**** ****的区别：**

1. Lock 的加锁和解锁都是由java 代码配合native 方法（调用操作系统的相关方法）实现的，而synchronize 的加锁和解锁的过程是由JVM 管理的

2. 当一个线程使用 synchronize 获取锁时，若锁被其他线程占用着，那么当前只能被阻塞，直到成功获取锁。而 Lock 则提供超时锁和可中断等更加灵活的方式，在未能获取锁的	条件下提供一种退出的机制。

3. 一个锁内部可以有多个Condition 实例，即有多路条件队列，而synchronize 只有一路条件队列；同样Condition 也提供灵活的阻塞方式，在未获得通知之前可以通过中断线程以及设置等待时限等方式退出条件队列。

4. synchronize 对线程的同步仅提供独占模式，而Lock 即可以提供独占模式，也可以提供共享模式




| synchronized | Lock |
| :---: | :---: |
| 关键字 | 类 |
| 自动加锁和释放锁 | 需要手动调用 unlock 方法释放锁 |
| jvm 层面的锁 | API 层面的锁 |
| 非公平锁 | 可以选择公平或者非公平锁 |
| 锁是一个对象,并且锁的信息保存在了对象中 | 代码中通过 int 类型的 state 标识 |
| 有一个锁升级的过程 | 无 |




> 更新: 2024-04-30 18:22:36  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/xyk7hag9bnv9wxrg>