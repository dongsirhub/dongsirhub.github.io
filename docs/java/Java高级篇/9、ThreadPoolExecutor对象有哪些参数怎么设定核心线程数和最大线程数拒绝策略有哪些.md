# 9、ThreadPoolExecutor 对象有哪些参数 怎么设定核心线程数和最大线程数 拒绝策略有哪些

**参数与作用：**共7 个参数

(1) **corePoolSize****：**核心线程数，

<font style="background-color:rgb(192,192,192);">在</font><font style="background-color:rgb(192,192,192);">ThreadPoolExecutor</font><font style="background-color:rgb(192,192,192);"> </font><font style="background-color:rgb(192,192,192);">中有一个与它相关的配置：</font><font style="background-color:rgb(192,192,192);">allowCoreThreadTimeOut</font><font style="background-color:rgb(192,192,192);">（</font><font style="background-color:rgb(192,192,192);">默认</font><font style="background-color:rgb(192,192,192);">为</font><font style="background-color:rgb(192,192,192);">false</font><font style="background-color:rgb(192,192,192);">）</font><font style="background-color:rgb(192,192,192);">，当</font><font style="background-color:rgb(192,192,192);">allowCoreThreadTimeOut</font><font style="background-color:rgb(192,192,192);"> </font><font style="background-color:rgb(192,192,192);">为</font><font style="background-color:rgb(192,192,192);">false</font><font style="background-color:rgb(192,192,192);"> </font><font style="background-color:rgb(192,192,192);">时，核心线程会一直存活，</font><font style="background-color:rgb(192,192,192);">哪怕</font><font style="background-color:rgb(192,192,192);">是一直空闲着。而当</font><font style="background-color:rgb(192,192,192);">allowCoreThreadTimeOut</font><font style="background-color:rgb(192,192,192);"> </font><font style="background-color:rgb(192,192,192);">为</font><font style="background-color:rgb(192,192,192);">true</font><font style="background-color:rgb(192,192,192);"> </font><font style="background-color:rgb(192,192,192);">时核心线程空闲时间超过</font><font style="background-color:rgb(192,192,192);">keepAliveTime</font><font style="background-color:rgb(192,192,192);"> </font><font style="background-color:rgb(192,192,192);">时会被回收。</font>

(2) **maximumPoolSize****：**最大线程数

线程池能容纳的最大线程数，当线程池中的线程达到最大时，此时添加任务将会采用拒绝策略，默认的拒绝策略是抛出一个运行时错误

（RejectedExecutionException）。值得一提的是，当初始化时用的工作队列为

LinkedBlockingDeque 时，这个值将无效。

(3) **keepAliveTime****：**存活时间，

当非核心空闲超过这个时间将被回收，同时空闲核心线程是否回收受

allowCoreThreadTimeOut 影响。

(4) **unit****：**keepAliveTime 的单位。

(5) **workQueue****：**任务队列

常用有三种队列，即SynchronousQueue,LinkedBlockingDeque（无界队列）,ArrayBlockingQueue（有界队列）。

(6) **threadFactory****：**线程工厂，

ThreadFactory 是一个接口，用来创建worker。通过线程工厂可以对线程的一些属性进行定制。默认直接新建线程。

**(7)********RejectedExecutionHandler****：****拒绝策略**

也是一个接口，只有一个方法，当线程池中的资源已经全部使用，添加新线程被拒绝时，会调用RejectedExecutionHandler 的rejectedExecution 法。默认是抛出一个运行时异常。

**线程池大小设置：**

1. 需要分析线程池执行的任务的特性：CPU 密集型还是IO 密集型

2. 每个任务执行的平均时长大概是多少，这个任务的执行时长可能还跟任务处理逻辑是否涉及到网络传输以及底层系统资源依赖有关系

如果是CPU 密集型，主要是执行计算任务，响应时间很快，cpu 一直在运行，这种任务cpu 的利用率很高，那么线程数的配置应该根据CPU 核心数来决定，CPU

核心数=最大同时执行线程数，加入CPU 核心数为4，那么服务器最多能同时执行4 个线程。过多的线程会导致上下文切换反而使得效率降低。那线程池的最大线程数可以配置为cpu 核心数+1 如果是IO 密集型，主要是进行IO 操作，执行IO 操作的时间较长，这是cpu 出于空闲状态，导致cpu 的利用率不高，这种情况下可以增加线程池的大小。这种情况下可以结合线程的等待时长来做判断，等待时间越高，那么线程数也相对越多。一般可以配置cpu 核心数的2 倍。

一个公式：线程池设定最佳线程数目= （（线程池设定的线程等待时间+线程

CPU 时间）/

线程CPU 时间）* CPU 数目

这个公式的线程cpu 时间是预估的程序单个线程在cpu 上运行的时间（通常使用

loadrunner 测试大量运行次数求出平均值） **拒绝策略：**

1. AbortPolicy：直接抛出异常，默认策略；

2. CallerRunsPolicy：用调用者所在的线程来执行任务；

3. DiscardOldestPolicy：丢弃阻塞队列中靠最前的任务，并执行当前任务；

4. DiscardPolicy：直接丢弃任务；当然也可以根据应用场景实现RejectedExecutionHandler 接口，自定义饱和策略，如记录日志或持久化存储不能处理的任务

> 更新: 2024-04-30 18:21:04  
