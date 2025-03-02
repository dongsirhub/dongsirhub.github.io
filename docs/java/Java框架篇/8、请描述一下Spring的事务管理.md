# 8、请描述一下 Spring 的事务管理

（1） 声明式事务管理的定义：用在Spring 配置文件中声明式的处理事务来代替代码式的处理事务。这样的好处是，事务管理不侵入开发的组件，具体来说，业务逻辑对象就不会意识到正在事务管理之中，事实上也应该如此，因为事务管理是属于系统层面的服务，而不是业务逻辑的一部分，如果想要改变事务管理策划的话，也只需要在定义文件中重新配置即可，这样维护起来极其方便。

基于TransactionInterceptor 的声明式事务管理：两个次要的属性： transactionManager，用来指定一个事务治理器，并将具体事务相关的操作请托给它；其他一个是Properties 类型的transactionAttributes 属性，该属性的每一个键值对中，键指定的是方法名，方法名可以行使通配符，而值就是表现呼应方法的所运用的事务属性。

（2） 基于@Transactional 的声明式事务管理：Spring 2.x 还引入了基于Annotation 的体式格式，具体次要触及@Transactional 标注。@Transactional 可以浸染于接口、接口方法、类和类方法上。算作用于类上时，该类的一切public 方法将都具有该类型的事务属性。

（3） 编程式事物管理的定义：在代码中显式挪用beginTransaction()、commit()、rollback()等事务治理相关的方法，这就是编程式事务管理。Spring 对事物的编程式管理有基于底层API 的编程式管理和基于TransactionTemplate 的编程式事务管理两种方式。



> 更新: 2024-05-01 16:00:25  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/qnk7naflpe25yrr5>