# 17、SpringBoot 配置文件有哪些 怎么实现多环境配置

Spring Boot 的核心配置文件是application 和bootstrap 配置文件。application 配置文件这个容易理解，主要用于Spring Boot 项目的自动化配置。**bootstrap 配置文件的特性：**

● bootstrap 由父ApplicationContext 加载，比applicaton 优先加载

● bootstrap 里面的属性不能被覆盖

**bootstrap 配置文件有以下几个应用场景：**

****

● 使用Spring Cloud Config 配置中心时，这时需要在bootstrap 配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息；

● 一些固定的不能被覆盖的属性；

● 一些加密/解密的场景； 提供多套配置文件，如：

applcation.properties

application-dev.properties application-test.properties application-prod.properties

运行时指定具体的配置文件，具体请看这篇文章《[SpringBootProfile不同环境配](https://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw%3D%3D&mid=2247484369&idx=1&sn=1155fccb4fef1db88cb76fd17b1756d7&scene=21)<u><font style="color:rgb(51,57,64);">置</font></u>》。

> 更新: 2024-05-01 16:05:17  
