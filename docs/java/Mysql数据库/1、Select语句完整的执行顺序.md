# 1、Select 语句完整的执行顺序

SQL Select 语句完整的执行顺序：



（1） from 子句组装来自不同数据源的数据；



（2） where 子句基于指定的条件对记录行进行筛选；



（3） group by 子句将数据划分为多个分组；



（4） 使用聚集函数进行计算；



（5） 使用having 子句筛选分组；



（6） 计算所有的表达式；



（7） select 的字段；



使用order by 对结果集进行排序



> 更新: 2024-05-01 16:09:13  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/aurcmcb96ontnp4v>