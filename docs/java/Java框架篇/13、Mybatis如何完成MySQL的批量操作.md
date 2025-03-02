# 13、Mybatis 如何完成 MySQL 的批量操作

MyBatis 完成 MySQL 的批量操作主要是通过<foreach>标签来拼装相应的 SQL 语句

例如:

<font style="color:rgb(154,109,57);"><</font>insert<font style="color:rgb(154,109,57);">*</font><font style="color:rgb(154,109,57);">*</font><font style="color:rgb(154,109,57);"> </font>id<font style="color:rgb(154,109,57);">=</font><font style="color:rgb(102,153,0);">"</font><font style="color:rgb(102,153,0);">i</font><font style="color:rgb(102,153,0);">n</font><font style="color:rgb(102,153,0);">s</font><font style="color:rgb(102,153,0);">e</font><font style="color:rgb(102,153,0);">r</font><font style="color:rgb(102,153,0);">t</font><font style="color:rgb(102,153,0);">B</font><font style="color:rgb(102,153,0);">a</font><font style="color:rgb(102,153,0);">t</font><font style="color:rgb(102,153,0);">c</font><font style="color:rgb(102,153,0);">h</font><font style="color:rgb(102,153,0);">"</font><font style="color:rgb(102,153,0);"> </font><font style="color:rgb(154,109,57);">></font>

insert into <font style="color:rgb(221,73,104);">t</font><font style="color:rgb(221,73,104);">b</font><font style="color:rgb(221,73,104);">l</font><font style="color:rgb(221,73,104);">_</font><font style="color:rgb(221,73,104);">e</font><font style="color:rgb(221,73,104);">m</font><font style="color:rgb(221,73,104);">p</font><font style="color:rgb(221,73,104);">l</font><font style="color:rgb(221,73,104);">o</font><font style="color:rgb(221,73,104);">y</font><font style="color:rgb(221,73,104);">ee</font><font style="color:rgb(153,153,153);">(</font>last_name<font style="color:rgb(153,153,153);">,</font>email<font style="color:rgb(153,153,153);">,</font>gender<font style="color:rgb(153,153,153);">,</font>d_id<font style="color:rgb(153,153,153);">)</font><font style="color:rgb(153,153,153);"> </font>values

<font style="color:rgb(154,109,57);"><</font>foreach<font style="color:rgb(154,109,57);">** </font>collection<font style="color:rgb(154,109,57);">=</font><font style="color:rgb(102,153,0);">"emps" </font>item<font style="color:rgb(154,109,57);">=</font><font style="color:rgb(102,153,0);">"curr_emp" </font>separator<font style="color:rgb(154,109,57);">=</font><font style="color:rgb(102,153,0);">","</font><font style="color:rgb(154,109,57);">**></font>

<font style="color:rgb(154,109,57);"></font>

<font style="color:rgb(153,153,153);">(</font>#<font style="color:rgb(153,153,153);">{</font>curr_emp<font style="color:rgb(153,153,153);">.</font>lastName<font style="color:rgb(153,153,153);">}</font><font style="color:rgb(153,153,153);">,</font>#<font style="color:rgb(153,153,153);">{</font>curr_emp<font style="color:rgb(153,153,153);">.</font>email<font style="color:rgb(153,153,153);">}</font><font style="color:rgb(153,153,153);">,</font>#<font style="color:rgb(153,153,153);">{</font>curr_emp<font style="color:rgb(153,153,153);">.</font>gender<font style="color:rgb(153,153,153);">}</font><font style="color:rgb(153,153,153);">,</font>#<font style="color:rgb(153,153,153);">{</font>curr_emp<font style="color:rgb(153,153,153);">.</font>dept<font style="color:rgb(153,153,153);">.</font>id<font style="color:rgb(153,153,153);">}</font>

<font style="color:rgb(153,153,153);">)</font>

<font style="color:rgb(154,109,57);"></</font>foreach<font style="color:rgb(154,109,57);">></font>

<font style="color:rgb(154,109,57);"></</font>insert<font style="color:rgb(154,109,57);">></font>



> 更新: 2024-05-01 16:02:38  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/uxdc7ufxkus9yfq6>