# 11、MyBatis 如何获取自动生成的(主)键值

在<insert>标签中使用useGeneratedKeys 和keyProperty 两个属性来获取自动生成的主键值。

示例:

<font style="color:rgb(154,109,57);"><</font>insert id<font style="color:rgb(154,109,57);">=</font>”insertname” usegeneratedkeys<font style="color:rgb(154,109,57);">=</font>”<font style="color:rgb(153,0,84);">t</font><font style="color:rgb(153,0,84);">r</font><font style="color:rgb(153,0,84);">u</font><font style="color:rgb(153,0,84);">e</font>” keyproperty<font style="color:rgb(154,109,57);">=</font>”id”<font style="color:rgb(154,109,57);">> </font>insert into names <font style="color:rgb(153,153,153);">(</font>name<font style="color:rgb(153,153,153);">)</font><font style="color:rgb(153,153,153);"> </font>values <font style="color:rgb(153,153,153);">(</font>#<font style="color:rgb(153,153,153);">{</font>name<font style="color:rgb(153,153,153);">}</font><font style="color:rgb(153,153,153);">)</font>

<font style="color:rgb(154,109,57);"></</font>insert<font style="color:rgb(154,109,57);">></font>

> 更新: 2024-05-01 16:01:38  
