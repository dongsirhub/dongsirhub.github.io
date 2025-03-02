# 3、Java 中垃圾收集的方法有哪些

**<font style="color:rgb(0,0,255);">采用分区分代回收思想：</font>**

l **<font style="color:rgb(32,36,41);">复制算法</font>**<font style="color:rgb(32,36,41);">年轻代中使用的是</font><font style="color:rgb(32,36,41);">Minor</font><font style="color:rgb(32,36,41);"> GC</font><font style="color:rgb(32,36,41);">，这种</font><font style="color:rgb(32,36,41);">GC</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">算法采用的是复制算法</font>

<font style="color:rgb(32,36,41);">(Copying)</font>

<font style="color:rgb(32,36,41);">a) 效率高，缺点：需要内存容量大，比较耗内存</font>

<font style="color:rgb(32,36,41);">b)</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">使用在占空间比较小、刷新次数多的新生区</font>

<font style="color:rgb(32,36,41);">l</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(32,36,41);">标记</font>****<font style="color:rgb(32,36,41);">-</font>****<font style="color:rgb(32,36,41);">清除</font>**<font style="color:rgb(32,36,41);">老年代一般是由标记清除或者是标记清除与标记整理的混合实现</font>

<font style="color:rgb(32,36,41);">a</font><font style="color:rgb(32,36,41);">) </font><font style="color:rgb(32,36,41);">效率比较低，会差生碎片。</font>

<font style="color:rgb(32,36,41);">l</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(32,36,41);">标记</font>****<font style="color:rgb(32,36,41);">-</font>****<font style="color:rgb(32,36,41);">整理</font>**<font style="color:rgb(32,36,41);">老年代一般是由标记清除或者是标记清除与标记整理的混合实现</font>

<font style="color:rgb(32,36,41);">a) 效率低速度慢，需要移动对象，但不会产生碎片。</font>



> 更新: 2024-04-30 16:55:31  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/drggh27dsluyqpw5>