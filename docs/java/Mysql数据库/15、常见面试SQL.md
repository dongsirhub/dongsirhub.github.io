# 15、常见面试 SQL

**例1：**

用一条SQL 语句查询出每门课都大于80 分的学生姓名

name kecheng	fenshu

张三	语文	81

张三	数学	75

李四	语文	76

李四	数学	90

王五	语文	81

王五	数学	100

王五	英语	90

**<font style="color:rgb(233,30,44);">答</font>****<font style="color:rgb(233,30,44);">1</font>****<font style="color:rgb(233,30,44);">：</font>**

**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">distinct</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">name</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">table</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">name</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(139,139,139);">not</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(139,139,139);">in</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">distinct</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">name</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">table</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">w</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">here</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">fenshu<=80)</font>

**<font style="color:rgb(233,30,44);">答</font>****<font style="color:rgb(233,30,44);">2</font>****<font style="color:rgb(233,30,44);">：</font>**

**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">name</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">table</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">group</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">by</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">name having</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">min</font>**<font style="color:rgb(32,36,41);">(fenshu)>80</font>



**例****2****：**

学生表如下:

自动编号	学号	姓名	课程编号	课程名称	分数



| 1 | 2005001 | 张三 | 0001 | 数学 | 69 |
| :--- | ---: | ---: | :--- | :---: | ---: |
| 2 | 2005002 | 李四 | 0001 | 数学 | 89 |
| 3 | 2005001 | 张三 | 0001 | 数学 | 69 |


删除除了自动编号不同，其他都相同的学生冗余信息**<font style="color:rgb(233,30,44);">答：</font>**

  


****

**<font style="color:rgb(5,117,197);">delete</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">tablename</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">自动编号</font><font style="color:rgb(139,139,139);">not</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(139,139,139);">in</font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">min</font>**<font style="color:rgb(32,36,41);">(</font><font style="color:rgb(32,36,41);">自动编</font>

<font style="color:rgb(32,36,41);">号</font><font style="color:rgb(32,36,41);">) </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">tablename</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">group</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">by</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">学号</font><font style="color:rgb(32,36,41);">, </font><font style="color:rgb(32,36,41);">姓名</font><font style="color:rgb(32,36,41);">, </font><font style="color:rgb(32,36,41);">课程编号</font><font style="color:rgb(32,36,41);">, </font><font style="color:rgb(32,36,41);">课程名称</font><font style="color:rgb(32,36,41);">, </font><font style="color:rgb(32,36,41);">分数</font><font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>

****

**例3：**

一个叫team 的表，里面只有一个字段name,一共有4 条纪录，分别是a,b,c,d,对应

四个球队，现在四个球队进行比赛，用一条sql 语句显示所有可能的比赛组合.

**<font style="color:rgb(233,30,44);">答：</font>**

<font style="color:rgb(5,117,197);">1.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">a.</font>**<font style="color:rgb(5,117,197);">name</font>**<font style="color:rgb(32,36,41);">,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">b.</font>**<font style="color:rgb(5,117,197);">name</font>**

<font style="color:rgb(5,117,197);">2.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">team</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">a,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">team b</font>

<font style="color:rgb(5,117,197);">3. </font>**<font style="color:rgb(5,117,197);">where </font>**<font style="color:rgb(32,36,41);">a.</font>**<font style="color:rgb(5,117,197);">name </font>**<font style="color:rgb(32,36,41);">< b.</font>**<font style="color:rgb(5,117,197);">name</font>**

****

**例****4****：**

****

| 怎么把这样一个表 | | | | | | | |
| :--- | --- | --- | --- | --- | --- | --- | --- |
| year | month amount | | | | | | |
| 1991	1 | 1.1 | | | | | | |
| 1991	2 | 1.2 | | | | | | |
| 1991	3 | 1.3 | | | | | | |
| 1991	4 | 1.4 | | | | | | |
| 1992	1 | 2.1 | | | | | | |
| 1992	2 | 2.2 | | | | | | |
| 1992	3 | 2.3 | | | | | | |
| 1992	4 | 2.4 | | | | | | |
| 查成这样一个结果 | | | | | | | |
| year<br/>1991	1.1 | m1 | ****<br/>1.2 | m2 | ****<br/>1.3 | m3 | ****<br/>1.4 | m4 |
| 1992	2.1 |  | 2.2 |  | 2.3 |  | 2.4 |  |
| **<font style="color:rgb(233,30,44);">答：</font>** |  |  |  |  |  |  |  |


