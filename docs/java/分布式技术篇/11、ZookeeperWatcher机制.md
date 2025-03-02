# 11、Zookeeper Watcher 机制

Zookeeper 允许客户端向服务端的某个Znode 注册一个Watcher 监听，当服务端的一些指定事件触发了这个Watcher，服务端会向指定客户端发送一个事件通知来实现分布式的通知功能，然后客户端根据Watcher 通知状态和事件类型做出业务上的改变。

**工作机制：**

● 客户端注册watcher



● 服务端处理watcher



● 客户端回调watcher

**Watcher**** ****特性总结：**



****

（1） 一次性

无论是服务端还是客户端，一旦一个Watcher 被触发，Zookeeper 都会将其从相应的存储中移除。这样的设计有效的减轻了服务端的压力，不然对于更新非常频繁的节 点，服务端会不断的向客户端发送事件通知，无论对于网络还是服务端的压力都非常大。

（2） 客户端串行执行

客户端Watcher 回调的过程是一个串行同步的过程。



（3） 轻量



Watcher 通知非常简单，只会告诉客户端发生了事件，而不会说明事件的具体内容。



客户端向服务端注册Watcher 的时候，并不会把客户端真实的Watcher 对象实体传递到服务端，仅仅是在客户端请求中使用boolean 类型属性进行了标记。

watcher event 异步发送watcher 的通知事件从server 发送到client 是异步的，这就存在一个问题，不同的客户端和服务器之间通过socket 进行通信，由于网络延迟或其他因素导致客户端在不通的时刻监听到事件，由于Zookeeper 本身提供了ordering guarantee，即客户端监听事件后，才会感知它所监视znode 发生了变化。所以我们使用Zookeeper 不能期望能够监控到节点每次的变化。Zookeeper 只能保证最终的一致性，而无法保证强一致性。

注册watcher getData、exists、getChildren



触发watcher create、delete、setData



当一个客户端连接到一个新的服务器上时，watch 将会被以任意会话事件触发。当与一个服务器失去连接的时候，是无法接收到watch 的。而当client 重新连接时，如果需要的话，所有先前注册过的watch，都会被重新注册。通常这是完全透明的。只有在一个特殊情况下，watch 可能会丢失：对于一个未创建的znode 的exist watch，如果在客户端断开连接期间被创建了，并且随后在客户端连接上之前又删除了，这种情况下，这个watch 事件可能会被丢失。



> 更新: 2024-05-01 16:36:11  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/cpqh7t3rle01u88b>