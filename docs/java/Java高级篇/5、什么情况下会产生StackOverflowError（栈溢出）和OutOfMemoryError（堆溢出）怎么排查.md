# 5、什么情况下会产生 StackOverflowError（栈溢出）和OutOfMemoryError（堆溢出）怎么排查

(1) 引发StackOverFlowError 的常见原因有以下几种

● 无限递归循环调用（最常见）

● 执行了大量方法，导致线程栈空间耗尽

● 方法内声明了海量的局部变量

● native 代码有栈上分配的逻辑，并且要求的内存还不小，比

如java.net.SocketInputStream.read0 会在栈上要求分配一个64KB 的缓存（64 位

Linux）。

(2) 引发OutOfMemoryError 的常见原因有以下几种

● 内存中加载的数据量过于庞大，如一次从数据库取出过多数据

● 集合类中有对对象的引用，使用完后未清空，使得JVM 不能回收

● 代码中存在死循环或循环产生过多重复的对象实体

● 启动参数内存值设定的过小

l 排查：可以通过jvisualvm 进行内存快照分析

参考[https://www.cnblogs.com/boboooo/p/13164071.html](https://www.cnblogs.com/boboooo/p/13164071.html)



栈溢出、堆溢出案例演示

![1714467382101-c3e083fe-0dc0-42a3-a327-1a9b9c3a6c08.png](./img/jEP0N4-Y40_Lbh3k/1714467382101-c3e083fe-0dc0-42a3-a327-1a9b9c3a6c08-485664.png)

``<font style="color:rgb(0,119,170);">p</font><font style="color:rgb(0,119,170);">u</font><font style="color:rgb(0,119,170);">b</font><font style="color:rgb(0,119,170);">l</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);">l</font><font style="color:rgb(0,119,170);">a</font><font style="color:rgb(0,119,170);">s</font><font style="color:rgb(0,119,170);">s</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(221,73,104);">S</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">a</font><font style="color:rgb(221,73,104);">c</font><font style="color:rgb(221,73,104);">k</font><font style="color:rgb(221,73,104);">O</font><font style="color:rgb(221,73,104);">v</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">r</font><font style="color:rgb(221,73,104);">F</font><font style="color:rgb(221,73,104);">l</font><font style="color:rgb(221,73,104);">o</font><font style="color:rgb(221,73,104);">w</font><font style="color:rgb(221,73,104);">T</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">s</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);"> </font><font style="color:rgb(153,153,153);">{ </font><font style="color:rgb(0,119,170);">p</font><font style="color:rgb(0,119,170);">r</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">v</font><font style="color:rgb(0,119,170);">a</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">e</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">s</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">a</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">n</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);"> </font>count <font style="color:rgb(154,109,57);">=</font><font style="color:rgb(154,109,57);"> </font><font style="color:rgb(153,0,84);">1</font><font style="color:rgb(153,153,153);">;</font>

<font style="color:rgb(0,119,170);">                public static void </font><font style="color:rgb(221,73,104);">main</font><font style="color:rgb(153,153,153);">(</font><font style="color:rgb(221,73,104);">String</font><font style="color:rgb(153,153,153);">[] </font>args<font style="color:rgb(153,153,153);">) {</font>

<font style="color:rgb(144,159,174);">//模拟栈溢出</font>

<font style="color:rgb(144,159,174);">//getDieCircle();</font>

<font style="color:rgb(144,159,174);">                               //模拟堆溢出</font><font style="color:rgb(221,73,104);">getOutOfMem</font><font style="color:rgb(153,153,153);">();</font>

<font style="color:rgb(153,153,153);">}</font>

<font style="color:rgb(0,119,170);">p</font><font style="color:rgb(0,119,170);">u</font><font style="color:rgb(0,119,170);">b</font><font style="color:rgb(0,119,170);">l</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">s</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">a</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">v</font><font style="color:rgb(0,119,170);">o</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">d</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(221,73,104);">g</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">D</font><font style="color:rgb(221,73,104);">i</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">C</font><font style="color:rgb(221,73,104);">i</font><font style="color:rgb(221,73,104);">r</font><font style="color:rgb(221,73,104);">c</font><font style="color:rgb(221,73,104);">l</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(153,153,153);">()</font><font style="color:rgb(153,153,153);">{ </font><font style="color:rgb(221,73,104);">S</font><font style="color:rgb(221,73,104);">y</font><font style="color:rgb(221,73,104);">s</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">m</font><font style="color:rgb(153,153,153);">.</font>out<font style="color:rgb(153,153,153);">.</font><font style="color:rgb(221,73,104);">p</font><font style="color:rgb(221,73,104);">r</font><font style="color:rgb(221,73,104);">i</font><font style="color:rgb(221,73,104);">n</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">l</font><font style="color:rgb(221,73,104);">n</font><font style="color:rgb(153,153,153);">(</font>count<font style="color:rgb(154,109,57);">++</font><font style="color:rgb(153,153,153);">)</font><font style="color:rgb(153,153,153);">; </font><font style="color:rgb(221,73,104);">g</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">D</font><font style="color:rgb(221,73,104);">i</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">C</font><font style="color:rgb(221,73,104);">i</font><font style="color:rgb(221,73,104);">r</font><font style="color:rgb(221,73,104);">c</font><font style="color:rgb(221,73,104);">l</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(153,153,153);">()</font><font style="color:rgb(153,153,153);">;</font>

<font style="color:rgb(153,153,153);">}</font>

<font style="color:rgb(0,119,170);">p</font><font style="color:rgb(0,119,170);">u</font><font style="color:rgb(0,119,170);">b</font><font style="color:rgb(0,119,170);">l</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">s</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">a</font><font style="color:rgb(0,119,170);">t</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">c</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(0,119,170);">v</font><font style="color:rgb(0,119,170);">o</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">d</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(221,73,104);">g</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">O</font><font style="color:rgb(221,73,104);">u</font><font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">O</font><font style="color:rgb(221,73,104);">f</font><font style="color:rgb(221,73,104);">M</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">m</font><font style="color:rgb(153,153,153);">()</font><font style="color:rgb(153,153,153);">{ </font><font style="color:rgb(0,119,170);">w</font><font style="color:rgb(0,119,170);">h</font><font style="color:rgb(0,119,170);">i</font><font style="color:rgb(0,119,170);">l</font><font style="color:rgb(0,119,170);">e</font><font style="color:rgb(0,119,170);"> </font><font style="color:rgb(153,153,153);">(</font><font style="color:rgb(153,0,84);">t</font><font style="color:rgb(153,0,84);">r</font><font style="color:rgb(153,0,84);">u</font><font style="color:rgb(153,0,84);">e</font><font style="color:rgb(153,153,153);">)</font><font style="color:rgb(153,153,153);"> </font><font style="color:rgb(153,153,153);">{</font>

<font style="color:rgb(221,73,104);">                Object </font>o <font style="color:rgb(154,109,57);">= </font><font style="color:rgb(0,119,170);">new </font><font style="color:rgb(221,73,104);">Object</font><font style="color:rgb(153,153,153);">(); </font><font style="color:rgb(221,73,104);">System</font><font style="color:rgb(153,153,153);">.</font>out<font style="color:rgb(153,153,153);">.</font><font style="color:rgb(221,73,104);">println</font><font style="color:rgb(153,153,153);">(</font>o<font style="color:rgb(153,153,153);">);</font>

<font style="color:rgb(153,153,153);">          }</font>

<font style="color:rgb(153,153,153);">    }</font>

<font style="color:rgb(153,153,153);">}</font>

![1714467433944-72cf6643-5a7d-4d19-9422-5b7247196165.png](./img/jEP0N4-Y40_Lbh3k/1714467433944-72cf6643-5a7d-4d19-9422-5b7247196165-986994.png)

![1714467438904-014e16bd-1efe-4989-b5bb-5284a2e9f257.png](./img/jEP0N4-Y40_Lbh3k/1714467438904-014e16bd-1efe-4989-b5bb-5284a2e9f257-902684.png)



> 更新: 2024-04-30 16:58:17  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/ddo91gadttgg0kgw>