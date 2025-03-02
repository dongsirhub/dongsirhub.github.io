# 4、如何判断一个对象是否存活(或者GC 对象的判定方法)

##### **难度系数：**⭐
**(1)**** ****引用计数法**

所谓引用计数法就是给每一个对象设置一个引用计数器，每当有一个地方引用这个对象时，就将计数器加一，引用失效时，计数器就减一。当一个对象的引用计数器为零时，说明此对象没有被引用，也就是“死对象”,将会被垃圾回收.

引用计数法有一个缺陷就是无法解决循环引用问题，也就是说当对象A 引用对象B，对象B 又引用者对象A，那么此时A,B 对象的引用计数器都不为零，也就造成无法完成垃圾回收，所以主流的虚拟机都没有采用这种算法。

**(2) 可达性算法(引用链法)**

<font style="color:rgb(32,36,41);">●</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">该算法的基本思路就是通过一些被称为引用链（</font><font style="color:rgb(32,36,41);">GC</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">Roots</font><font style="color:rgb(32,36,41);">）的对象作为起点，从这些节点开始向下搜索，搜索走过的路径被称为（</font><font style="color:rgb(32,36,41);">Reference</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">Chain)</font><font style="color:rgb(32,36,41);">，当</font><font style="color:rgb(32,36,41);">一个对象到</font><font style="color:rgb(32,36,41);">GC Roots</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">没有任何引用链相连时</font><font style="color:rgb(32,36,41);">（</font><font style="color:rgb(32,36,41);">即从</font><font style="color:rgb(32,36,41);">GC</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">Roots</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">节点到该节点不可达），则证明该对象是不可用的。</font>

● 在java 中可以作为GC Roots 的对象有以下几种：虚拟机栈中引用的对象、方法区类静态属性引用的对象、方法区常量池引用的对象、本地方法栈JNI 引用的对象。



> 更新: 2024-04-30 16:55:42  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/qv6g5unc5yufdnqs>