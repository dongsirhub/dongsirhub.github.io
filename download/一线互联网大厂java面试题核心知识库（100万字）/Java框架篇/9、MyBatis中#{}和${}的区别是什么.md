# 9、MyBatis 中 #{}和${}的区别是什么

#{}是预编译处理，${}是字符串替换；



Mybatis 在处理#{}时，会将sql 中的#{}替换为?号，调用PreparedStatement 的set

方法来赋值；



Mybatis 在处理${}时，就是把${}替换成变量的值；



使用#{}可以有效的防止SQL 注入，提高系统安全性。



> 更新: 2024-05-01 16:00:50  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/gyay7mtt143r8cdy>