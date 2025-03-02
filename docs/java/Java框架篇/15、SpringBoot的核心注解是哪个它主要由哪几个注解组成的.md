# 15、Spring Boot 的核心注解是哪个 它主要由哪几个注解组成的

启动类上面的注解是@SpringBootApplication，它也是Spring Boot 的核心注解，主要组合包含了以下3 个注解：



● @SpringBootConfiguration：组合了@Configuration 注解，实现配置文件的功能。

● @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，

● 如关闭数据源自动配置功能：@SpringBootApplication(exclude =

{ DataSourceAutoConfiguration.class })。



● @ComponentScan：Spring 组件扫描。



> 更新: 2024-05-01 16:04:18  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/lexw4qkvobl1grnz>