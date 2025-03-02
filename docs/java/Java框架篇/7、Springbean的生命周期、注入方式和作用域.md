# 7、Spring bean 的生命周期、注入方式和作用域

**Bean 的生命周期**

（1） 默认情况下，IOC 容器中bean 的生命周期分为五个阶段:



● 调用构造器或者是通过工厂的方式创建Bean 对象



● 给bean 对象的属性注入值



● 调用初始化方法，进行初始化，初始化方法是通过init-method 来指定的.



● 使用



● IOC 容器关闭时，销毁Bean 对象.



（2） 当加入了Bean 的后置处理器后，IOC 容器中bean 的生命周期分为七个阶段:



● 调用构造器或者是通过工厂的方式创建Bean 对象



● 给bean 对象的属性注入值



● 执行Bean 后置处理器中的postProcessBeforeInitialization



● 调用初始化方法，进行初始化，初始化方法是通过init-method 来指定的.x



● 执行Bean 的后置处理器中postProcessAfterInitialization



● 使用



● IOC 容器关闭时，销毁Bean 对象



<font style="color:rgb(233,30,44);">只需要回答出第一点即可，第二点也回答可适当</font><font style="color:rgb(233,30,44);">加分。</font>**注入方式：**

通过setter 方法注入



通过构造方法注入

**Bean**** ****的作用域**

总共有四种作用域:



● Singleton 单例的

  




● Prototype 原型的

● Request

● Session



> 更新: 2024-05-01 16:00:00  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/emv1v4lrqcr7fkw4>