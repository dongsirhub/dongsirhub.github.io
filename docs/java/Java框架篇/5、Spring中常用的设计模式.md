# 5、Spring 中常用的设计模式

(1) 代理模式——spring 中两种代理方式，若目标对象实现了若干接口，spring 使用jdk 的java.lang.reflect.Proxy 类代理。若目标兑现没有实现任何接口，spring 使用CGLIB 库生成目标类的子类。

(2) 单例模式——在spring 的配置文件中设置bean 默认为单例模式。



(3) 模板方式模式——用来解决代码重复的问题。



(4) 比如：RestTemplate、JmsTemplate、JpaTemplate



(5) 工厂模式——在工厂模式中，我们在创建对象时不会对客户端暴露创建逻辑，并且是通过使用同一个接口来指向新创建的对象。Spring 中使用beanFactory 来创建对象的实例。



> 更新: 2024-05-01 15:28:40  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/pnncm5qghm0lipy3>