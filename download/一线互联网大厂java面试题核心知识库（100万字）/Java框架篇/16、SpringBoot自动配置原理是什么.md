# 16、Spring Boot 自动配置原理是什么

注解@EnableAutoConfiguration, @Configuration, @ConditionalOnClass 就是自动配置的核心，

首先它得是一个配置文件，其次根据类路径下是否有这个类去自动配置。



@EnableAutoConfiguration 是实现自动配置的注解



@Configuration 表示这是一个配置文件具体参考文档：

[https://mp.weixin.qq.com/s?biz=MzI3ODcxMzQzMw==&mid=2247484365&idx=1](https://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw%3D%3D&mid=2247484365&idx=1&sn=a4ab1d977d6b03bf122b4d596d7ee1ab&scene=21)

<u><font style="color:rgb(51,57,64);">&sn=a4ab1d977d6b03bf122b4d596d7ee1ab&scene=21</font></u>

<u><font style="color:rgb(51,57,64);"></font></u>



> 更新: 2024-05-01 16:04:42  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/dzr6tkfgl5ii9n67>