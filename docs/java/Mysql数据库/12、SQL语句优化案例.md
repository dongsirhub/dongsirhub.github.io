# 12、SQL 语句优化案例

**例1：where 子句中可以对字段进行null 值判断吗？**

可以，比如select id from t where num is null 这样的sql 也是可以的。但是最好不要给数据库留NULL，尽可能的使用NOT NULL 填充数据库。不要以为NULL 不需要空间，比如：char(100) 型，在字段建立时，空间就固定了，不管是否插入值（NULL 也包含在内），都是占用100 个字符的空间的，如果是varchar 这样的变长字段，null 不占用空间。可以在num 上设置默认值0，确保表中num 列没有null 值，然后这样查询：select id from t where num= 0。

**例****2****：如何优化****?****下面的语句？**

select * from admin left	join	log on admin.admin_id	= log.admin_id where log.admin_id>10

优化为：select * from (select * from admin where admin_id>10) T1 lef join log on T1.admin_id = log.admin_id。

使用JOIN 时候，应该用小的结果驱动大的结果（left join 左边表结果尽量小如果有条件应该放到左边先处理，right join 同理反向），同时尽量把牵涉到多表联合的查询拆分多个query（多个连表查询效率低，容易到之后锁表和阻塞）。

**例****3****：****limit**** ****的基数比较大时使用****between**

例如：select * from admin order by admin_id limit 100000,10



优化为：select * from admin where admin_id between 100000 and 100010 order by admin_id。

**例****4****：尽量避免在列上做运算，这样导致索引失效**

例如：select * from admin where year(admin_time)>2014



优化为：select * from admin where admin_time> '2014-01-01′



> 更新: 2024-05-01 16:21:58  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/gk8zgwuvqhvg4sgp>