<font style="color:rgb(5,117,197);">1.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">,</font>

<font style="color:rgb(32,36,41);">2.</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">amount</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">aaa</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">m</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">month</font><font style="color:rgb(32,36,41);">=1</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(139,139,139);">and</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(32,36,41);">m.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">=aaa.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">m1,</font>

<font style="color:rgb(32,36,41);">3.</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">amount</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">aaa</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">m</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">month</font><font style="color:rgb(32,36,41);">=2</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(139,139,139);">and</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(32,36,41);">m.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">=aaa.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">m2,</font>

<font style="color:rgb(32,36,41);">4.</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">amount</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">aaa</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">m</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">month</font><font style="color:rgb(32,36,41);">=3</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(139,139,139);">and</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(32,36,41);">m.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">=aaa.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">m3,</font>

<font style="color:rgb(32,36,41);">5.</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">amount</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">aaa</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">m</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">month</font><font style="color:rgb(32,36,41);">=4</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(139,139,139);">and</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(32,36,41);">m.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">=aaa.</font><font style="color:rgb(199,20,182);">year</font><font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">m4</font>

<font style="color:rgb(5,117,197);">6.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">aaa</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">group</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">by</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">year</font>



**例5：**

说明：复制表(只复制结构,源表名：a 新表名：b)

**<font style="color:rgb(233,30,44);">答：</font>**

SQL:

**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">*</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">into</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">b</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">a</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">1<>1</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(where1=1</font><font style="color:rgb(32,36,41);">，拷贝表结构和数据内容</font><font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>ORACLE:

**<font style="color:rgb(5,117,197);">1.</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">create</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">table</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(32,36,41);">b</font>**

<font style="color:rgb(5,117,197);">2.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">As</font>**

<font style="color:rgb(5,117,197);">3. </font>**<font style="color:rgb(5,117,197);">Select </font>**<font style="color:rgb(32,36,41);">* </font>**<font style="color:rgb(5,117,197);">from </font>**<font style="color:rgb(32,36,41);">a </font>**<font style="color:rgb(5,117,197);">where </font>**<font style="color:rgb(32,36,41);">1=2</font>



[<>（不等于）(SQL Server Compact)



比较两个表达式。当使用此运算符比较非空表达式时，如果左操作数不等于右操作数，则结果为TRUE。否则，结果为FALSE。]



为了便于阅读,查询此表后的结果显式如下(及格分数为60):



写出此查询语句**<font style="color:rgb(233,30,44);">答：</font>**

**<font style="color:rgb(5,117,197);">select </font>**<font style="color:rgb(32,36,41);">courseid, coursename ,score ,if(score>=60, </font><font style="color:rgb(135,48,204);">"pass"</font><font style="color:rgb(32,36,41);">,</font><font style="color:rgb(135,48,204);">"fail"</font><font style="color:rgb(32,36,41);">) </font>**<font style="color:rgb(5,117,197);">as </font>**<font style="color:rgb(32,36,41);">mark </font>**<font style="color:rgb(5,117,197);">from </font>**<font style="color:rgb(32,36,41);">course</font>



| **例****7****：**<br/>表名：购物信息购物人商品名称 | <br/><br/><br/>数量 |  |
| :--- | --- | --- |
| A	甲 |  | 2 |
| B	乙 | 4 |  |
| C	丙 | 1 |  |
| A	丁 | 2 |  |
| B	丙 | 5 |  |




给出所有购入商品为两种或两种以上的购物人记录**<font style="color:rgb(233,30,44);">答：</font>**

**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">*</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">购物信息</font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">购物人</font><font style="color:rgb(139,139,139);">in</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select </font>**<font style="color:rgb(32,36,41);">购物人</font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">购物信息</font>**<font style="color:rgb(5,117,197);">group</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">by</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">购物</font>

<font style="color:rgb(32,36,41);">人</font>**<font style="color:rgb(5,117,197);">having</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(199,20,182);">count</font><font style="color:rgb(32,36,41);">(*</font><font style="color:rgb(32,36,41);">) >= 2);</font>





  


2005-05-10	1	2

**<font style="color:rgb(233,30,44);">答</font>****<font style="color:rgb(233,30,44);">1</font>****<font style="color:rgb(233,30,44);">：</font>**

