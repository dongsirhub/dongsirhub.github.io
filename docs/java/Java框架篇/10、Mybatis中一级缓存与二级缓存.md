# 10、Mybatis 中一级缓存与二级缓存

(1) MyBatis 的缓存分为一级缓存和二级缓存。**一级缓存**是SqlSession 级别的缓存，默认开启。

**二级缓存**是NameSpace 级别(Mapper)的缓存，多个SqlSession 可以共享，使用时需要进行配置开启。



(2) 缓存的查找顺序：二级缓存=> 一级缓存=> 数据库



> 更新: 2024-05-01 16:01:11  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/fy03tgu66kma8fy8>