**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">date</font>**<font style="color:rgb(32,36,41);">,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(199,20,182);">sum</font><font style="color:rgb(32,36,41);">(</font><font style="color:rgb(199,20,182);">case</font><font style="color:rgb(199,20,182);"> </font>**<font style="color:rgb(5,117,197);">when</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">result</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">=</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(135,48,204);">"win"</font><font style="color:rgb(135,48,204);"> </font>**<font style="color:rgb(5,117,197);">then</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">1</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">else</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">0</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">end</font>**<font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(135,48,204);">"win"</font><font style="color:rgb(32,36,41);">,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(199,20,182);">sum</font><font style="color:rgb(32,36,41);">(</font><font style="color:rgb(199,20,182);">case</font><font style="color:rgb(199,20,182);"> </font>**<font style="color:rgb(5,117,197);">wh</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">en</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">result </font><font style="color:rgb(32,36,41);">=</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(135,48,204);">"lose"</font><font style="color:rgb(135,48,204);"> </font>**<font style="color:rgb(5,117,197);">then </font>**<font style="color:rgb(32,36,41);">1</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">else</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">0</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">end</font>**<font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(135,48,204);">"lose"</font><font style="color:rgb(135,48,204);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">info</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">group</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">by</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">date</font>**<font style="color:rgb(32,36,41);">;</font>

**<font style="color:rgb(233,30,44);">答</font>****<font style="color:rgb(233,30,44);">2</font>****<font style="color:rgb(233,30,44);">：</font>**

<font style="color:rgb(5,117,197);">1.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">a.</font>**<font style="color:rgb(5,117,197);">date</font>**<font style="color:rgb(32,36,41);">,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">a.result</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">win,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">b.result</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">lose</font>

**<font style="color:rgb(5,117,197);">2.</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">from</font>**

<font style="color:rgb(32,36,41);">3.</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select date</font>**<font style="color:rgb(32,36,41);">, </font><font style="color:rgb(199,20,182);">count</font><font style="color:rgb(32,36,41);">(result) </font>**<font style="color:rgb(5,117,197);">as </font>**<font style="color:rgb(32,36,41);">result </font>**<font style="color:rgb(5,117,197);">from </font>**<font style="color:rgb(32,36,41);">info </font>**<font style="color:rgb(5,117,197);">where </font>**<font style="color:rgb(32,36,41);">result = </font><font style="color:rgb(135,48,204);">"win" </font>**<font style="color:rgb(5,117,197);">group </font>****<font style="color:rgb(5,117,197);">by d</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">ate</font>**<font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">a</font>

<font style="color:rgb(139,139,139);">4.</font><font style="color:rgb(139,139,139);"> </font><font style="color:rgb(139,139,139);">join</font>

<font style="color:rgb(32,36,41);">5.</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">(</font>**<font style="color:rgb(5,117,197);">select</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">date</font>**<font style="color:rgb(32,36,41);">,</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(199,20,182);">count</font><font style="color:rgb(32,36,41);">(result)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">result</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">from</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">info</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">where</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">result</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">=</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(135,48,204);">"lose"</font><font style="color:rgb(135,48,204);"> </font>**<font style="color:rgb(5,117,197);">group</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">by</font>****<font style="color:rgb(5,117,197);"> </font>****<font style="color:rgb(5,117,197);">date</font>**<font style="color:rgb(32,36,41);">)</font><font style="color:rgb(32,36,41);"> </font>**<font style="color:rgb(5,117,197);">as</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">b</font>

<font style="color:rgb(5,117,197);">6.</font><font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(5,117,197);">on</font>****<font style="color:rgb(5,117,197);"> </font>**<font style="color:rgb(32,36,41);">a.</font>**<font style="color:rgb(5,117,197);">date </font>**<font style="color:rgb(32,36,41);">=</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">b.</font>**<font style="color:rgb(5,117,197);">date</font>**<font style="color:rgb(32,36,41);">;</font>



例9 

mysql 创建了一个联合索引(a,b,c) 以下索引生效的是(1,2,4）



1、where a = 1 and b = 1 and c =1 

2、where a = 1 and c = 1

3、where b = 1 and c = 1,

4、where b = 1 and a =1 and c = 1



> 更新: 2024-05-01 16:25:19  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/gvca8twgogore7go>