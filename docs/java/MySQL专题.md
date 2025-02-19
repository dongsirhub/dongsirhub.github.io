1.1.数据库基础知识

### 1.1.1.范式化设计

#### 1.1.1.1.什么是范式

范式来自英文Normal Form，简称NF。

实际上你可以把它粗略地理解为 **一张数据表的表结构所符合的某种设计标准的级别** 。就像家里装修买建材，最环保的是E0级，其次是E1级，还有E2级等等

目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式5NF，又称完美范式）。

满足最低要求的范式是第一范式（1NF），在第一范式的基础上进一步满足更多规范要求的称为第二范式（2NF），其余范式以次类推。一般来说，数据库只需满足第三范式(3NF）就行了。![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/85d0baa6c50443d292669b21453b4553.png)

#### 1.1.1.2.第一范式（1NF）

定义： 属于第一范式关系的所有属性都不可再分，即数据项不可分。

理解：第一范式强调数据表的原子性，是其他范式的基础。一张表有一个name-age列，这个列具有两个属性，一个name,一个 age，所以不符合第一范式，我们把它拆分成两列name和age，这张表就符合第一范式关系。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/166049f492a3467f82ad60fff2de2ed3.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/685b406406ae467c886692941525bba0.png)

你在关系型数据库管理系统（RDBMS），例如SQL Server，Oracle，MySQL中创建数据表的时候，1NF是所有关系型数据库设计的最基本要求。

**第一范式详细的要求如下：**

1、每一列属性都是不可再分的属性值，确保每一列的原子性；

2、两列的属性相近或相似或一样，尽量合并属性一样的列，确保不产生冗余数据；

3、单一属性的列为基本数据类型构成；

4、设计出来的表都是简单的二维表。

#### 1.1.1.2.第二范式（2NF）

第二范式（2NF）是在第一范式（1NF）的基础上建立起来的，即满足第二范式（2NF）必须先满足第一范式（1NF）。

第二范式（2NF）要求实体的属性完全依赖于主关键字。![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/361ffcc4c44944e584efeb889ccb5c4b.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6cbd918d8b8b45318a64076e26b7fd02.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/29507df53b5f48ed9539bbf64f682cca.png)

以上这张表不符合第二范式（2NF），虽然有主键，但是实体的属性不完全依赖于主关键字。

所谓完全依赖是指不能存在仅依赖主关键字一部分的属性，如果存在，那么这个属性和主关键字的这一部分应该分离出来形成一个新的实体，新实体与原实体之间是一对多的关系。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2de641a78ace4a6bb1ee9a84331e5472.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/7ae62a49fb76431f912a42924885d9a7.png)

设计成两张表，主键分别是id和op_id，这样就符合第二范式（2NF）。

#### 1.1.1.3.第三范式（3NF）

满足第三范式（3NF）必须先满足第二范式（2NF）；

第三范式（3NF）要求一个数据库表中不包含已在其它表中包含的非主关键字信息，即数据不能存在传递关系，即每个属性都跟主键有直接关系而不是间接关系。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/5b5862b761da4130bdb21eb1f9735039.png)

产品表

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/1669ce8c28e749a4abdfe06f9133bbd8.png)

这里如果产品ID或产品名称变化会发生什么情况？所以以上不符合第三范式（3NF）

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/183c600ae6ca471a80677bc034c63274.png)

以上订单表就符合第三范式

### 1.1.2.反范式化设计

完全符合范式化的设计真的完美无缺吗？很明显在实际的业务查询中会大量存在着表的关联查询，而表设计都做成了范式化设计（甚至很高的范式），大量的表关联很多的时候非常影响查询的性能。

**反范式化就是违反范式化设计：**

1、为了性能和读取效率而适当的违反对数据库设计范式的要求；

2、为了查询的性能，允许存在部分（少量）冗余数据

**换句话来说反范式化就是使用空间来换取时间。**

### 1.1.3.范式化和反范式对比

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/e8e525cf363942a2b56093310ec4e3fe.png)

1、范式化的更新操作通常比反范式化要快（字段较少）。

2、当数据较好地范式化时，就只有很少或者没有重复数据，所以只需要修改更少的数据。

3、范式化的表通常更小，所以占据的内存更少。

4、范式化设计的缺点是通常需要关联，稍微复杂一些的查询语句在符合范式的表上都可能需要至少一次关联，也许更多。

5、复杂一些的查询语句也可能使一些索引策略无效。例如，范式化可能将列存放在不同的表中，而这些列如果在一个表中本可以属于同一个索引。

### 1.1.4.项目中常见的反范式实现

范式化和反范式化的各有优劣，**怎么选择最佳的设计?小孩子才做选择，我们全都要！！！**

#### 1.1.4.1.缓存与汇总数据

**“缓存”来表示存储那些可以比较简单地从其他表获取数据的表。**

比如从父表冗余一些数据到子表的。前面我们看到的分类信息放到商品表里面进行冗余存放就是典型的例子。

**“汇总”则保存的是使用GROUP BY语句聚合数据的表。**

如果需要显示每个用户发了多少消息，可以每次执行一个对用户发送消息进行count的子查询来计算并显示它，也可以在user表用户中建一个消息发送数目的专门列，每当用户发新消息时更新这个值。

在使用缓存表和汇总表时，有个关键点是如何维护缓存表和汇总表中的数据，常用的有两种方式，实时维护数据和定期重建，这个取决于应用程序，不过一般来说，缓存表用实时维护数据更多点，往往在一个事务中同时更新数据本表和缓存表，汇总表则用定期重建更多，使用定时任务对汇总表进行更新。

#### 1.1.4.2.计数器表设计

计数器表在Web应用中很常见。比如网站点击数、用户的朋友数、文件下载次数等。对于高并发下的处理，首先可以创建一张独立的表存储计数器，这样可使计数器表小且快，并且可以使用一些更高级的技巧。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b45835bb11424246b792d9d4d19fb23c.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/cd385ee871054bd3ae93a53a6d633d79.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/779011d6a8384c40904b4d8ac69a0b5b.png)

比如假设有一个计数器表，只有一行数据，记录网站的点击次数，网站的每次点击都会导致对计数器进行更新，问题在于，对于任何想要更新这一行的事务来说，这条记录上都有一个全局的互斥锁(mutex)。这会使得这些事务只能串行执行，会严重限制系统的并发能力。

怎么改进呢？可以将计数器保存在多行中，每次随机选择一行进行更新。在具体实现上，可以增加一个槽（slot)字段，然后预先在这张表增加100行或者更多数据，当对计数器更新时，选择一个随机的槽（slot)进行更新即可。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/bcee9d54deb64453a79326c0186fa43e.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/03d4f890b1044b1aa08b41bf7761e425.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8c843b05fb3c4ee093c1e6baadf6ce66.png)

### 1.1.4.字段数据类型优化

MySQL支持的数据类型非常多，选择正确的数据类型对于获得高性能至关重要。不管存储哪种类型的数据，下面几个简单的原则都有助于做出更好的选择。

#### 1.1.4.1.字段优化基本原则

* **更小的通常更好**

一般情况下,应该尽量使用可以正确存储数据的最小数据类型。更小的数据类型通常更快，因为它们占用更少的磁盘、内存和CPU缓存，并且处理时需要的CPU周期也更少。

比如：是有一个类型既可以用字符串也可以使用整型，**优先选择整型**。因为字符串牵涉到了字符集及校对规则等。

* **简单就好**

简单数据类型的操作通常需要更少的CPU周期。例如，整型比字符操作代价更低，因为字符集和校对规则(排序规则)使字符比较比整型比较更复杂。比如应该使用MySQL内建的类型而不是字符串来存储日期和时间。

* **尽量避免NULL**

通常情况下最好指定列为NOT NULL，除非真的需要存储NULL值。

如果查询中包含可为NULL的列，对MySQL来说更难优化，因为可为NULL的列使得索引、索引统计和值比较都更复杂。可为NULL的列会使用更多的存储空间，在MySQL里也需要特殊处理。当可为NULL的列被索引时，每个索引记录需要一个额外的字节。

通常把可为NULL的列改为NOT NULL带来的性能提升比较小，所以（调优时）没有必要首先在现有schema中查找并修改掉这种情况，除非确定这会导致问题。但是，如果计划在列上建索引，就应该尽量避免设计成可为NULL的列。

#### 1.1.4.2.Int/整数类型

存储整数，可以使用这几种整数类型:TINYINT，SMALLINT，MEDIUMINT，INT，BIGINT。分别使用8，16，24，32，64位存储空间，也就是1、2、3、4、8个字节。它们可以存储的值的范围请自行计算。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8ab773b79c2a4c4d949c26e608f5d802.png)

同时整数类型有可选的 UNSIGNED属性，表示不允许负值，这大致可以使正数的上限提高一倍。例如TINYINT UNSIGNED可以存储的范围是0255，而TINYINT的存储范围是-128127。

有符号和无符号类型使用相同的存储空间，并具有相同的性能，因此可以根据实际情况选择合适的类型。

另外integer和int存储及大小没有任何差别，只是为了业务上区分。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2731390a415e4cceabef107b1424d50f.png)

MySQL可以为整数类型指定宽度，例如INT(11)，对大多数应用这是没有意义的，它不会限制值的合法范围,只是规定了MySQL的一些交互工具（例如MySQL命令行客户端)用来显示字符的个数。对于存储和计算来说，INT(1)和INT(20)是相同的。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/15348d2ff9db487096e11179b5dbe8bf.png)

MySQL中没有long型，对应的只有bigint

#### 1.1.4.3.实数类型

实数是带有小数部分的数字。MySQL既支持精确类型的存储DECIMAL类型，也支持不精确类型存储FLOAT和 DOUBLE类型（浮点类型）。DECIMAL类型用于存储精确的小数，本质上MySQL是以字符串形式存放的。所以CPU不支持对DECIMAL的直接计算，只是在MySQL中自身实现了DECIMAL的高精度计算。相对而言，CPU直接支持原生浮点计算，所以浮点运算明显更快。

浮点类型在存储同样范围的值时，通常比DECIMAL使用更少的空间。FLOAT使用4个字节存储，DOUBLE占用8个字节，DECIMAL里面存储65个数字，DECIMAL对于列的空间消耗比较大，另外DOUBLE比 FLOAT有更高的精度和更大的范围。

**如何选择？**
在精度不敏感和需要快速运算的时候，选择FLOAT和 DOUBLE。

应该尽量只在对小数进行精确计算时才使用DECIMAL，例如存储财务或金融数据。

但在数据量比较大的而且要求精度时，可以考虑使用BIGINT代替DECIMAL，将需要存储的货币单位根据小数的位数乘以相应的倍数即可。假设要存储财务数据精确到万分之一分，则可以把所有金额乘以一百万,然后将结果存储在BIGINT里，这样可以同时避免浮点存储计算不精确和 DECIMAL精确计算代价高的问题。

#### 1.1.4.4.字符串类型

MysQL支持多种字符串类型，包括VARCHAR和CHAR类型、BLOB和TEXT类型、ENUM（枚举）和SET类型。

**VARCHAR和 CHAR是两种最主要的字符串类型。**

##### VARCHAR

VARCHAR类型用于存储可变长字符串，是最常见的字符串数据类型。它比定长类型更节省空间，因为它仅使用必要的空间（例如，越短的字符串使用越少的空间)。在内部实现上，既然是变长，VARCHAR需要使用1或2个额外字节记录字符串的长度，如果列的最大长度小于或等于255字节,则只使用1个字节表示,否则使用2个字节。

VARCHAR节省了存储空间，所以对性能也有帮助。但是，由于行是变长的，在UPDATE时新值比旧值长时，使行变得比原来更长，这就肯能导致需要做额外的工作。如果一个行占用的空间增长，并且在页内没有更多的空间可以存储，在这种情况下，MyISAM会将行拆成不同的片段存储，InnoDB则需要分裂页来使行可以放进页内。

##### CHAR

CHAR类型是定长的，MySQL总是根据定义的字符串长度分配足够的空间。当存储CHAR值时，MySQL会删除所有的末尾空格，CHAR值会根据需要采用空格进行填充以方便比较。

##### CHAR与VARCHAR如何选择？

在CHAR和VARCHAR的选择上，这些情况下使用VARCHAR是合适的：

字符串列的最大长度比平均长度大很多，列的更新很少；使用了像UTF-8这样复杂的字符集，每个字符都使用不同的字节数进行存储。

CHAR适合存储很短的字符串，或者所有值定长或都接近同一个长度。例如，CHAR非常适合存储密码的MD5值，因为这是一个定长的值。对于经常变更的数据，CHAR也比VARCHAR更好，因为定长的CHAR类型不容易产生碎片。

对于非常短的列，CHAR比VARCHAR在存储空间上也更有效率。例如用CHAR( 1)来存储只有Y和N的值，如果采用单字节字符集只需要一个字节，但是VARCHAR(1)却需要两个字节，因为还有一个记录长度的额外字节。

另外，使用VARCHAR(5)和VARCHAR(200)存储'hello'在磁盘空间上开销是一样的。我们随便选择一个就好？应该使用更短的列，为什么?

事实证明有很大的优势。更长的列会消耗更多的内存，因为MySQL通常会分配固定大小的内存块来保存内部值。尤其是使用内存临时表进行排序或操作时会特别糟糕。在利用磁盘临时表进行排序时也同样糟糕。

所以最好的策略是只分配真正需要的空间。

#### 1.1.4.5.BLOB和TEXT类型

BLOB和TEXT都是为存储很大的数据而设计的字符串数据类型，分别采用二进制和字符方式存储。

与其他类型不同，MySQL把每个BLOB和TEXT值当作一个独立的对象处理。存储引擎在存储时通常会做特殊处理。当BLOB和TEXT值太大时，InnoDB会使用专门的“外部”存储区域来进行存储，此时每个值在行内需要1~4个字节存储一个指针，然后在外部存储区域存储实际的值。

BLOB和TEXT家族之间仅有的不同是BLOB类型存储的是二进制数据，没有排序规则或字符集，而 TEXT类型有字符集和排序规则。

使用BLOB和TEXT要慎重：

(1） BLOB和 TEXT 值会引起一些性能问题，所以尽量避免使用BLOB和TEXT类型；

(2）一定要用，建议把BLOB或TEXT 列分离到单独的表中；

(3）在不必要的时候避免检索大型的 BLOB或TEXT值。例如，SELECT *查询就不是很好的想法，除非能够确定作为约束条件的WHERE子句只会找到所需要的数据行。否则，很可能毫无目的地在网络上传输大量的值。建议可以搜索索引列，决定需要的哪些数据行，然后从符合条件的数据行中检索BLOB或 TEXT值；

(4）还可以使用合成的(Synthetic)索引来提高大文本字段(BLOB或TEXT)的查询性能。简单来说，合成索引就是根据大文本字段的内容建立一个散列值，并把这个值存储在单独的数据列中，接下来就可以通过检索散列值找到数据行了。但是，要注意这种技术只能用于精确匹配的查询（散列值对于类似“&#x3c;”或“>=”等范围搜索操作符是没有用处的)。可以使用MD5函数生成散列值，也可以使用SHA1(或CRC32)，或者使用自己的应用程序逻辑来计算散列值。

#### 1.1.4.6.枚举类型

如果表中的字段的取值是固定几个字符串，可以使用枚举列代替常用的字符串类型。

枚举列可以把一些不重复的字符串存储成一个预定义的集合。MySQL在存储枚举时非常紧凑，会根据列表值的数量压缩到一个或者两个字节中，MySQL在内部会将每个值在列表中的位置保存为整数，这样的话可以让表的大小大为缩小。

具体枚举使用见官网地址：https://dev.mysql.com/doc/refman/5.7/en/enum.html

```
CREATE TABLE
enum_test(e ENUM(' fish', 'apple', 'dog') NOT NULL);

INSERT INTO
enum_test(e) VALUES(1),(2),(3);
```

但是要注意，

1）因为枚举列实际存储为整数，而不是字符串，所以不要使用数字作为ENUM枚举常量，这种双重性很容易导致混乱，例如ENUM( ' 1','2'，'3')。

2）枚举字段是按照内部存储的整数而不是定义的字符串进行排序的，所以尽量按照需要的顺序来定义枚举列。

#### 1.1.4.7.日期和时间类型

MySQL可以使用许多类型来保存日期和时间值，例如YEAR和 DATE以及DATETIME和TIMESTAMP。MySQL能存储的最小时间粒度为秒。

datetime 存储日期范围：1001年~9999年

timestamp 存储日期范围：1970年~2038年,并且跟时区有关系。

如果需要存储比秒更小粒度的日期和时间值怎么办？MySQL目前没有提供合适的数据类型，但是可以使用自己的存储格式：可以使用BIGINT类型存储微秒级别的时间截，或者使用DOUBLE存储秒之后的小数部分。

### 1.1.5.命名规范

1、可读性原则

数据库、表、字段的命名要遵守可读性原则，尽可能少使用或者不使用缩写。

对象的名字应该能够描述它所表示的对象。例如：表的名称应该能够体现表中存储的数据内容，最好是遵循“业务名称_表的作用”；对于存储过程存储过程应该能够体现存储过程的功能。库名与应用名称尽量一致。

表达是与否概念的字段，应该使用is_xxx的方式命名，数据类型是unsigned tinyint（1表示是，0表示否）。

2、表名、字段名必须使用小写字母或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。数据库字段名的修改代价很大，因为无法进行预发布，所以字段名称需要慎重考虑。
说明：MySQL在Windows下不区分大小写，但在Linux下默认是区分大小写。因此，数据库名、表名、字段名，都不允许出现任何大写字母，避免节外生枝。

3、表名不使用复数名词

4、数据库、表、字段的命名禁用保留字，如desc、range、match之类

6、主键索引名为pk_字段名；唯一索引名为uk_字段名；普通索引名则为idx_字段名。

**在面试过程中涉及到设计表的时，如果命名不规范，必定是一个很大的扣分项。**

### 1.1.6MySql中的索引

MySQL官方对索引的定义为：索引（Index）是帮助MySQL高效获取数据的数据结构。可以得到索引的本质： **索引是数据结构** 。InnoDB存储引擎支持以下几种常见的索引：B+树索引、全文索引、哈希索引，其中比较关键的是B+树索引

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/ab345e828dd043b7a89748587f993e6c.png)

**那为什么HashMap不适合做数据库索引？**

1、hash表只能匹配是否相等，不能实现范围查找；

2、当需要按照索引进行order by时，hash值没办法支持排序；

3、组合索引可以支持部分索引查询，如(a,b,c)的组合索引，查询中只用到了a和b也可以查询的，如果使用hash表，组合索引会将几个字段合并hash，没办法支持部分索引；

4、当数据量很大时，hash冲突的概率也会非常大。

### 1.1.7.B+Tree

B+树索引就是传统意义上的索引，这是目前关系型数据库系统中查找最常用和最为有效的索引。B+树索引的构造类似于二叉树，根据键值（Key Value）快速找到数据。注意B+树中的B不是代表二叉(binary)，而是代表平衡(balance)，因为B+树是从最早的平衡二叉树演化而来，但是B+树不是一个二叉树。

在讲二叉树之前，我们必须了解一下**二分查找：**

二分查找法（binary search） 也称为折半查找法，用来查找一组有序的记录数组中的某一记录。

在以下数组中找到数字48对应的下标

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/22adb01ec5c34eff8c432e3c872ec2d8.png)

通过3次二分查找 就找到了我们所要的数字，而顺序查找需8次。

对于上面10个数来说，顺序查找平均查找次数为（1+2+3+4+5+6+7+8+9+10)/10=5.5次。而二分查找法为(4+3+2+4+3+1+4+3+2+3)/10=2.9次。在最坏的情况下，顺序查找的次数为10，而二分查找的次数为4。

所以为了索引查找的高效性，我们引入了二叉查找树。

#### 1.1.7.1.二叉树

##### **1.1.7.1.1.树(Tree)**

N个结点构成的有限集合。

* 树中有一个称为”根(Root)”的特殊结点
* 其余结点可分为M个互不相交的树，称为原来结点的”子树”

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d193107a999b45c08ed3f27addbc7e29.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f52851a10e9b4bb09b97b7f79e7a2790.png)

##### **1.1.7.1.2.树与非树**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a7298460a83e445ebfa7a29f194de138.png)

##### **1.1.7.1.3.树的一些基本术语**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/1d1f4d7dd316443484765e3a01890d62.png)

##### **1.1.7.1.4.二叉树**

**度为2的树（也可称之为阶）：**（树的度：树中所有结点中最大的度。结点的度：结点的子树个数）

**子树有左右顺序之分：**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d2ec2025c1e447a893fc06a46f18e827.png)

##### 1.1.7.1.5.二叉查找(搜索)树

二叉查找树首先肯定是个二叉树，除此之外还符合以下几点：

* 左子树的所有的值小于根节点的值
* 右子树的所有的值大于或等于根节点的值
* 左、右子树满足以上两点

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6013b65d519f4c2c806dc02427e089b8.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b4a824b10110475abc41127e87f27fb3.png)

但是二叉查找树，如果设计不良，完全可以变成一颗极不平衡的二叉查找树：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8019f6e1498947fd8b8dab177ea546eb.png)

因此若想最大性能地构造一棵二叉查找树，需要这棵二叉查找树是平衡的，从而引出了新的定义——平衡二叉树，或称为AVL树。

##### 1.1.7.1.6.平衡二叉树（AVL-树）

它是一棵二叉排序树，它的左右两个子树的高度差（平衡因子）的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

目的：使得树的高度最低，因为树查找的效率决定于树的高度

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/580ef2d1f0d14ff1bda9b96a3c43f878.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/55e3e384d0c7479e8eca51cfc0f1a615.png)

平衡二叉树的查找性能是比较高的，但是维护一棵平衡二叉树的代价是非常大的。通常来说，需要1次或多次左旋和右旋来得到插入、更新和删除后树的平衡性。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/24448bd2d42648c69ee5d9a43d01ff4d.png)

具体树的旋转见：[算法数据结构体系学习班 马士兵教育官网 - IT职业领路人 (mashibing.com)](https://www.mashibing.com/course/339)

章节11-13

#### 1.1.7.2.B+树

B+ 树是从平衡二叉查找树演化而来（但B+树不是二叉树，而是一个多叉查找平衡树）。

下图就是一颗平衡二叉查找树

借助网页工具：[Data Structure Visualization (usfca.edu)](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/384705e33b054ff8861248fa5da21d45.png)

现在我们将其改造成 B+ 树

树的阶数表示一个节点最多能有多少个子节点。

每个叶子页（LeafPage）存储了实际的数据，如下图中有的叶子页就存放了3条数据记录，当然可以更多，叶子节点由小到大（有序）串联在一起，叶子页中的数据也是排好序的；

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/5e3015173b7e4305870044246ec0ffdc.png)

从AVL到B+树的变化可知，如果节点特别多的话，AVL树的高度远远高于B+树。

我们可以归纳出B+树的几个特征：

1、相同节点数量的情况下，B+树高度远低于平衡二叉树；

2、非叶子节点只保存索引信息和下一层节点的指针信息，不保存实际数据记录；

3、每个叶子页（LeafPage）存储了实际的数据，比如上图中每个叶子页就存放了3条数据记录，当然可以更多，叶子节点由小到大（有序）串联在一起，叶子页中的数据也是排好序的；

4、相邻的叶子节点之间用指针相连。

**注意：叶子节点中的数据在物理存储上完全可以是无序的，仅仅是在逻辑上有序（通过指针串在一起）。**

当然，一棵m阶的B+树完整定义如下：

* 每个节点最多可以有 m 个元素；

* 除了根节点外，每个节点最少有 (m/2) 个元素；

* 如果根节点不是叶节点，那么它最少有 2 个孩子节点；

* 所有的叶子节点都在同一层；

* 非叶子节点只存放关键字和指向下一个孩子节点的索引，记录只存放在叶子节点中；

* 一个有 k 个孩子节点的非叶子节点有(k-1) 个元素，按升序排列；

* 某个元素的左子树中的元素都比它小，右子树的元素都大于或等于它（二叉排序树的特征）；

* 相邻的叶子节点之间用指针相连。

  以上知识可以不了解，一般面试不会问到B+树的细节（B+树的插入、B+树的删除、B+树的旋转等等），除非面试岗位就是做数据库实现的。
  如果想详细了解，可以找《算法导论》这本书

  ![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/04f3f7da16024428af56e65fdadccce8.png)

  **面试问得比较多的可能是B树(也可以是B-树)、B*树，以及为什么选用B+树。**

  B树也B+树的差别是，B树的非叶子节点也需要存放数据，下图是B树

  ![image-20240129140902145](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129140902145.png)

  

  而B+树的话，数据只存在叶子节点上，同时相邻的叶子节点有链表的结构

  ![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a07fdc0a59cb4d6799a57f601a533135.png)

  同时要注意，MySQL中实现的B+树，叶子节点之间的链表是双向链表，这是一个细微的差别。

  另外B树的话，与B+树的差别就是在非叶子节点之间，也有相互的指针指向。

  ![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/e0c704ad343a41d59a6b9037a7e229a0.png)
  
  **那为什么MySQL不用B树而使用B+树呢？**
  
* 因为B数据每个节点都存储数据，每次查询的数据大小固定，就会造成每次查询返回的数据的条数变少，相同数据规模的情况下B树会增加io次数，而B+树，则数据量较小，一次可以返回多条记录，io次数较少

* 范围查询B+树明显优于B树

### 1.1.8.MySQL与B+树

为什么关系型数据库都选择了B+树，这个和磁盘的特性有着非常大的关系。

为了提高效率，要尽量减少磁盘I/O。为了达到这个目的，磁盘往往不是严格按需读取，而是每次都会预读，即使只需要一个字节，磁盘也会从这个位置开始，顺序向后读取一定长度的数据放入内存，这个称之为**预读。**

预读的长度一般为页（page）的整倍数。页是计算机管理存储器的逻辑块，硬件及操作系统往往将主存和磁盘存储区分割为连续的大小相等的块，每个存储块称为一页，页大小通常为4k。

按照磁盘的这种性质，如果是一个页存放一个B+树的节点，自然是可以存放很多的数据的，比如InnoDB里，默认定义的B+树的节点大小是16KB，这就是说，假如一个Key是8个字节，那么一个节点可以存放大约1000个Key，意味着B+树可以有1000个分叉。同时InnoDB每一次磁盘I/O，读取的都是 16KB的整数倍的数据。也就是说InnoDB在节点的读写上是可以充分利用磁盘顺序IO的高速读写特性。

同时按照B+树逻辑结构来说，在叶子节点一层，所有记录的主键按照从小到大的顺序排列，并且形成了一个双向链表。同一层的非叶子节点也互相串联，形成了一个双向链表。那么在实际读写的时候，很大的概率相邻的节点会放在相邻的页上，又可以充分利用磁盘顺序IO的高速读写特性。

所以我们对MySQL优化的一大方向就是 **尽可能的多让数据顺序读写，少让数据随机读写** 。

磁盘顺序读取的效率很高（不需要寻道时间，只需很少的旋转时间），一般来说，磁盘的顺序读的效率是随机读的40到400倍都有可能，顺序写是随机写的10到100倍。

![image-20240129140831511](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129140831511.png)







### 1.1.9.B+树的作用总结

* 在磁盘设备上，通过B+树可以有效的存储数据；
* 所有记录都存储在叶子节点上，非叶子(non-leaf)存储索引(keys)信息；而且记录按照索引列的值由小到大排好了序。
* B+树含有非常高的扇出（fanout），通常超过100，在查找一个记录时，可以有效的减少IO操作；

*扇出：是每个索引节点(Non-LeafPage)指向每个叶子节点(LeafPage)的指针；

**扇出数 = 索引节点(Non-LeafPage)可存储的最大关键字个数 + 1*



#### 算一算：

3层B+Tree能存储多少数据

![image-20240129142619239](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129142619239.png)







## 1.2.MySQL中的索引

InnoDB存储引擎支持以下几种常见的索引：B+树索引、全文索引、哈希索引，其中比较关键的是B+树索引

先看看官网。

搜 ：Indexes 

 14.6.2.1 Clustered and Secondary Indexes

https://dev.mysql.com/doc/refman/5.7/en/innodb-index-types.html

Each InnoDB table has a special  index called the clustered index that stores row data. Typically, the clustered index is synonymous with the primary key. To get the best performance from queries, inserts, and other database operations, it is important to understand how InnoDB uses the clustered index to optimize the common lookup and DML operations.

- When you define a PRIMARY KEY on a table, InnoDB uses it as the clustered index. A primary key should be defined for each table. If there is no logical  unique and non-null column or set of columns to use a the primary key, add an auto-increment column. Auto-increment column values are unique and are added automatically   as new rows are inserted.
- If you do not define a PRIMARY KEY for a table, InnoDB uses the first UNIQUE index with all key columns defined as NOT NULL as the clustered index.
- If a table has no PRIMARY KEY or suitable  UNIQUE index, InnoDB generates a hidden clustered     index named GEN_CLUST_INDEX on a synthetic column that contains row ID values. The rows are ordered by the row ID that InnoDB assigns. The row ID is a 6-byte field that increases monotonically as new rows are inserted. Thus, the rows ordered by the row ID are physically in order of insertion.

**How Secondary**  **Indexes Relate**  **to the** **Clustered Index** ****

Indexes other than the clustered index are known as secondary indexes. In InnoDB, each record in a secondary index contains the primary key columns for the row, as well as the columns specified for the secondary index . InnoDB uses this primary key value to search for the row in the clustered index.

If the primary key is long, the secondary indexes use more space, so it is advantageous to have a short primary key.

### 1.2.1.B+树索引

InnoDB中的索引自然也是按照B+树来组织的，前面我们说过B+树的叶子节点用来放数据的，但是放什么数据呢？索引自然是要放的，因为B+树的作用本来就是就是为了快速检索数据而提出的一种数据结构，不放索引放什么呢？但是数据库中的表，数据才是我们真正需要的数据，索引只是辅助数据，甚至于一个表可以没有自定义索引。InnoDB中的数据到底是如何组织的？

#### 1.2.1.1.聚集索引/聚簇索引

InnoDB中使用了聚集索引，就是将表的主键用来构造一棵B+树，并且将整张表的行记录数据存放在该B+树的叶子节点中。

也就是所谓的索引即数据，数据即索引。由于聚集索引是利用表的主键构建的，所以每张表只能拥有一个聚集索引。

聚集索引的叶子节点就是数据页。换句话说，数据页上存放的是完整的每行记录。因此聚集索引的一个优点就是：通过过聚集索引能获取完整的整行数据。另一个优点是：对于主键的排序查找和范围查找速度非常快。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/e280d5663e534e08a5e5afc2d5e6dbc3.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/23a70c89f27240ba82f8b288d30e364b.png)



如果我们没有定义主键呢？MySQL会使用唯一性索引，没有唯一性索引，MySQL也会创建一个隐含列RowID来做主键，然后用这个主键来建立聚集索引。

#### 1.2.1.2.辅助索引/二级索引

聚簇索引只能在搜索条件是主键值时才能发挥作用，因为B+树中的数据都是按照主键进行排序的。

如果我们想以别的列作为搜索条件怎么办？我们一般会建立多个索引，这些索引被称为辅助索引/二级索引。

（每建立一个索引，就有一颗B+树

对于辅助索引(Secondary Index，也称二级索引、非聚集索引)，叶子节点并不包含行记录的全部数据。叶子节点除了包含键值以外，每个叶子节点中的索引行中还包含了一个书签( bookmark)。该书签用来告诉InnoDB存储引擎哪里可以找到与索引相对应的行数据。因此InnoDB存储引擎的辅助索引的书签就是相应行数据的聚集索引键。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/70e7cdc503e14bc995ac06887c583128.png)

比如辅助索引index(node)，那么叶子节点中包含的数据就包括了(note和主键)。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/eb80ca41a76c44bdba04fed1f6ec42fc.png)

##### 二级索引如何查询完整数据

![image-20240129144422034](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129144422034.png)

#### 1.2.1.3.回表

辅助索引的存在并不影响数据在聚集索引中的组织，因此每张表上可以有多个辅助索引。当通过辅助索引来寻找数据时，InnoDB存储引擎会遍历辅助索引并通过叶级别的指针获得指向主键索引的主键，然后再通过主键索引（聚集索引）来找到一个完整的行记录。这个过程也被称为 **回表** 。也就是根据辅助索引的值查询一条完整的用户记录需要使用到2棵B+树----一次辅助索引，一次聚集索引。



为什么我们还需要一次回表操作呢?

直接把完整的用户记录放到辅助索引d的叶子节点不就好了么？

如果把完整的用户记录放到叶子节点是可以不用回表，但是太占地方了，相当于每建立一棵B+树都需要把所有的用户记录再都拷贝一遍，这就有点太浪费存储空间了。而且每次对数据的变化要在所有包含数据的索引中全部都修改一次，性能也非常低下。

很明显，回表的记录越少，性能提升就越高，需要回表的记录越多，使用二级索引的性能就越低，甚至让某些查询宁愿使用全表扫描也不使用二级索引。

那什么时候采用全表扫描的方式，什么时候使用采用二级索引 + 回表的方式去执行查询呢？

这个就是查询优化器做的工作，查询优化器会事先对表中的记录计算一些统计数据，然后再利用这些统计数据根据查询的条件来计算一下需要回表的记录数，需要回表的记录数越多，就越倾向于使用全表扫描，反之倾向于使用二级索引 + 回表的方式。



#### 1.2.1.4.联合索引/复合索引

前面我们对索引的描述，隐含了一个条件，那就是构建索引的字段只有一个，但实践工作中构建索引的完全可以是多个字段。所以，将表上的多个列组合起来进行索引我们称之为联合索引或者复合索引，比如index(a,b)就是将a,b两个列组合起来构成一个索引。

千万要注意一点，建立联合索引只会建立1棵B+树，多个列分别建立索引会分别以每个列则建立B+树，有几个列就有几个B+树，比如，index(note)、index(b)，就分别对note,b两个列各构建了一个索引。

而如果是index(note,b)在索引构建上，包含了两个意思：

1、先把各个记录按照note列进行排序。

2、在记录的note列相同的情况下，采用b列进行排序

从原理可知，为什么有最佳左前缀法则，就是这个道理

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6f15eac444b045179d65e601b588a03f.png)

#### 1.2.1.5.覆盖索引

既然多个列可以组合起来构建为联合索引，那么辅助索引自然也可以由多个列组成。

InnoDB存储引擎支持覆盖索引(covering index，或称索引覆盖)，即从辅助索引中就可以得到查询的记录，而不需要查询聚集索引中的记录(回表)。使用覆盖索引的一个好处是辅助索引不包含整行记录的所有信息，故其大小要远小于聚集索引，因此可以减少大量的IO操作。所以记住，覆盖索引并不是索引类型的一种。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/37985f1a9c0a4c2c8ba506d89bf14803.png)

**避免多次回表，用到覆盖索引（Covering index ）**

**回表：**先定位主键值，再定位行记录，遍历两次树

**覆盖索引：如果select 查的所有列 （有order by等也须在），已经包含了用到的索引中。那就不要用到回表了。**

常见的方法是：将被查询的字段，建立到联合索引里去

覆盖索引的标志：Extra 里面打印 **using index** 

explain SELECT `name` ,`phone` FROM user WHERE name='天明';

explain SELECT `name` FROM user WHERE phone = '18588887668' AND name= '诸葛';

explain SELECT `name` FROM user WHERE phone= '18588887668';

explain SELECT * FROM user WHERE `name` ='天明';

重点在3：

查的条件 phone 没有，但是要得到的是字段 name，不满足刚说上一个最左匹配原则，理论上没有用到索引，那肯定更谈不上什么覆盖索引了。

但是结果却。。。。出乎意料。为啥呢？还是优化器的作用.他怎么去优化的呢？虽然检索的时候违反了最左匹配原则用不到索引，但是发现你刚好查的就是索引的列 name。 所以他直接就给你优化成通过这个name去过滤先。）

 如果在前三个已经优化了覆盖索引得语句  后面加上 ORDER BY sex 呢？



### 1.2.2.哈希索引

InnoDB存储引擎除了我们前面所说的各种索引，还有一种adaptive hash Index自适应哈希索引，我们知道B+树的查找次数,取决于B+树的高度,在生产环境中,B+树的高度一般为3、4层,故需要3、4次的IO查询。

所以在InnoDB存储引擎内部自己去监控索引表，如果监控到某个索引经常用，那么就认为是热数据，然后内部自己创建一个hash索引，称之为自适应哈希索引( Adaptive Hash Index,AHI)，创建以后，如果下次又查询到这个索引，那么直接通过hash算法推导出记录的地址，直接一次就能查到数据，比重复去B+tree索引中查询三四次节点的效率高了不少。

InnoDB存储引擎使用的哈希函数采用除法散列方式，其冲突机制采用链表方式。注意，对于自适应哈希索引仅是**数据库自身创建并使用**的，我们并不能对其进行干预。

 频繁通过二级索引查询（连续3次等值查询==号>=等不行）成为热点数据会建立hash index 带来速度的提升

**show engine innodb status**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/189e15fdc29041cfa5a55c162f607734.png)

哈希索引只能用来搜索等值的查询,如 SELECT* FROM table WHERE index co=xxx。而对于其他查找类型,如范围查找,是不能使用哈希索引的,

因此这里出现了non-hash searches/s的情况。通过 hash searches: non- hash searches可以大概了解使用哈希索引后的效率。

**innodb_adaptive_hash_index**来考虑是禁用或启动此特性,默认AHI为开启状态。

**示意图：**



### 1.2.3.全文索引

什么是全文检索（Full-Text Search）？它是将存储于数据库中的整本书或整篇文章中的任意内容信息查找出来的技术。它可以根据需要获得全文中有关章、节、段、句、词等信息，也可以进行各种统计和分析。我们比较熟知的Elasticsearch、Solr等就是全文检索引擎，底层都是基于Apache Lucene的。

举个例子，现在我们要保存唐宋诗词，数据库中我们们会怎么设计？诗词表我们可能的设计如下：

| 朝代 | 作者   | 诗词年代 | 标题   | 诗词全文                                                     |
| ---- | ------ | -------- | ------ | ------------------------------------------------------------ |
| 唐   | 李白   |          | 静夜思 | 床前明月光，疑是地上霜。 举头望明月，低头思故乡。            |
| 宋   | 李清照 |          | 如梦令 | 常记溪亭日暮，沉醉不知归路，兴尽晚回舟，误入藕花深处。争渡，争渡，惊起一滩鸥鹭。 |
| ….   | ….     | …        | ….     | …….                                                          |

要根据朝代或者作者寻找诗，都很简单，比如“select 诗词全文 from 诗词表 where作者=‘李白’”，如果数据很多，查询速度很慢，怎么办？我们可以在对应的查询字段上建立索引加速查询。

但是如果我们现在有个需求：要求找到包含“望”字的诗词怎么办？用

“select 诗词全文 from 诗词表 where诗词全文 like‘%望%’”，这个意味着要扫描库中的诗词全文字段，逐条比对，找出所有包含关键词“望”字的记录，。基本上，数据库中一般的SQL优化手段都是用不上的。数量少，大概性能还能接受，如果数据量稍微大点，就完全无法接受了，更何况在互联网这种海量数据的情况下呢？怎么解决这个问题呢，用倒排索引。

倒排索引就是，将文档中包含的关键字全部提取处理，然后再将关键字和文档之间的对应关系保存起来，最后再对关键字本身做索引排序。用户在检索某一个关键字是，先对关键字的索引进行查找，再通过关键字与文档的对应关系找到所在文档。

于是我们可以这么保存

| 序号 | 关键字 | 蜀道难 | 静夜思 | 春台望 | 鹤冲天 |
| ---- | ------ | ------ | ------ | ------ | ------ |
| 1    | 望     | 有     | 有     | 有     | 有     |
|      |        |        |        |        |        |

如果查哪个诗词中包含上，怎么办，上述的表格可以继续填入新的记录

| 序号 | 关键字 | 蜀道难 | 静夜思 | 春台望 | 鹤冲天 |
| ---- | ------ | ------ | ------ | ------ | ------ |
| 1    | 望     | 有     | 有     | 有     | 有     |
| 2    | 上     | 有     |        |        | 有     |

从InnoDB 1.2.x版本开始，InnoDB存储引擎开始支持全文检索，对应的MySQL版本是5.6.x系列。不过MySQL从设计之初就是关系型数据库，存储引擎虽然支持全文检索，整体架构上对全文检索支持并不好而且限制很多，比如每张表只能有一个全文检索的索引，不支持没有单词界定符

( delimiter）的语言，如中文、日语、韩语等。

所以MySQL中的全文索引功能比较弱鸡，了解即可。

### 1.2.4.索引在查询中的使用

索引在查询中的作用到底是什么？在我们的查询中发挥着什么样的作用呢？

请记住：

1、 一个索引就是一个B+树，索引让我们的查询可以快速定位和扫描到我们需要的数据记录上，加快查询的速度 。

2、一个select查询语句在执行过程中一般最多能使用一个二级索引，即使在where条件中用了多个二级索引。

### 1.2.4.高性能的索引创建策略

正确地创建和使用索引是实现高性能查询的基础。前面我们已经了解了索引相关的数据结构，各种类型的索引及其对应的优缺点。现在我们一起来看看如何真正地发挥这些索引的优势。

#### 1.2.4.1.索引列的类型尽量小

我们在定义表结构的时候要显式的指定列的类型，以整数类型为例，有TTNYINT、NEDUMNT、INT、BIGTNT这么几种，它们占用的存储空间依次递增，我们这里所说的类型大小指的就是该类型表示的数据范围的大小。能表示的整数范围当然也是依次递增，如果我们想要对某个整数列建立索引的话，在表示的整数范围允许的情况下，尽量让索引列使用较小的类型，比如我们能使用INT就不要使用BIGINT，能使用NEDIUMINT就不要使用INT，这是因为数据类型越小，在查询时进行的比较操作越快（CPU层次)数据类型越小，索引占用的存储空间就越少，在一个数据页内就可以放下更多的记录，从而减少磁盘/0带来的性能损耗，也就意味着可以把更多的数据页缓存在内存中，从而加快读写效率。

这个建议对于表的主键来说更加适用，因为不仅是聚簇索引中会存储主键值，其他所有的二级索引的节点处都会存储一份记录的主键值，如果主键适用更小的数据类型，也就意味着节省更多的存储空间和更高效的I/0。

#### 1.2.4.2.索引的选择性

创建索引应该选择选择性/离散性高的列。索引的选择性/离散性是指，不重复的索引值（也称为基数，cardinality)和数据表的记录总数（N)的比值，范围从1/N到1之间。索引的选择性越高则查询效率越高，因为选择性高的索引可以让MySQL在查找时过滤掉更多的行。唯一索引的选择性是1，这是最好的索引选择性，性能也是最好的。

很差的索引选择性就是列中的数据重复度很高，比如性别字段，不考虑政治正确的情况下，只有两者可能，男或女。那么我们在查询时，即使使用这个索引，从概率的角度来说，依然可能查出一半的数据出来。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f3908cc7cedc4344aa928936bd86c70f.png)

哪列做为索引字段最好？当然是姓名字段，因为里面的数据没有任何重复，性别字段是最不适合做索引的，因为数据的重复度非常高。

怎么算索引的选择性/离散性？比如person这个表：

SELECT count(DISTINCT name)/count(*) FROM person;
SELECT count(DISTINCT sex)/count(*) FROM person;
SELECT count(DISTINCT age)/count(*) FROM person;
SELECT count(DISTINCT  area)/count(*) FROM person;

#### 1.2.4.3.前缀索引

针对blob、text、很长的varchar字段，mysql不支持索引他们的全部长度，需建立前缀索引。

语法：Alter table tableName add key/index (column(X))

**缺点：**前缀索引是一种能使索引更小、更快的有效办法，但另一方面也有其缺点MySQL无法使用前缀索引做ORDER BY和GROUP BY，也无法使用前缀索引做覆盖扫描。

有时候后缀索引 (suffix
index)也有用途（例如，找到某个域名的所有电子邮件地址)。MySQL原生并不支持反向索引，但是可以把字符串反转后存储，并基于此建立前缀索引。可以通过触发器或者应用程序自行处理来维护索引。

案例：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/bf3a2bf88d56492a958086486e7d57c7.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/1a662f14ed1948f3a2b5dbdb46690091.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/5d5c5368694b409f99f0d1a8a238f29a.png)

首先找到最常见的值的列表：

```
SELECT COUNT(DISTINCT LEFT(order_note,3))/COUNT(*) AS sel3,
COUNT(DISTINCT LEFT(order_note,4))/COUNT(*)AS sel4,
COUNT(DISTINCT LEFT(order_note,5))/COUNT(*) AS sel5,
COUNT(DISTINCT LEFT(order_note, 6))/COUNT(*) As sel6,
COUNT(DISTINCT LEFT(order_note, 7))/COUNT(*) As sel7,
COUNT(DISTINCT LEFT(order_note, 8))/COUNT(*) As sel8,
COUNT(DISTINCT LEFT(order_note, 9))/COUNT(*) As sel9,
COUNT(DISTINCT LEFT(order_note, 10))/COUNT(*) As sel10,
COUNT(DISTINCT LEFT(order_note, 11))/COUNT(*) As sel11,
COUNT(DISTINCT LEFT(order_note, 12))/COUNT(*) As sel12,
COUNT(DISTINCT LEFT(order_note, 13))/COUNT(*) As sel13,
COUNT(DISTINCT LEFT(order_note, 14))/COUNT(*) As sel14,
COUNT(DISTINCT LEFT(order_note, 15))/COUNT(*) As sel15,
COUNT(DISTINCT order_note)/COUNT(*) As total
FROM order_exp;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/ffbfccc4e0fa4ff39903505adb5f1a4e.png)

可以看见，从第10个开始选择性的增加值很高，随着前缀字符的越来越多，选择度也在不断上升，但是增长到第15时，已经和第14没太大差别了，选择性提升的幅度已经很小了，都非常接近整个列的选择性了。

那么针对这个字段做前缀索引的话，从第13到第15都是不错的选择

在上面的示例中，已经找到了合适的前缀长度，如何创建前缀索引:

**ALTER TABLE order_exp ADD KEY (order_note(14));**

建立前缀索引后查询语句并不需要更改：

select * from order_exp where order_note = 'xxxx' ;

前缀索引是一种能使索引更小、更快的有效办法，但另一方面也有其缺点MySQL无法使用前缀索引做ORDER BY和GROUP BY，也无法使用前缀索引做覆盖扫描。

有时候后缀索引 (suffix index)也有用途（例如，找到某个域名的所有电子邮件地址)。MySQL原生并不支持反向索引，但是可以把字符串反转后存储，并基于此建立前缀索引。可以通过触发器或者应用程序自行处理来维护索引。

#### 1.2.4.4.只为用于搜索、排序或分组的列创建索引

也就是说，只为出现在WHERE 子句中的列、连接子句中的连接列创建索引，而出现在查询列表中的列一般就没必要建立索引了，除非是需要使用覆盖索引；又或者为出现在ORDER BY或GROUP BY子句中的列创建索引，这句话什么意思呢？比如：

**搜索**

select order_note from .... and ....

只为 条件中的列建立索引即可

**排序**

SELECT * FROM order_exp ORDER BY insert_time, order_status,expire_time;

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/30ba8ead865741a1bad33637c189fefa.png)

查询的结果集需要先按照insert_time值排序，如果记录的insert_time值相同，则需要按照order_status来排序，如果order_status的值相同，则需要按照expire_time排序。回顾一下联合索引的存储结构，u_idx_day_status索引本身就是按照上述规则排好序的，所以直接从索引中提取数据，然后进行回表操作取出该索引中不包含的列就好了。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a97a0c6253ef4030bf18088eee4cc974.png)

#### 1.2.4.5.多列索引

很多人对多列索引的理解都不够。一个常见的错误就是，为每个列创建独立的索引，或者按照错误的顺序创建多列索引。

我们遇到的最容易引起困惑的问题就是索引列的顺序。正确的顺序依赖于使用该索引的查询，并且同时需要考虑如何更好地满足排序和分组的需要。反复强调过，在一个多列B-Tree索引中，索引列的顺序意味着索引首先按照最左列进行排序，其次是第二列，等等。所以，索引可以按照升序或者降序进行扫描，以满足精确符合列顺序的ORDER BY、GROUP BY和DISTINCT等子句的查询需求。

所以多列索引的列顺序至关重要。对于如何选择索引的列顺序有一个经验法则：将选择性最高的列放到索引最前列。当不需要考虑排序和分组时，将选择性最高的列放在前面通常是很好的。这时候索引的作用只是用于优化WHERE条件的查找。在这种情况下，这样设计的索引确实能够最快地过滤出需要的行，对于在WHERE子句中只使用了索引部分前缀列的查询来说选择性也更高。

然而，性能不只是依赖于索引列的选择性，也和查询条件的有关。可能需要根据那些运行频率最高的查询来调整索引列的顺序，比如排序和分组，让这种情况下索引的选择性最高。

同时，在优化性能的时候，可能需要使用相同的列但顺序不同的索引来满足不同类型的查询需求。

#### 1.2.4.6.三星索引

**三星索引概念**

对于一个查询而言，一个三星索引，可能是其最好的索引。

满足的条件如下：

* 索引将相关的记录放到一起则获得一星    （比重27%）
* 如果索引中的数据顺序和查找中的排列顺序一致则获得二星（排序星） （比重27%）
* 如果索引中的列包含了查询中需要的全部列则获得三星（宽索引星） （比重50%）

这三颗星，哪颗最重要？第三颗星。因为将一个列排除在索引之外可能会导致很多磁盘随机读（回表操作）。第一和第二颗星重要性差不多，可以理解为第三颗星比重是50%，第一颗星为27%，第二颗星为23%，所以在大部分的情况下，会先考虑第一颗星，但会根据业务情况调整这两颗星的优先度。

**一星：**

一星的意思就是：如果一个查询相关的索引行是相邻的或者至少相距足够靠近的话，必须扫描的索引片宽度就会缩至最短，也就是说，让索引片尽量变窄，也就是我们所说的索引的扫描范围越小越好。

**二星（排序星）** ：

在满足一星的情况下，当查询需要排序，group by、 order by，如果查询所需的顺序与索引是一致的（索引本身是有序的），是不是就可以不用再另外排序了，一般来说排序可是影响性能的关键因素。

**三星（宽索引星）** ：

在满足了二星的情况下，如果索引中所包含了这个查询所需的所有列（包括 where 子句和 select 子句中所需的列，也就是覆盖索引），这样一来，查询就不再需要回表了，减少了查询的步骤和IO请求次数，性能几乎可以提升一倍。

#### 1.2.4.6.设计三星索引实战

**现在有表，SQL如下**

```sql
CREATE TABLE customer (
	cno INT,
	lname VARCHAR (10),
	fname VARCHAR (10),
	sex INT,
	weight INT,
	city VARCHAR (10)
);

CREATE INDEX idx_cust ON customer (city, lname, fname, cno);
```

对于下面的SQL而言，这是个三星索引

```sql
select cno,fname from customer where lname=’xx’ and city =’yy’ order by fname;
```

来评估下：

第一颗星：所有等值谓词的列，是组合索引的开头的列，可以把索引片缩得很窄，符合。

根据之前讲过的联合索引，我们是知道条件已经把搜索范围搜到很窄了

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f0f05f49cd024c538bf8afa800a71e9b.png)

第二颗星：order by的fname字段在组合索引中且是索引自动排序好的，符合。

第三颗星：select中的cno字段、fname字段在组合索引中存在，符合。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/72ceb2eda7724db58d944048dca8a590.png)

**现在有表，SQL如下：**

```sql
CREATE TABLE `test` (
	`id` INT (11) NOT NULL AUTO_INCREMENT,
	`user_name` VARCHAR (100) DEFAULT NULL,
	`sex` INT (11) DEFAULT NULL,
	`age` INT (11) DEFAULT NULL,
	`c_date` datetime DEFAULT NULL,
	PRIMARY KEY (`id`),

) ENGINE = INNODB AUTO_INCREMENT = 12 DEFAULT CHARSET = utf8;
```

SQL语句如下：

```sql
select user_name,sex,age from test where user_name like 'test%'  and sex =1 ORDER BY age
```

**如果我们建立索引(user_name,sex,age)：**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/35954180a81049c68d1e45275b71b19e.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/02edf4066ee5456fbd58b658af6f5904.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a6fe8c913c6d4f1ba3b41f7922ecaebb.png)

第三颗星，满足

第一颗星，满足

第二颗星，不满足，user_name 采用了范围匹配，sex 是过滤列，此时age 列无法保证有序的。

上述我们看到，此时索引(user_name,sex,age)并不能满足三星索引中的第二颗星（排序）。

**于是我们改改，建立索引(sex, age，user_name)：**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/85c6ee6f25934d5eadef7cca32ff278d.png)

第一颗星，不满足，只可以匹配到sex，sex选择性很差，意味着是一个宽索引片(同时因为age也会导致排序选择的碎片问题)

第二颗星，满足，等值sex 的情况下，age是有序的，

第三颗星，满足，select查询的列都在索引列中，

对于索引(sex,age，user_name)我们可以看到，此时无法满足第一颗星，窄索引片的需求。

以上2个索引，都是无法同时满足三星索引设计中的三个需求的，我们只能尽力满足2个。而在多数情况下，能够满足2颗星，已经能缩小很大的查询范围了，具体最终要保留那一颗星（排序星 or 窄索引片星），这个就需要看查询者自己的着重点了，无法给出标准答案。1.3.MySQL性能调优



## 1.3.MySQL调优

### 1.3.1.MySQL调优金字塔

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/098cb1ed7e96428eaea382ab6b69848d.png)

很明显从图上可以看出，越往上走，难度越来越高，收益却是越来越小的。

对于**架构调优**，在系统设计时首先需要充分考虑业务的实际情况，是否可以把不适合数据库做的事情放到数据仓库、搜索引擎或者缓存中去做；然后考虑写的并发量有多大，是否需要采用分布式；最后考虑读的压力是否很大，是否需要读写分离。对于核心应用或者金融类的应用，需要额外考虑数据安全因素，数据是否不允许丢失。所以在进行优化时，首先需要关注和优化的应该是架构，如果架构不合理，即使是DBA能做的事情其实是也是比较有限的。

对于**MySQL调优**，需要确认业务表结构设计是否合理，SQL语句优化是否足够，该添加的索引是否都添加了，是否可以剔除多余的索引等等

比如**硬件和OS调优**，需要对硬件和OS有着非常深刻的了解，仅仅就磁盘一项来说，一般非DBA能想到的调整就是SSD盘比用机械硬盘更好。DBA级别考虑的至少包括了，使用什么样的磁盘阵列（RAID）级别、是否可以分散磁盘IO、是否使用裸设备存放数据，使用哪种文件系统（目前比较推荐的是XFS），操作系统的磁盘调度算法选择，是否需要调整操作系统文件管理方面比如atime属性等等。

所以本章我们重点关注MySQL方面的调优，特别是索引。SQL/索引调优要求对业务和数据流非常清楚。在阿里巴巴内部，有三分之二的DBA是业务DBA，从业务需求讨论到表结构审核、SQL语句审核、上线、索引更新、版本迭代升级，甚至哪些数据应该放到非关系型数据库中，哪些数据放到数据仓库、搜索引擎或者缓存中，都需要这些DBA跟踪和复审。他们甚至可以称为数据架构师（Data Architecher）。

### 1.3.2.查询性能优化

前面的章节我们知道如何设计最优的库表结构、如何建立最好的索引，这些对于高性能来说是必不可少的。但这些还不够—还需要合理的设计查询。如果查询写得很糟糕，即使库表结构再合理、索引再合适，也无法实现高性能。

#### 1.3.2.1.什么是慢查询

慢查询日志，顾名思义，就是查询花费大量时间的日志，是指mysql记录所有执行超过long_query_time参数设定的时间阈值的SQL语句的日志。该日志能为SQL语句的优化带来很好的帮助。默认情况下，慢查询日志是关闭的，要使用慢查询日志功能，首先要开启慢查询日志功能。如何开启，我们稍后再说。

##### **1.3.2.1.1慢查询基础-优化数据访问**

查询性能低下最基本的原因是访问的数据太多。大部分性能低下的查询都可以通过减少访问的数据量的方式进行优化。对于低效的查询，一般通过下面两个步骤来分析总是很有效:

1．确认应用程序是否在检索大量超过需要的数据。这通常意味着访问了太多的行，但有时候也可能是访问了太多的列。

2．确认MySQL服务器层是否在分析大量超过需要的数据行。

##### **1.3.2.1.2请求了不需要的数据？**

有些查询会请求超过实际需要的数据，然后这些多余的数据会被应用程序丢弃。这会给MySQL服务器带来额外的负担，并增加网络开销，另外也会消耗应用服务器的CPU和内存资源。比如:

**查询不需要的记录**

一个常见的错误是常常会误以为MySQL会只返回需要的数据，实际上MySQL却是先返回全部结果集再进行计算。我们经常会看到一些了解其他数据库系统的人会设计出这类应用程序。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/c42215b7f5c442869027906f5aa80f4e.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8915ae332c7b4dbea0fa3c591e902197.png)

以上SQL你认为MySQL会执行查询，并只返回他们需要的20条数据，然后停止查询。实际情况是MySQL会查询出全部的结果集，客户端的应用程序会接收全部的结果集数据，然后抛弃其中大部分数据。

**总是取出全部列**

每次看到SELECT*的时候都需要用怀疑的眼光审视，是不是真的需要返回全部的列？很可能不是必需的。取出全部列，会让优化器无法完成索引覆盖扫描这类优化,还会为服务器带来额外的I/O、内存和CPU的消耗。因此，一些DBA是严格禁止SELECT *的写法的，这样做有时候还能避免某些列被修改带来的问题。

尤其是使用二级索引，使用*的方式会导致回表，导致性能低下。

什么时候可以使用SELECT*如果应用程序使用了某种缓存机制，或者有其他考虑，获取超过需要的数据也可能有其好处，但不要忘记这样做的代价是什么。获取并缓存所有的列的查询，相比多个独立的只获取部分列的查询可能就更有好处。

**重复查询相同的数据**

不断地重复执行相同的查询，然后每次都返回完全相同的数据。比较好的方案是，当初次查询的时候将这个数据缓存起来，需要的时候从缓存中取出，这样性能显然会更好。

##### 1.3.2.1.3.是否在扫描额外的记录

在确定查询只返回需要的数据以后，接下来应该看看查询为了返回结果是否扫描了过多的数据。对于MySQL，最简单的衡量查询开销的三个指标如下:

**响应时间、扫描的行数、返回的行数**

没有哪个指标能够完美地衡量查询的开销，但它们大致反映了MySQL在内部执行查询时需要访问多少数据，并可以大概推算出查询运行的时间。这三个指标都会记录到MySQL的慢日志中，所以检查慢日志记录是找出扫描行数过多的查询的好办法。

**响应时间**

响应时间是两个部分之和:服务时间和排队时间。

服务时间是指数据库处理这个查询真正花了多长时间。

排队时间是指服务器因为等待某些资源而没有真正执行查询的时间—-可能是等I/O操作完成，也可能是等待行锁，等等。

**扫描的行数和返回的行数**

分析查询时，查看该查询扫描的行数是非常有帮助的。这在一定程度上能够说明该查询找到需要的数据的效率高不高。

理想情况下扫描的行数和返回的行数应该是相同的。但实际情况中这种“美事”并不多。例如在做一个关联查询时，服务器必须要扫描多行才能生成结果集中的一行。扫描的行数对返回的行数的比率通常很小，一般在1:1和10:1之间，不过有时候这个值也可能非常非常大。

**扫描的行数和访问类型**

在评估查询开销的时候，需要考虑一下从表中找到某一行数据的成本。MySQL有好几种访问方式可以查找并返回一行结果。有些访问方式可能需要扫描很多行才能返回一行结果，也有些访问方式可能无须扫描就能返回结果。

在EXPLAIN语句中的type列反应了访问类型。访问类型有很多种，从全表扫描到索引扫描、范围扫描、唯一索引查询、常数引用等。这里列的这些，速度是从慢到快，扫描的行数也是从小到大。你不需要记住这些访问类型，但需要明白扫描表、扫描索引、范围访问和单值访问的概念。

如果查询没有办法找到合适的访问类型，那么解决的最好办法通常就是增加一个合适的索引，为什么索引对于查询优化如此重要了。索引让 MySQL以最高效、扫描行数最少的方式找到需要的记录。

一般 MySQL能够使用如下三种方式应用WHERE条件，从好到坏依次为:

1、在索引中使用WHERE条件来过滤不匹配的记录。这是在存储引擎层完成的。

select .... from where a>100 and a &#x3c;200

2、使用覆盖索引扫描来返回记录，直接从索引中过滤不需要的记录并返回命中的结果。这是在 MySQL服务器层完成的，但无须再回表查询记录。

3、从数据表中返回数据(存在回表)，然后过滤不满足条件的记录。这在 MySQL服务器层完成，MySQL需要先从数据表读出记录然后过滤。

好的索引可以让查询使用合适的访问类型，尽可能地只扫描需要的数据行。

**如果发现查询需要扫描大量的数据但只返回少数的行，那么通常可以尝试下面的技巧去优化它:**

1、使用索引覆盖扫描，把所有需要用的列都放到索引中，这样存储引擎无须回表获取对应行就可以返回结果了

2、改变库表结构。例如使用单独的汇总表。

3、重写这个复杂的查询，让MySQL优化器能够以更优化的方式执行这个查询。

### 1.3.3.慢查询

#### 1.3.3.1慢查询配置

我们已经知道慢查询日志可以帮助定位可能存在问题的SQL语句，从而进行SQL语句层面的优化。但是默认值为关闭的，需要我们手动开启。

```
show VARIABLES like 'slow_query_log';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f72a83180181494fa68d4f014375127b.png)

```
set GLOBAL slow_query_log=1;
```

开启1，关闭0

但是多慢算慢？MySQL中可以设定一个阈值，将运行时间超过该值的所有SQL语句都记录到慢查询日志中。long_query_time参数就是这个阈值。默认值为10，代表10秒。

```
show VARIABLES like '%long_query_time%';
```

当然也可以设置

```
set global long_query_time=0;
```

默认10秒，这里为了演示方便设置为0

同时对于运行的SQL语句没有使用索引，则MySQL数据库也可以将这条SQL语句记录到慢查询日志文件，控制参数是：

```
show VARIABLES like '%log_queries_not_using_indexes%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/19a8d15f0d724fae93946b5bd4f63cc3.png)

开启1，关闭0（默认）

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/67a74308e0524b459cb30cfa66bdba40.png)

```
show VARIABLES like '%slow_query_log_file%';
```

**MySQL自带了**

#### 慢查询解析工具

bin 目录下面有一个 mysqldumpslow 怎么用呢 ？（先前说的 window需要perl语言环境，所以用虚拟机）



连虚拟机  

whereis mysqldumpslow

/usr/bin/mysqldumpslow /usr/share/man/man1/mysqldumpslow.1.gz

放在这个bin下面，你可以在任何地方使用。通过 mysqldumpslow --help 怎么用呢？

查看帮助 可以看到后面可以加很多的参数做相应的统计（支线：具体可以自行翻译 或 API下,如有人问可简单翻译）

Usage/用法/: 

--verbose verbose /冗长的/ 

default al: average/平均/ lock time ar: average /平均/ rows sent at

 -r reverse /颠倒；反转 /the sort order (largest last instead of first) 

-t NUM 前几条

-n NUM abstract numbers with at least n digits within names 

-g PATTERN /模式/ grep /UNIX工具程序；可做文件内的字符串查找/: 匹配的正则表达式

-s top排序的规则 ：锁 查询的时间等 al平均锁定时间 ar平均返回记录时间  at平均查询时间（默认） c计数 l锁定时间 r返回记录 t查询时间 

 

当然通过一个例子来实验，比如我要统计查询最慢的十条select 语句 怎么写呢？



mysqldumpslow -s t -t 10 -g 'select' /var/lib/mysql/slow-query.log    (虚拟机1)

这样马上就给你统计出来 慢查询的一个排序了，额，接下来你就可以看这个sql是谁的，今晚抓起他加班就对了。

当然为了效果 你可以来一个 SELECT SLEEP(10) 之类的去故意制造10s等待。



##### 小结

l  slow_query_log 启动停止慢查询日志

l  slow_query_log_file 指定慢查询日志得存储路径及文件（默认和数据文件放一起）

l  long_query_time 指定记录慢查询日志SQL执行时间得伐值（单位：秒，默认10秒）

l  log_queries_not_using_indexes  是否记录未使用索引的SQL

l  log_output 日志存放的地方可以是[TABLE][FILE][FILE,TABLE]

### 1.3.4.Explain执行计划

#### 1.3.4.1.什么是执行计划

有了慢查询语句后，就要对语句进行分析。一条查询语句在经过MySQL查询优化器的各种基于成本和规则的优化会后生成一个所谓的执行计划，这个执行计划展示了接下来具体执行查询的方式，比如多表连接的顺序是什么，对于每个表采用什么访问方法来具体执行查询等等。EXPLAIN语句来帮助我们查看某个查询语句的具体执行计划，我们需要搞懂EPLATNEXPLAIN的各个输出项都是干嘛使的，从而可以有针对性的提升我们查询语句的性能。

通过使用EXPLAIN关键字可以模拟优化器执行SQL查询语句，从而知道MySQL是如何处理你的SQL语句的。分析查询语句或是表结构的性能瓶颈，总的来说通过EXPLAIN我们可以：

l  表的读取顺序

l  数据读取操作的操作类型

l  哪些索引可以使用

l  哪些索引被实际使用

l  表之间的引用

l  每张表有多少行被优化器查询

#### 1.3.4.2.执行计划的语法

执行计划的语法其实非常简单： 在SQL查询的前面加上EXPLAIN关键字就行。比如：EXPLAIN select * from table1

重点的就是EXPLAIN后面你要分析的SQL语句

除了以SELECT开头的查询语句，其余的DELETE、INSERT、REPLACE以及UPOATE语句前边都可以加上EXPLAIN，用来查看这些语句的执行计划，不过我们这里对SELECT语句更感兴趣，所以后边只会以SELECT语句为例来描述EsxPLAIN语句的用法。

#### 1.3.4.3.执行计划详解

为了让大家先有一个感性的认识，我们把EXPLAIN语句输出的各个列的作用先大致罗列一下:

**explain
select * from order_exp;**

**id** **： ****在一个大的查询语句中每个SELECT****关键字都对应一个唯一的id**

**select_type** **： SELECT****关键字对应的那个查询的类型**

**table** **：表名**

**partitions** **：匹配的分区信息**

**type** **：针对单表的访问方法**

**possible_keys** **：可能用到的索引**

**key** **：实际上使用的索引**

**key_len** **：实际使用到的索引长度**

**ref** **：当使用索引列等值查询时，与索引列进行等值匹配的对象信息**

**rows** **：预估的需要读取的记录条数**

**filtered** **：某个表经过搜索条件过滤后剩余记录条数的百分比**

**Extra** **：—些额外的信息**

##### id

我们知道我们写的查询语句一般都以SELECT关键字开头，比较简单的查询语句里只有一个SELECT关键字，

稍微复杂一点的连接查询中也只有一个SELECT关键字，比如:

```sql
SELECT *FROM s1
INNER J0IN s2 ON s1.id = s2.id
WHERE s1.order_status = 0 ;
```

但是下边两种情况下在一条查询语句中会出现多个SELECT关键字:

1、查询中包含子查询的情况

比如下边这个查询语句中就包含2个SELECT关键字:

```
SELECT* FROM s1 WHERE id IN ( SELECT * FROM s2);
```

2、查询中包含UNION语句的情况

比如下边这个查询语句中也包含2个SELECT关键字:

```
SELECT * FROM s1
UNION SELECT * FROM s2 ;
```

查询语句中每出现一个SELECT关键字，MySQL就会为它分配一个唯一的id值。这个id值就是EXPLAIN语句的第一个列。

###### 单SELECT关键字

比如下边这个查询中只有一个SELECT关键字，所以EXPLAIN的结果中也就只有一条id列为1的记录∶

```
EXPLAIN SELECT * FROM s1 WHERE order_no = 'a';
```

###### 连接查询

对于连接查询来说，一个SELEOT关键字后边的FROM子句中可以跟随多个表，所以在连接查询的执行计划中，每个表都会对应一条记录，但是这些记录的id值都是相同的，比如:

```
EXPLAIN SELECT * FROM s1 WHERE order_no = 'a';
```

可以看到，上述连接查询中参与连接的s1和s2表分别对应一条记录，但是这两条记录对应的id值都是1。这里需要大家记住的是，在连接查询的执行计划中，每个表都会对应一条记录，这些记录的id列的值是相同的。

###### 包含子查询

对于包含子查询的查询语句来说，就可能涉及多个SELECT关键字，所以在包含子查询的查询语句的执行计划中，每个SELECT关键字都会对应一个唯一的id值，比如这样:

```
EXPLAIN
SELECT * FROM s1 WHERE id IN (SELECT id FROM s2) OR order_no = 'a';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/93136f4766424e9e91a0b065908ad1c8.png)

但是这里大家需要特别注意，查询优化器可能对涉及子查询的查询语句进行重写，从而转换为连接查询。所以如果我们想知道查询优化器对某个包含子查询的语句是否进行了重写，直接查看执行计划就好了，比如说:

```
EXPLAIN
SELECT * FROM s1 WHERE id IN (SELECT id FROM s2 WHERE order_no = 'a');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6475b28cd68144b89566254b0891a210.png)

可以看到，虽然我们的查询语句是一个子查询，但是执行计划中s1和s2表对应的记录的id值全部是1，这就表明了查询优化器将子查询转换为了连接查询,

###### 包含UNION子句

对于包含UNION子句的查询语句来说，每个SELECT关键字对应一个id值也是没错的，不过还是有点儿特别的东西，比方说下边这个查询:

```
EXPLAIN
SELECT * FROM s1 UNION SELECT * FROM s2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/4907ca3c4cea47a0add9684f8081acc3.png)

这个语句的执行计划的第三条记录为什么这样？UNION
子句会把多个查询的结果集合并起来并对结果集中的记录进行去重，怎么去重呢? MySQL使用的是内部的临时表。正如上边的查询计划中所示，UNION 子句是为了把id为1的查询和id为2的查询的结果集合并起来并去重，所以在内部创建了一个名为&#x3c;union1，2>的临时表（就是执行计划第三条记录的table列的名称)，id为NULL表明这个临时表是为了合并两个查询的结果集而创建的。

跟UNION 对比起来，UNION
ALL就不需要为最终的结果集进行去重，它只是单纯的把多个查询的结果集中的记录合并成一个并返回给用户，所以也就不需要使用临时表。所以在包含UNION ALL子句的查询的执行计划中，就没有那个id为NULL的记录，如下所示:

```
EXPLAIN
SELECT * FROM s1 UNION ALL SELECT * FROM s2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f58b6838d5c34edc8580e1309a96cd16.png)

##### table

不论我们的查询语句有多复杂，里边包含了多少个表，到最后也是需要对每个表进行单表访问的，MySQL规定EXPLAIN语句输出的每条记录都对应着某个单表的访问方法，该条记录的table列代表着该表的表名。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/ad26adcd3f0b45d39ebc12b51de8c74b.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/e41c8c8a619c4781b0fd7293c556ed54.png)

可以看见，只涉及对s1表的单表查询，所以EXPLAIN输出中只有一条记录，其中的table列的值是s1，而连接查询的执行计划中有两条记录，这两条记录的table列分别是s1和s2.

##### partitions

和分区表有关，一般情况下我们的查询语句的执行计划的partitions列的值都是NULL。

##### type

我们前边说过执行计划的一条记录就代表着MySQL对某个表的执行查询时的访问方法/访问类型，其中的type列就表明了这个访问方法/访问类型是个什么东西，是较为重要的一个指标，结果值从最好到最坏依次是：

出现比较多的是system>const>eq_ref>ref>range>index>ALL

一般来说，得保证查询至少达到range级别，最好能达到ref。

###### system

当表中只有一条记录并且该表使用的存储引擎的统计数据是精确的，比如MyISAM、Memory，那么对该表的访问方法就是system。

```
explain select * from test_myisam;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/0cd60414ae624c2aad6b7870d8702116.png)

当然，如果改成使用InnoDB存储引擎，试试看执行计划的type列的值是什么。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/5f326bb8471841da9b8b750877c497b8.png)

###### const

就是当我们根据主键或者唯一二级索引列与常数进行等值匹配时，对单表的访问方法就是const。因为只匹配一行数据，所以很快。

例如将主键置于where列表中

```
EXPLAIN
SELECT * FROM s1 WHERE id = 716;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/854f80afc83e4d53b368a29634dea02a.png)

B+树叶子节点中的记录是按照索引列排序的，对于的聚簇索引来说，它对应的B+树叶子节点中的记录就是按照id列排序的。B+树矮胖，所以这样根据主键值定位一条记录的速度很快。类似的，我们根据唯一二级索引列来定位一条记录的速度也很快的，比如下边这个查询：

```
SELECT * FROM
order_exp WHERE insert_time=’’ and order_status=’’ and expire_time=’’ ;
```

这个查询的执行分两步，第一步先从u_idx_day_status对应的B+树索引中根据索引列与常数的等值比较条件定位到一条二级索引记录，然后再根据该记录的id值到聚簇索引中获取到完整的用户记录。

MySQL把这种通过主键或者唯一二级索引列来定位一条记录的访问方法定义为：const，意思是常数级别的，代价是可以忽略不计的。

不过这种const访问方法只能在主键列或者唯一二级索引列和一个常数进行等值比较时才有效，如果主键或者唯一二级索引是由多个列构成的话，组成索引的每一个列都是与常数进行等值比较时，这个const访问方法才有效。

对于唯一二级索引来说，查询该列为NULL值的情况比较特殊，因为唯一二级索引列并不限制 NULL 值的数量，所以上述语句可能访问到多条记录，也就是说is null不可以使用const访问方法来执行。

###### eq_ref

在连接查询时，如果被驱动表是通过主键或者唯一二级索引列等值匹配的方式进行访问的〈如果该主键或者唯一二级索引是联合索引的话，所有的索引列都必须进行等值比较)，则对该被驱动表的访问方法就是eq_ref。

(***驱动表与被驱动表：*** *A**表和B**表join**连接查询，如果通过A**表的结果集作为循环基础数据，然后一条一条地通过该结果集中的数据作为过滤条件到B**表中查询数据，然后合并结果。那么我们称A**表为驱动表，B**表为被驱动表*)

比方说:

```
EXPLAIN
SELECT * FROM s1 INNER JOIN s2 ON s1.id = s2.id;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a33c7b8ce8e449d79866fc374baa7739.png)

从执行计划的结果中可以看出，MySQL打算将s2作为驱动表，s1作为被驱动表，重点关注s1的访问方法是eq_ref，表明在访问s1表的时候可以通过主键的等值匹配来进行访问。

###### ref

当通过普通的二级索引列与常量进行等值匹配时来查询某个表，那么对该表的访问方法就可能是ref。

本质上也是一种索引访问，它返回所有匹配某个单独值的行，然而，它可能会找到多个符合条件的行，所以他属于查找和扫描的混合体

```
EXPLAIN
SELECT * FROM s1 WHERE order_no = 'a';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/adbe165526944750b5087866b270c858.png)

对于这个查询，我们当然可以选择全表扫描来逐一对比搜索条件是否满足要求，我们也可以先使用二级索引找到对应记录的id值，然后再回表到聚簇索引中查找完整的用户记录。

由于普通二级索引并不限制索引列值的唯一性，所以可能找到多条对应的记录，也就是说使用二级索引来执行查询的代价取决于等值匹配到的二级索引记录条数。如果匹配的记录较少，则回表的代价还是比较低的，所以MySQL可能选择使用索引而不是全表扫描的方式来执行查询。这种搜索条件为二级索引列与常数等值比较，采用二级索引来执行查询的访问方法称为：ref。

对于普通的二级索引来说，通过索引列进行等值比较后可能匹配到多条连续的记录，而不是像主键或者唯一二级索引那样最多只能匹配1条记录，所以这种ref访问方法比const要差些，但是在二级索引等值比较时匹配的记录数较少时的效率还是很高的（如果匹配的二级索引记录太多那么回表的成本就太大了）。

###### range

如果使用索引获取某些范围区间的记录，那么就可能使用到range访问方法，一般就是在你的where语句中出现了between、&#x3c;、>、in等的查询。

这种范围扫描索引扫描比全表扫描要好，因为它只需要开始于索引的某一点，而结束语另一点，不用扫描全部索引。

```
EXPLAIN
SELECT * FROM s1 WHERE order_no IN ('a', 'b', 'c');

EXPLAIN
SELECT * FROM s1 WHERE order_no > 'a' AND order_no < 'b';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/e04fb43a98264bf5850510fdbe1db8d5.png)

这种利用索引进行范围匹配的访问方法称之为：range。

此处所说的使用索引进行范围匹配中的 `索引` 可以是聚簇索引，也可以是二级索引。

###### index

当我们可以使用索引覆盖，但需要扫描全部的索引记录时，该表的访问方法就是index。

```
EXPLAIN
SELECT insert_time FROM s1 WHERE expire_time = '2021-03-22 18:36:47';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a79786e8fe9147eb97696eaa28f1fada.png)

###### all

最熟悉的全表扫描，将遍历全表以找到匹配的行

```
EXPLAIN
SELECT * FROM s1;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/315c3953f3a64e249435e19a5ce2089f.png)

##### possible_keys与key

在EXPLAIN 语句输出的执行计划中,possible_keys列表示在某个查询语句中，对某个表执行单表查询时可能用到的索引有哪些，key列表示实际用到的索引有哪些，如果为NULL，则没有使用索引。比方说下边这个查询:。

```
EXPLAIN SELECT order_note FROM s1 WHERE
insert_time = '2021-03-22 18:36:47';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d2f72f3156cd44369ed275e5991dcbb2.png)

上述执行计划的possible keys列的值表示该查询可能使用到u_idx_day_status,idx_insert_time两个索引，然后key列的值是u_idx_day_status，表示经过查询优化器计算使用不同索引的成本后，最后决定使用u_idx_day_status来执行查询比较划算。

##### key_len

key_len列表示当优化器决定使用某个索引执行查询时，该索引记录的最大长度，计算方式是这样的：

对于使用固定长度类型的索引列来说，它实际占用的存储空间的最大长度就是该固定值，对于指定字符集的变长类型的索引列来说，比如某个索引列的类型是VARCHAR(100)，使用的字符集是utf8，那么该列实际占用的最大存储空间就是100 x 3 = 300个字节。

如果该索引列可以存储NULL值，则key_len比不可以存储NULL值时多1个字节。

对于变长字段来说，都会有2个字节的空间来存储该变长列的实际长度。

⽐如下边这个查询：

```
EXPLAIN
SELECT * FROM s1 WHERE id = 718;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f898e5b7cfa54e3e9c63cd3b11a3920e.png)

由于id列的类型是bigint，并且不可以存储NULL值，所以在使用该列的索引时key_len大小就是8。

对于可变长度的索引列来说，比如下边这个查询:

```
EXPLAIN
SELECT * FROM s1 WHERE order_no = 'a';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/74a8a80a304545c69e8fbaf4325908de.png)

由于order_no列的类型是VARCHAR(50)，所以该列实际最多占用的存储空间就是50*3字节，又因为该列是可变长度列，所以key_len需要加2，所以最后ken_len的值就是152。

MySQL在执行计划中输出key_len列主要是为了让我们区分某个使用联合索引的查询具体用了几个索引列(复合索引有最左前缀的特性，如果复合索引能全部使用上，则是复合索引字段的索引长度之和，这也可以用来判定复合索引是否部分使用，还是全部使用)，而不是为了准确的说明针对某个具体存储引擎存储变长字段的实际长度占用的空间到底是占用1个字节还是2个字节。

##### rows

如果查询优化器决定使用全表扫描的方式对某个表执行查询时，执行计划的rows列就代表预计需要扫描的行数，如果使用索引来执行查询时，执行计划的rows列就代表预计扫描的索引记录行数。比如下边两个个查询:

```
EXPLAIN
SELECT * FROM s1 WHERE order_no > 'z';

EXPLAIN
SELECT * FROM s1 WHERE order_no > 'a';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b3527b40c9494d17b4e608b3d8a21db6.png)

我们看到执行计划的rows列的值是分别是1和10573，这意味着查询优化器在经过分析使用idx_order_no进行查询的成本之后，觉得满足order_no> ' a '这个条件的记录只有1条，觉得满足order_no> ' a '这个条件的记录有10573条。

##### filtered

查询优化器预测有多少条记录满⾜其余的搜索条件，什么意思呢？看具体的语句：

```
EXPLAIN SELECT *
FROM s1 WHERE id > 5890 AND order_note = 'a';
```

从执行计划的key列中可以看出来，该查询使用 PRIMARY索引来执行查询，从rows列可以看出满足id > 5890的记录有5286条。执行计划的filtered列就代表查询优化器预测在这5286条记录中，有多少条记录满足其余的搜索条件，也就是order_note = 'a'这个条件的百分比。此处filtered列的值是10.0，说明查询优化器预测在5286条记录中有10.00%的记录满足order_note = 'a'这个条件。

对于单表查询来说，这个filtered列的值没什么意义，我们更关注在连接查询中驱动表对应的执行计划记录的filtered值，比方说下边这个查询:

```
EXPLAIN SELECT * FROM s1 INNER JOIN s2 ON s1.order_no = s2.order_no WHERE s1.order_note > '你好，李焕英';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6ba004e4db004b03b5632d9aa1a327c9.png)

从执行计划中可以看出来，查询优化器打算把
1当作驱动表，s2当作被驱动表。我们可以看到驱动表s1表的执行计划的rows列为10573，filtered列为33.33 ，这意味着驱动表s1的扇出值就是10573 x 33.33 % = 3524.3，这说明还要对被驱动表执行大约3524次查询。

##### Extra

顾名思义，Extra列是用来说明一些额外信息的，我们可以通过这些额外信息来更准确的理解MySQL到底将如何执行给定的查询语句

### 1.3.5.查询优化器

一条SQL语句在MySQL执行的过程如下：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b0dc955876354f09938142e60bc1f4ce.png)

1.如果是查询语句（select语句），首先会查询缓存是否已有相应结果，有则返回结果，无则进行下一步（如果不是查询语句，同样调到下一步）

2.解析查询，创建一个内部数据结构（解析树），这个解析树主要用来SQL语句的语义与语法解析；

3.优化：优化SQL语句，例如重写查询，决定表的读取顺序，以及选择需要的索引等。这一阶段用户是可以查询的，查询服务器优化器是如何进行优化的，便于用户重构查询和修改相关配置，达到最优化。这一阶段还涉及到存储引擎，优化器会询问存储引擎，比如某个操作的开销信息、是否对特定索引有查询优化等。

### 1.3.6.高性能的索引使用策略

首先给大家总结下

### 索引失效场景:

**模型数空运最回**

模糊查询。like查询以%开头，会导致索引失效。可以有两种方式优化： a. 使用覆盖索引优化，只查询索引列； b. 把%放后面，索引生效

数据类型。编写sql时要保证索引字段与匹配数据类型一致。

函数。索引字段不做函数处理

空。null值需要慎重使用 唯一索引有null值  not null & null（不同版本会有不同。5.7refornull 8组合其他null的大概率能走，不过也可能会all）

运算。索引字段不做运算

最左匹配。尽量满足最左匹配

回表超过临界值。避免回表尽量覆盖索引

### 具体注意事项：

#### 1.3.6.1.不在索引列上做任何操作

我们通常会看到一些查询不当地使用索引，或者使得MySQL无法使用已有的索引。如果查询中的列不是独立的，则 MySQL就不会使用索引。“独立的列”是指索引列不能是表达式的一部分，也不能是函数的参数。

例如，我们假设id上有主键索引，但是下面这个查询无法使用主键索引:

```
EXPLAIN SELECT * FROM order_exp WHERE id + 1 = 17;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/4654e2c912994f258e99f87a7fbf722c.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8b61405caded4ebb9cf0aa43e97db2ab.png)

凭肉眼很容易看出 WHERE中的表达式其实等价于id= 16，但是MySQL无法自动解析这个方程式。这完全是用户行为。我们应该养成简化WHERE条件的习惯，始终将索引列单独放在比较符号的一侧。

下面是另一个常见的错误:

在索引列上使用函数，也是无法利用索引的。

```
EXPLAIN SELECT * from order_exp WHERE YEAR(insert_time)=YEAR(DATE_SUB(NOW(),INTERVAL 1 YEAR));
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/40f54f165b8b45138d0adf947eb013b4.png)

```
EXPLAIN SELECT * from order_exp WHERE insert_time BETWEEN str_to_date('01/01/2021', '%m/%d/%Y') and str_to_date('12/31/2021', '%m/%d/%Y');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d8e9925bf3b445a3812aeca5ab3caa9c.png)

#### 1.3.6.2.尽量全值匹配

建立了联合索引列后，如果我们的搜索条件中的列和索引列一致的话，这种情况就称为全值匹配，比方说下边这个查找语句：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2ef49edd0615433c8d878da02793f414.png)

```
 EXPLAIN select * from order_exp where insert_time='2021-03-22 18:34:55' and order_status=0 and expire_time='2021-03-22 18:35:14';
```

我们建立的u_idx_day_statusr索引包含的3个列在这个查询语句中都展现出来了，联合索引中的三个列都可能被用到。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d8ba5a3726cc4fc59bdd677cbfe314b7.png)

有的同学也许有个疑问，WHERE子句中的几个搜索条件的顺序对查询结果有啥影响么？

也就是说如果我们调换 `insert_time`, `order_status`, `expire_time`这几个搜索列的顺序对查询的执行过程有影响么？

比方说写成下边这样：

```
EXPLAIN select * from order_exp where  order_status=0 and insert_time='2021-03-22 18:34:55'  and expire_time='2021-03-22 18:35:14';
```

放心，MySQL没这么蠢，查询优化器会分析这些搜索条件并且按照可以使用的索引中列的顺序来决定先使用哪个搜索条件，后使用哪个搜索条件。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/5341da5a2f8c4d548496e938571446fe.png)

所以，当建立了联合索引列后，能在where条件中使用索引的尽量使用。

#### 1.3.6.3.最佳左前缀法则

建立了联合索引列，如果搜索条件不够全值匹配怎么办？在我们的搜索语句中也可以不用包含全部联合索引中的列，但要遵守最左前缀法则。指的是查询从索引的最左前列开始并且不跳过索引中的列。

搜索条件中必须出现左边的列才可以使用到这个B+树索引

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6470ee4f75b54fe9a3895a04a285445e.png)

```
EXPLAIN select * from order_exp where insert_time='2021-03-22 18:23:42' and order_status=1;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d6c0f39567d44f488b33673d7426fae1.png)

```
EXPLAIN select * from order_exp where insert_time='2021-03-22 18:23:42' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2cb52dc41f2d467485a6540a03fdad13.png)

搜索条件中没有出现左边的列不可以使用到这个B+树索引

```
EXPLAIN SELECT * FROM order_exp WHERE order_status=1;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2be581275fda43d9bde9e919ca08edea.png)

```
EXPLAIN Select * from s1 where order_status=1 and expire_time='2021-03-22 18:35:14';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6904ca07e50942b9a89624601b7e76d5.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8c5afbb6141042729c9cb6b62eae9be3.png)

那为什么搜索条件中必须出现左边的列才可以使用到这个B+树索引呢？比如下边的语句就用不到这个B+树索引么？

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6d37e1eeeac044c8935919a484dc12f4.png)

因为B+树的数据页和记录先是按照insert_time列的值排序的，在insert_time列的值相同的情况下才使用order_status列进行排序，也就是说insert_time列的值不同的记录中order_status的值可能是无序的。而现在你跳过insert_time列直接根据order_status的值去查找，怎么可能呢？expire_time也是一样的道理，那如果我就想在只使用expire_time的值去通过B+树索引进行查找咋办呢？这好办，你再对expire_time列建一个B+树索引就行了。

但是需要特别注意的一点是，如果我们想使用联合索引中尽可能多的列，搜索条件中的各个列必须是联合索引中从最左边连续的列。比方说联合索引u_idx_day_status中列的定义顺序是 `insert_time`, `order_status`, `expire_time`，如果我们的搜索条件中只有insert_time和expire_time，而没有中间的order_status，

```
EXPLAIN select * from order_exp where insert_time='2021-03-22 18:23:42' and expire_time='2021-03-22 18:35:14';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/71c66aeee5624538b15c1ac65bfb441c.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b0c30125c76547549274176558ba4eac.png)

请注意key_len,只有5，说明只有insert_time用到了，其他的没有用到。

#### 1.3.6.4.范围条件放最后

这一点，也是针对联合索引来说的，前面我们反复强调过，所有记录都是按照索引列的值从小到大的顺序排好序的，而联合索引则是按创建索引时的顺序进行分组排序。

比如：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/c6343d4b9e404154a5d9542ab0991961.png)

```
EXPLAIN select * from order_exp_cut where insert_time>'2021-03-22 18:23:42' and insert_time<'2021-03-22 18:35:00';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/288265c4c0ef489eb6fd23f908389ba4.png)

由于B+树中的数据页和记录是先按insert_time列排序的，所以我们上边的查询过程其实是这样的：

找到insert_time值为'2021-03-22 18:23:42' 的记录。

找到insert_timee值为'2021-03-22 18:35:00'的记录。

由于所有记录都是由链表连起来的，所以他们之间的记录都可以很容易的取出来，找到这些记录的主键值，再到聚簇索引中回表查找完整的记录。

但是如果对多个列同时进行范围查找的话，只有对索引最左边的那个列进行范围查找的时候才能用到B+树索引：

```
select * from order_exp_cut where insert_time>'2021-03-22 18:23:42' and insert_time<'2021-03-22 18:35:00' and order_status > -1;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b4ef55a0bbb043aa9fb6ea7aea4014d1.png)

上边这个查询可以分成两个部分：

通过条件insert_time>'2021-03-22 18:23:42' and insert_time&#x3c;'2021-03-22 18:35:00' 来对insert_time进行范围，查找的结果可能有多条insert_time值不同的记录，

对这些insert_time值不同的记录继续通过order_status>-1条件继续过滤。

这样子对于联合索引u_idx_day_status来说，只能用到insert_time列的部分，而用不到order_status列的部分（这里的key_len和之前的SQL的是一样长），因为只有insert_time值相同的情况下才能用order_status列的值进行排序，而这个查询中通过insert_time进行范围查找的记录中可能并不是按照order_status列进行排序的，所以在搜索条件中继续以order_status列进行查找时是用不到这个B+树索引的。

**所以对于一个联合索引来说，虽然对多个列都进行范围查找时只能用到最左边那个索引列，但是如果左边的列是精确查找，则右边的列可以进行范围查找：**

```
EXPLAIN select * from order_exp_cut
where insert_time='2021-03-22 18:34:55' and order_status=0 and expire_time>'2021-03-22
18:23:57' and expire_time<'2021-03-22 18:35:00' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/591940f39f1b4b38aa5b32e55202bd60.png)

**而中间有范围查询会导致后面的列全部失效，无法充分利用这个联合索引：**

```
EXPLAIN select * from order_exp_cut
where insert_time='2021-03-22 18:23:42' and order_status>-1 and expire_time='2021-03-22
18:35:14';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/5874bb991dc1459cabd34bfa0bc7299a.png)

#### 1.3.6.5.覆盖索引尽量用

覆盖索引是非常有用的工具，能够极大地提高性能，三星索引里最重要的那颗星就是宽索引星。考虑一下如果查询只需要扫描索引而无须回表，会带来多少好处:

索引条目通常远小于数据行大小，所以如果只需要读取索引，那 MySQL就会极大地减少数据访问量。这对缓存的负载非常重要，因为这种情况下响应时间大部分花费在数据拷贝上。覆盖索引对于I/O密集型的应用也有帮助，因为索引比数据更小,更容易全部放入内存中。

因为索引是按照列值顺序存储的，所以对于I/O密集型的范围查询会比随机从磁盘读取每一行数据的I/O要少得多。

由于InnoDB的聚簇索引，覆盖索引对InnoDB表特别有用。InnoDB的二级索引在叶子节点中保存了行的主键值，所以如果二级主键能够覆盖查询，则可以避免对主键索引的二次查询。

尽量使用覆盖索引(只访问索引的查询(索引列和查询列一致))，不是必要的情况下减少select*，除非是需要将表中的全部列检索后，进行缓存。

```
EXPLAIN  select * from
order_exp_cut where insert_time='2021-03-22 18:34:55' and order_status=0 and
expire_time='2021-03-22 18:35:04' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/9dde17c64e9648cd8c41d8ed8e3b2b65.png)

使用具体名称取代*

```
EXPLAIN  select expire_time,id from
order_exp_cut where insert_time='2021-03-22 18:34:55' and order_status=0 and
expire_time='2021-03-22 18:35:04' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/c50ef9c9280f4d8e94cf27cca596f9c1.png)

**解释一下Extra中的Using index**

当我们的查询列表以及搜索条件中只包含属于某个索引的列，也就是在可以**使用索引覆盖的情况**下，在Extra列将会提示该额外信息。以上的查询中只需要用到u_idx_day_status而不需要回表操作：

#### 1.3.6.6.不等于要慎用

mysql 在使用不等于(!= 或者&#x3c;>)的时候无法使用索引会导致全表扫描

```
EXPLAIN  SELECT * FROM order_exp WHERE order_no <> 'DD00_6S';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d75a6e6d69f547caa3b8661b0a369973.png)

**解释一下Extra中的Using where**
当我们使用全表扫描来执行对某个表的查询，并且该语句的WHERE子句中有针对该表的搜索条件时，在Extra列中会提示上述额外信息。

#### 1.3.6.7.Null/Not 有影响

需要注意null/not null对索引的可能影响

**表order_exp的order_no为索引列，同时不允许为null，**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/8ed4193b0c934d5dbbbc34f8dd581836.png)

```
explain SELECT * FROM order_exp WHERE order_no is null;
explain SELECT * FROM order_exp WHERE order_no is not null;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/aa527c85faf945e6a81faaa7a0025409.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/ec817b8cf6e5488bb6e9382e503828f0.png)

可以看见，order_no is null的情况下，MySQL直接表示Impossible WHERE(查询语句的WHERE子句永远为FALSE时将会提示该额外信息)，对于 is not null直接走的全表扫描。

**表order_exp_cut的order_no为索引列，同时允许为null，**

```
explain SELECT * FROM order_exp_cut WHERE order_no is null;
explain SELECT * FROM order_exp_cut WHERE order_no is not null;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/227c7a3ab927457d84739f1c3583ccdd.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d954036891374b18a6ef0671d793cd86.png)

is null会走ref类型的索引访问，is not null;依然是全表扫描。所以总结起来：

is not null容易导致索引失效，is null则会区分被检索的列是否为null，如果是null则会走ref类型的索引访问，如果不为null，也是全表扫描。

**但是当联合索引上使用时覆盖索引时，情况会有一些不同(order_exp_cut表的order_no可为空)：**

```
explain SELECT order_status,expire_time FROM order_exp WHERE insert_time is null;
explain SELECT order_status,expire_time FROM order_exp WHERE insert_time is not null;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/14d36c91cf0840a2b2be921b057e6f7a.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/42ebdd9dd8774f0d939440cde50512e1.png)

```
explain SELECT order_status,expire_time FROM order_exp_cut WHERE insert_time is null;
explain SELECT order_status,expire_time FROM order_exp_cut WHERE insert_time is not null;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/d2fc5cb60d1c455e92b38dd4f1c87ebe.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/50565fb21ad145d89d0329c126aca8cf.png)

根据system>const>eq_ref>ref>range>index>ALL 的原则，看起来在联合索引中，is not null的表现会更好（如果列可为null的话），但是key_len的长度增加了1。所以总的来说，在设计表时列尽可能的不要声明为null。

#### 1.3.6.8.Like查询要当心

like以通配符开头('%abc...')，mysql索引失效会变成全表扫描的操作

```
explain SELECT * FROM order_exp WHERE order_no like '%_6S';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/ac911fc11114479caa8ae55ac317bacf.png)

此时如果使用覆盖索引可以改善这个问题

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/0dd075168f3e48d69eca71710c72ed9e.png)

```
explain SELECT order_status,expire_time FROM order_exp_cut WHERE insert_time like '%18:35:09';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/e494db4f81c846db89e74e6d23cdc646.png)

#### 1.3.6.9.字符类型加引号

字符串不加单引号索引失效

```
explain SELECT * FROM order_exp WHERE order_no = 6;
explain SELECT * FROM order_exp WHERE order_no = '6';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/511255e7474c4502b15419058913d0cc.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/97f9ff147b5a4954aaf006f00b60660d.png)

MySQL的查询优化器，会自动的进行类型转换，比如上个语句里会尝试将order_no转换为数字后和6进行比较，自然造成索引失效。

#### 1.3.6.10.使用or关键字时要注意

```
explain SELECT * FROM order_exp WHERE order_no = 'DD00_6S' OR order_no = 'DD00_9S';
explain SELECT * FROM order_exp WHERE expire_time= '2021-03-22 18:35:09'  OR order_note = 'abc';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/55f8e2400c4845e5b337c1a122ea4737.png)

表现是不一样的，第一个SQL的or是相同列，相当于产生两个扫描区间，可以使用上索引。

第二个SQL中or是不同列，并且order_note不是索引。所以只能全表扫描

当然如果两个条件都是索引列，情况会有变化：

```
explain  SELECT * FROM order_exp WHERE expire_time= '2021-03-22 18:35:09'  OR order_no = 'DD00_6S';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/deabc3433e2440c5be499b296789d427.png)

这也给了我们提示，如果我们将 SQL改成union all

```
explain SELECT * FROM order_exp WHERE expire_time= '2021-03-22 18:35:09' 
					union all SELECT * FROM order_exp WHERE order_note = 'abc';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/643d0629a531459594e318cc0ea6547b.png)

当然使用覆盖扫描也可以改善这个问题：

```
explain SELECT order_status,id FROM order_exp_cut WHERE insert_time='2021-03-22 18:34:55' or expire_time='2021-03-22 18:28:28';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/aa9bc2fae8c54d4b86a3a38720cc42c2.png)

#### 1.3.6.11.使用索引扫描来做排序和分组

MySQL有两种方式可以生成有序的结果﹔通过排序操作﹔或者按索引顺序扫描施﹔如果EXPLAIN出来的type列的值为“index”，则说明MySQL使用了索引扫描来做排序。

扫描索引本身是很快的，因为只需要从一条索引记录移动到紧接着的下一条记录。但如果索引不能覆盖查询所需的全部列，那就不得不每扫描一条索引记录就都回表查询一次对应的行。这基本上都是随机I/O，因此按索引顺序读取数据的速度通常要比顺序地全表扫描慢，尤其是在IO密集型的工作负载时。

MySQL可以使用同一个索引既满足排序，又用于查找行。因此，如果可能，设计索引时应该尽可能地同时满足这两种任务，这样是最好的。

只有当索引的列顺序和ORDER BY子句的顺序完全一致，并且所有列的排序方向（倒序或正序）都一样时，MySQL才能够使用索引来对结果做排序。如果查询需要关联多张表，则只有当0RDER BY子句引用的字段全部为第一个表时，才能使用索引做排序。

#### 1.3.6.12.排序要当心

**ASC、DESC别混用**

对于使用联合索引进行排序的场景，我们要求各个排序列的排序顺序是一致的，也就是要么各个列都是ASC规则排序，要么都是DESC规则排序。

**排序列包含非同一个索引的列**

用来排序的多个列不是一个索引里的，这种情况也不能使用索引进行排序

```
explain
SELECT * FROM order_exp order by
order_no,insert_time;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/52bc3ba85bc1433cbed4510cba638556.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/645c2fa335824da292d3dcfcb32969e8.png)

#### 1.3.6.13.尽可能按主键顺序插入行

最好避免随机的（不连续且值的分布范围非常大）聚簇索引，特别是对于I/O密集型的应用。例如，从性能的角度考虑，使用UUID来作为聚簇索引则会很糟糕，它使得聚簇索引的插入变得完全随机，这是最坏的情况，使得数据没有任何聚集特性。

最简单的方法是使用AUTO_INCREMENT自增列。这样可以保证数据行是按顺序写入，对于根据主键做关联操作的性能也会更好。

注意到向UUID主键插入行不仅花费的时间更长，而且索引占用的空间也更大。这一方面是由于主键字段更长﹔另一方面毫无疑问是由于页分裂和碎片导致的。

因为主键的值是顺序的，所以InnoDB把每一条记录都存储在上一条记录的后面。当达到页的最大填充因子时(InnoDB默认的最大填充因子是页大小的15/16，留出部分空间用于以后修改)，下一条记录就会写入新的页中。一旦数据按照这种顺序的方式加载,主键页就会近似于被顺序的记录填满,这也正是所期望的结果。

如果新行的主键值不一定比之前插入的大，所以InnoDB无法简单地总是把新行插入到索引的最后，而是需要为新的行寻找合适的位置-—通常是已有数据的中间位置——并且分配空间。这会增加很多的额外工作，并导致数据分布不够优化。下面是总结的一些缺点:

写入的目标页可能已经刷到磁盘上并从缓存中移除，或者是还没有被加载到缓存中，InnoDB在插入之前不得不先找到并从磁盘读取目标页到内存中。这将导致大量的随机IO。

因为写入是乱序的，InnoDB不得不频繁地做页分裂操作，以便为新的行分配空间。页分裂会导致移动大量数据，一次插入最少需要修改三个页而不是一个页。

所以使用InnoDB时应该尽可能地按主键顺序插入数据，并且尽可能地使用单调增加的聚簇键的值来插入新行。

#### 1.3.6.14.优化Count查询

首先要注意，COUNT()是一个特殊的函数，有两种非常不同的作用:它可以统计某个列值的数量，也可以统计行数。

在统计列值时要求列值是非空的（不统计NULL)。

COUNT()的另一个作用是统计结果集的行数。常用的就是就是当我们使用COUNT(*)。实际上，它会忽略所有的列而直接统计所有的行数。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/3264f862df374302bef83c9459ad0a7a.png)

```
select count(*) from test;
select count(c1) from test;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/989e64fc120f45288787f480e1746dc1.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/52fccea24657442db67c3d7b102de0fa.png)

通常来说，COUNT()都需要扫描大量的行（意味着要访问大量数据）才能获得精确的结果，因此是很难优化的。在MySQL层面能做的基本只有索引覆盖扫描了。如果这还不够,就需要考虑修改应用的架构，可以用估算值取代精确值，可以增加汇总表，或者增加类似Redis这样的外部缓存系统。

#### 1.3.6.15.优化limit分页

在系统中需要进行分页操作的时候，我们通常会使用LIMIT加上偏移量的办法实现，同时加上合适的ORDER BY子句。

一个非常常见又令人头疼的问题就是，在偏移量非常大的时候，例如可能是

```
select * from order_exp limit 10000,10;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/358846c9b2db4bf79de4e2f200c5e46f.png)

这样的查询，这时MySQL需要查询10010条记录然后只返回最后10条，前面10 000条记录都将被抛弃，这样的代价非常高。

优化此类分页查询的一个最简单的办法是

会先查询翻页中需要的N条数据的主键值，然后根据主键值回表查询所需要的N条数据，在此过程中查询N条数据的主键id在索引中完成，所以效率会高一些。

```
EXPLAIN SELECT * FROM (select id from order_exp limit 10000,10) b,order_exp
					a where a.id = b.id;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b24ab67fa56e4da1b7fa151e0098c004.png)

从执行计划中可以看出，首先执行子查询中的order_exp表，根据主键做索引全表扫描，然后与a表通过id做主键关联查询，相比传统写法中的全表扫描效率会高一些。

从两种写法上能看出性能有一定的差距，虽然并不明显，但是随着数据量的增大，两者执行的效率便会体现出来。

上面的写法虽然可以达到一定程度的优化，但还是存在性能问题。最佳的方式是在业务上进行配合修改为以下语句：

```
EXPLAIN select * from order_exp where id > 67 order by id limit 10;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6efb18da3d19465e8538cb4e042d9e86.png)

采用这种写法，需要前端通过点击More来获得更多数据，而不是纯粹的翻页，因此，每次查询只需要使用上次查询出的数据中的id来获取接下来的数据即可，但这种写法需要业务配合。

#### 1.3.6.16.关于Null的特别说明

对于Null到底算什么，存在着分歧：

1、有的认为NULL值代表一个未确定的值，MySQL认为任何和NULL值做比较的表达式的值都为NULL，包括select
null=null和select null!=null;

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/11ebee5ff9db49b6bef2e80d2b2e46bd.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/3e152ca5c31048a5afca4a7611bc5798.png)

所以每一个NULL值都是独一无二的。

2、有的认为其实NULL值在业务上就是代表没有，所有的NULL值和起来算一份；

3、有的认为这NULL完全没有意义，所以在统计数量时压根儿不能把它们算进来。

假设一个表中某个列c1的记录为(2,1000,null,null)，在第一种情况下，表中c1的记录数为4，第二种表中c1的记录数为3，第三种表中c1的记录数为2。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/09c50dcca1ab4f33b2247edb054905ae.png)

在对统计索引列不重复值的数量时如何对待NULL值，MySQL专门提供了一个innodb_stats_method的系统变量，

https://dev.mysql.com/doc/refman/5.7/en/innodb-parameters.html#sysvar_innodb_stats_method

**这个系统变量有三个候选值：**

nulls_equal：认为所有NULL值都是相等的。这个值也是innodb_stats_method的默认值。

如果某个索引列中NULL值特别多的话，这种统计方式会让优化器认为某个列中平均一个值重复次数特别多，所以倾向于不使用索引进行访问。

nulls_unequal：认为所有NULL值都是不相等的。

如果某个索引列中NULL值特别多的话，这种统计方式会让优化器认为某个列中平均一个值重复次数特别少，所以倾向于使用索引进行访问。

nulls_ignored：直接把NULL值忽略掉。

而且有迹象表明，在MySQL5.7.22以后的版本，对这个innodb_stats_method的修改不起作用，MySQL把这个值在代码里写死为nulls_equal。也就是说MySQL在进行索引列的数据统计行为又把null视为第二种情况（NULL值在业务上就是代表没有，所有的NULL值和起来算一份），看起来，MySQL中对Null值的处理也很分裂。所以总的来说，对于列的声明尽可能的不要允许为null。



## 1.4.事务和事务的隔离级别

### 1.4.1.为什么需要事务

事务是数据库管理系统（DBMS）执行过程中的一个逻辑单位（不可再进行分割），由一个有限的数据库操作序列构成（多个DML语句，select语句不包含事务），要不全部成功，要不全部不成功。

A 给B 要划钱，A 的账户-1000元， B 的账户就要+1000元，这两个update 语句必须作为一个整体来执行，不然A 扣钱了，B 没有加钱这种情况就是错误的。那么事务就可以保证A 、B 账户的变动要么全部一起发生，要么全部一起不发生。

### 1.4.2.事务特性

事务应该具有4个属性：原子性、一致性、隔离性、持久性。这四个属性通常称为ACID特性。

**l  原子性（atomicity）**

**l  一致性（consistency）**

**l  隔离性（isolation）**

**l  持久性（durability）**

#### 1.4.2.1.原子性（atomicity）

一个事务必须被视为一个不可分割的最小单元，整个事务中的所有操作要么全部提交成功，要么全部失败，对于一个事务来说，不能只执行其中的一部分操作。比如：

天明借给诸葛老师1000元：

1.天明工资卡扣除1000元

2.诸葛老师工资卡增加1000元

整个事务的操作要么全部成功，要么全部失败，不能出现天明工资卡扣除，但是诸葛老师工资卡不增加的情况。如果原子性不能保证，就会很自然的出现一致性问题。

由undo log来保证，undo log记录事务需要回滚的日志信息，需要回滚是，取消已经执行成功的sql

#### 1.4.2.2.一致性（consistency）

一致性是指事务将数据库从一种一致性转换到另外一种一致性状态，在事务开始之前和事务结束之后数据库中数据的完整性没有被破坏。

天明借给诸葛老师1000元：

1.天明工资卡扣除1000元

2.诸葛老师工资卡增加1000元

扣除的钱（-500） 与增加的钱（500） 相加应该为0，或者说天明和诸葛老师的账户的钱加起来，前后应该不变。

有其他三种特性来保证一致性

#### 1.4.2.3.持久性（durability）

一旦事务提交，则其所做的修改就会永久保存到数据库中。此时即使系统崩溃，已经提交的修改数据也不会丢失。

bin log +redo log日志保证（详见redo log 二阶段提交） 。

前面几个特性的详细过程记得参看之前讲过的更新流程，尤其是三大日志和双写缓存部分的内容。

一个逻辑事务在 redo log 中的存储并不一定是连续的，但是一个原子性的 mtr 事务在 redo log 的存储一定是连续的，假设有2个逻辑事务在并行，每个逻辑事务都会产生多个 mtr 物理事务，在一个事务下的多个 mtr 通过链表来关联，都会关联到 xts id 上，xts id 代表事务 id，一个单调递增的 id，最后在 redo log 中的记录如下图所示:

![image-20240129184637294](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129184637294.png)

#### 1.4.2.4.隔离性（isolation）



一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。

如果隔离性不能保证，会导致什么问题？

天明借给诸葛老师生活费，借了两次，每次都是1000，天明的卡里开始有10000，诸葛老师的卡里开始有500，从理论上，借完后，天明的卡里有8000，诸葛老师的卡里应该有2500。

我们将天明向诸葛老师同时进行的两次转账操作分别称为T1和T2，在现实世界中T1和T2是应该没有关系的，可以先执行完T1，再执行T2，或者先执行完T2，再执行T1，结果都是一样的。但是很不幸，真实的数据库中T1和T2的操作可能交替执行的，

执行顺序来进行两次转账的话，最终我们看到，天明的账户里还剩9000元钱，相当于只扣了1000元钱，但是诸葛老师的账户里却成了2500元钱，多了1000元，这银行岂不是要亏死了？

所以对于现实世界中状态转换对应的某些数据库操作来说，不仅要保证这些操作以原子性的方式执行完成，而且要保证其它的状态转换不会影响到本次状态转换，这个规则被称之为隔离性。

由事务的MVCC多版本控制

### 1.4.3.事务并发引发的问题

我们知道MySQL是一个客户端／服务器架构的软件，对于同一个服务器来说，可以有若干个客户端与之连接，每个客户端与服务器连接上之后，就可以称之为一个会话（Session）。每个客户端都可以在自己的会话中向服务器发出请求语句，一个请求语句可能是某个事务的一部分，也就是对于服务器来说可能同时处理多个事务。

在上面我们说过事务有一个称之为隔离性的特性，理论上在某个事务对某个数据进行访问时，其他事务应该进行排队，当该事务提交之后，其他事务才可以继续访问这个数据，这样的话并发事务的执行就变成了串行化执行。

但是对串行化执行性能影响太大，我们既想保持事务的一定的隔离性，又想让服务器在处理访问同一数据的多个事务时性能尽量高些，当我们舍弃隔离性的时候，可能会带来什么样的数据问题呢？

#### 1.4.3.1.脏读

当一个事务读取到了另外一个事务修改但未提交的数据，被称为脏读。

![image-20240129191410506](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129191410506.png)

1、在事务A执⾏过程中，事务A对数据资源进⾏了修改，事务B读取了事务A修改后的数据。
2、由于某些原因，事务A并没有完成提交，发⽣了RollBack操作，则事务B读取的数据就是脏数据。
这种读取到另⼀个事务未提交的数据的现象就是脏读(Dirty Read)。

#### 1.4.3.2.不可重复读

当事务内相同的记录被检索两次，且两次得到的结果不同时，此现象称为不可重复读。

![image-20240129191434338](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129191434338.png)

事务B读取了两次数据资源，在这两次读取的过程中事务A修改了数据，导致事务B在这两次读取出来的
数据不⼀致。

#### 1.4.3.3.幻读

在事务执行过程中，另一个事务将新记录添加到正在读取的事务中时，会发生幻读。

count和范围查询时发生。

![image-20240129191459220](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129191459220.png)

事务B前后两次读取同⼀个范围的数据，在事务B两次读取的过程中事务A新增了数据，导致事务B后⼀
次读取到前⼀次查询没有看到的⾏。
幻读和不可重复读有些类似，但是幻读重点强调了读取到了之前读取没有获取到的记录。

### 1.1.4.SQL标准中的四种隔离级别

我们上边介绍了几种并发事务执行过程中可能遇到的一些问题，这些问题也有轻重缓急之分，我们给这些问题按照严重性来排一下序：

官方看看：

 美国国家标准协会 ANSI/ISO标准   sql92的版本

http://www.contrib.andrew.cmu.edu/~shadow/sql/sql1992.txt

![image-20240129191704878](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129191704878.png)

![image-20240129191751049](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129191751049.png)

脏读 > 不可重复读 > 幻读

我们上边所说的舍弃一部分隔离性来换取一部分性能在这里就体现在：设立一些隔离级别，隔离级别越低，越严重的问题就越可能发生。有一帮人（并不是设计MySQL的大叔们）制定了一个所谓的SQL标准，在标准中设立了4个隔离级别：

**READ UNCOMMITTED：未提交读。**

**READ COMMITTED：已提交读。**

**REPEATABLE READ：可重复读。**

**SERIALIZABLE：可串行化。**

SQL标准中规定，针对不同的隔离级别，并发事务可以发生不同严重程度的问题，具体情况如下：

也就是说：

**READ UNCOMMITTED隔离级别下，可能发生脏读、不可重复读和幻读问题。**

**READ COMMITTED隔离级别下，可能发生不可重复读和幻读问题，但是不可以发生脏读问题。**

**REPEATABLE READ隔离级别下，可能发生幻读问题，但是不可以发生脏读和不可重复读的问题。**

**SERIALIZABLE隔离级别下，各种问题都不可以发生。**

![image-20240129192005133](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129192005133.png)

### 1.4.5.MySQL中的隔离级别

不同的数据库厂商对SQL标准中规定的四种隔离级别支持不一样，比方说Oracle就只支持READ COMMITTED和SERIALIZABLE隔离级别。本书中所讨论的MySQL虽然支持4种隔离级别，但与SQL标准中所规定的各级隔离级别允许发生的问题却有些出入，**MySQL在REPEATABLE READ隔离级别下，是可以禁止幻读问题的发生的**。当然具体如何做到的后面会详细讲解。

![image-20240129191913134](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129191913134.png)



MySQL的默认隔离级别为REPEATABLE READ，我们可以手动修改事务的隔离级别。

#### 1.4.5.1.如何设置事务的隔离级别

我们可以通过下边的语句修改事务的隔离级别：

SET [GLOBAL|SESSION] TRANSACTION ISOLATION LEVEL level;

其中的level可选值有4个：

```
level: {
    REPEATABLE READ
   | READ COMMITTED
   | READ UNCOMMITTED
   | SERIALIZABLE
}
```

设置事务的隔离级别的语句中，在SET关键字后可以放置GLOBAL关键字、SESSION关键字或者什么都不放，这样会对不同范围的事务产生不同的影响，具体如下：

**使用GLOBAL关键字（在全局范围影响）：**

比方说这样：

```
SET GLOBAL TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

则： 只对执行完该语句之后产生的会话起作用。当前已经存在的会话无效。

**使用SESSION关键字（在会话范围影响）：**

比方说这样：

```
SET SESSION TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

则：对当前会话的所有后续的事务有效

该语句可以在已经开启的事务中间执行，但不会影响当前正在执行的事务。

如果在事务之间执行，则对后续的事务有效。

**上述两个关键字都不用（只对执行语句后的下一个事务产生影响）：**

比方说这样：

```
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

则：只对当前会话中下一个即将开启的事务有效。下一个事务执行完后，后续事务将恢复到之前的隔离级别。该语句不能在已经开启的事务中间执行，会报错的。

如果我们在服务器启动时想改变事务的默认隔离级别，可以修改启动参数transaction-isolation的值，比方说我们在启动服务器时指定了--transaction-isolation=SERIALIZABLE，那么事务的默认隔离级别就从原来的REPEATABLE READ变成了SERIALIZABLE。

想要查看当前会话默认的隔离级别可以通过查看系统变量transaction_isolation的值来确定：

```
SHOW VARIABLES LIKE 'transaction_isolation';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a863d53bff964d74a21b52de56bc97df.png)

或者使用更简便的写法：

```
SELECT @@transaction_isolation;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/390b1f7f9b7947ee97716cdc08d3848a.png)

注意：transaction_isolation是在MySQL 5.7.20的版本中引入来替换tx_isolation的，如果你使用的是之前版本的MySQL，请将上述用到系统变量transaction_isolation的地方替换为tx_isolation。

### 1.4.6.MySQL事务

#### 1.4.6.1.事务基本语法

**事务开始**

1、begin

2、START TRANSACTION（推荐）

3、begin work

**事务回滚**

rollback

**事务提交**

commit

使用事务插入两行数据，commit后数据还在

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/874c5a5d37c44347827edc01c7646d58.png)

使用事务插入两行数据，rollback后数据没有了

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/80e27d57435b4034a20c3ea4566c7674.png)

#### 1.4.6.2.保存点

如果你开启了一个事务，执行了很多语句，忽然发现某条语句有点问题，你只好使用ROLLBACK语句来让数据库状态恢复到事务执行之前的样子，然后一切从头再来，但是可能根据业务和数据的变化，不需要全部回滚。所以MySQL里提出了一个保存点（英文：savepoint）的概念，就是在事务对应的数据库语句中打几个点，我们在调用ROLLBACK语句时可以指定会滚到哪个点，而不是回到最初的原点。定义保存点的语法如下：

SAVEPOINT 保存点名称;

当我们想回滚到某个保存点时，可以使用下边这个语句（下边语句中的单词WORK和SAVEPOINT是可有可无的）：

```
ROLLBACK TO [SAVEPOINT] 保存点名称;
```

不过如果ROLLBACK语句后边不跟随保存点名称的话，会直接回滚到事务执行之前的状态。

如果我们想删除某个保存点，可以使用这个语句：

```
RELEASE SAVEPOINT 保存点名称;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/3dd600ff2c384d5f8e348c8bc33a6c76.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2e56bef3f9954c3f943168d546ae662f.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/dbca0f38164045eda2543112de99d69b.png)

#### 1.4.6.3.隐式提交

当我们使用START TRANSACTION或者BEGIN语句开启了一个事务，或者把系统变量autocommit的值设置为OFF时，事务就不会进行自动提交，但是如果我们输入了某些语句之后就会悄悄的提交掉，就像我们输入了COMMIT语句了一样，这种因为某些特殊的语句而导致事务提交的情况称为隐式提交，这些会导致事务隐式提交的语句包括：

##### 1.4.6.3.1.执行DDL

定义或修改数据库对象的数据定义语言（Datadefinition language，缩写为：DDL）。

所谓的数据库对象，指的就是数据库、表、视图、存储过程等等这些东西。当我们使用CREATE、ALTER、DROP等语句去修改这些所谓的数据库对象时，就会隐式的提交前边语句所属于的事务，就像这样：

```
BEGIN;

SELECT ... # 事务中的一条语句

UPDATE ... # 事务中的一条语句

... # 事务中的其它语句

CREATE TABLE ...
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/34acaa6366574b638f74d96d65f76274.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/9a70501b6a0645f389deae88494426fa.png)

**此语句会隐式的提交前边语句所属于的事务**

##### 1.4.6.3.2.隐式使用或修改mysql数据库中的表

当我们使用ALTER USER、CREATE USER、DROP USER、GRANT、RENAME USER、REVOKE、SET PASSWORD等语句时也会隐式的提交前边语句所属于的事务。

##### 1.4.6.3.3.事务控制或关于锁定的语句

当我们在一个会话里，一个事务还没提交或者回滚时就又使用START TRANSACTION或者BEGIN语句开启了另一个事务时，会隐式的提交上一个事务，比如这样：

```
BEGIN;

SELECT ... # 事务中的一条语句

UPDATE ... # 事务中的一条语句

... # 事务中的其它语句

BEGIN; # 此语句会隐式的提交前边语句所属于的事务
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6aaf9a1f630c4210996782d1c6fa6a97.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/93a9ef0063704f31b47838b257fb6cf0.png)

或者当前的autocommit系统变量的值为OFF，我们手动把它调为ON时，也会隐式的提交前边语句所属的事务。

或者使用LOCK TABLES、UNLOCK TABLES等关于锁定的语句也会隐式的提交前边语句所属的事务。

##### 1.4.6.3.4.加载数据的语句

比如我们使用LOAD DATA语句来批量往数据库中导入数据时，也会隐式的提交前边语句所属的事务。

##### 1.4.6.3.5.关于MySQL复制的一些语句

使用START SLAVE、STOP SLAVE、RESET SLAVE、CHANGE MASTER TO等语句时也会隐式的提交前边语句所属的事务。

##### 1.4.6.3.6.其它的一些语句

使用ANALYZE TABLE、CACHE INDEX、CHECK TABLE、FLUSH、 LOAD INDEX INTO CACHE、OPTIMIZE TABLE、REPAIR TABLE、RESET等语句也会隐式的提交前边语句所属的事务。

## 1.5.	MVCC

全称Multi-Version Concurrency Control，即多版本并发控制，主要是为了提高数据库的并发性能。
同一行数据平时发生读写请求时，会上锁阻塞住。但MVCC用更好的方式去处理读—写请求，做到在发生读—写请求冲突时不用加锁。
这个读是指的快照读，而不是当前读，当前读是一种加锁操作，是悲观锁。
那它到底是怎么做到读—写不用加锁的，快照读和当前读是指什么？我们后面都会学到。

### 1.5.1.MVCC原理

#### 1.5.1.1.复习事务隔离级别

![image-20240129194617306](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129194617306.png)

MySQL在REPEATABLE READ隔离级别下，是可以很大程度避免幻读问题的发生的，MySQL是怎么做到的？

#### 1.5.1.2.版本链

**必须要知道的概念：**

MVCC:生成一个数据请求时间点的一致性数据快照（Snapshot)，并用这个快照来提供一定级别（语句级或事务级）的一致性读取（MVCC）Multi Version Concurrency Control

先参看官网三个关键隐藏字段：

Internally, `InnoDB` adds three fields to each row stored in the database:

- A 6-byte `DB_TRX_ID` field indicates the transaction identifier for the last transaction that inserted or updated the row. Also, a deletion is treated internally as an update where a special bit in the row is set to mark it as deleted.
- A 7-byte `DB_ROLL_PTR` field called the roll pointer. The roll pointer points to an undo log record written to the rollback segment. If the row was updated, the undo log record contains the information necessary to rebuild the content of the row before it was updated.
- A 6-byte `DB_ROW_ID` field contains a row ID that increases monotonically as new rows are inserted. If `InnoDB` generates a clustered index automatically, the index contains row ID values. Otherwise, the `DB_ROW_ID` column does not appear in any index.

ROW_ID 详见索引章节

DB_TRX_ID  6字节   插入或更行行的最后一个事务的事务ID 自动递增 （创建版本号）

DB_ROLL_PTR  7字节  指定当前数据的undo log记录，回滚指针 （修改和删除版本号）

**每个版本链针对的一条数据**

我们知道，对于使用InnoDB存储引擎的表来说，它的聚簇索引记录中都包含两个必要的隐藏列（row_id并不是必要的，我们创建的表中有主键或者非NULL的UNIQUE键时都不会包含row_id列）：
trx_id：每次一个事务对某条聚簇索引记录进行改动时，都会把该事务的事务id赋值给trx_id隐藏列。
roll_pointer：每次对某条聚簇索引记录进行改动时，都会把旧的版本写入到undo日志中，然后这个隐藏列就相当于一个指针，可以通过它来找到该记录修改前的信息。

（补充点：undo日志：为了实现事务的原子性，InnoDB存储引擎在实际进行增、删、改一条记录时，都需要先把对应的undo日志记下来。**一般每对一条记录做一次改动，就对应着一条undo日志**，但在某些更新记录的操作中，也可能会对应着2条undo日志。一个事务在执行过程中可能新增、删除、更新若干条记录，也就是说需要记录很多条对应的undo日志，这些undo日志会被从0开始编号，也就是说根据生成的顺序分别被称为第0号undo日志、第1号undo日志、...、第n号undo日志等，这个编号也被称之为undo no。）

为了说明这个问题，我们创建一个演示表

```sql
CREATE TABLE teacher (
    number INT,
    name VARCHAR(100),
    domain varchar(100),
    PRIMARY KEY (number)
) Engine=InnoDB CHARSET=utf8;
```

然后向这个表里插入一条数据：

```sql
INSERT INTO teacher VALUES(1, '天明', '高级架构师讲师');
```

假设插入该记录的事务id为60，

假设之后两个事务id分别为80、120的事务对这条记录进行UPDATE操作

每次对记录进行改动，都会记录一条undo日志，每条undo日志也都有一个roll_pointer属性（INSERT操作对应的undo日志没有该属性，因为该记录并没有更早的版本），可以将这些undo日志都连起来，串成一个链表

对该记录每次更新后，都会将旧值放到一条undo日志中，就算是该记录的一个旧版本，随着更新次数的增多，所有的版本都会被roll_pointer属性连接成一个链表，我们把这个链表称之为版本链，版本链的头节点就是当前记录最新的值。另外，每个版本中还包含生成该版本时对应的事务id。**于是可以利用这个记录的版本链来控制并发事务访问相同记录的行为，那么这种机制就被称之为多版本并发控制(Mulit-Version Concurrency Control MVCC)。**

-- 快照一
start transaction; 
select * from t1 where id = 1234; 
-- 快照二
	udpate t1 set a  = "x2" where id = 1234；
-- 快照一
	select * from t1 where id = 1234; 

​	第二次查询 会延用第一次的快照。

##### 具体快照如下：

![image-20240129203028296](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129203028296.png)

#### 1.5.1.3.ReadView


对于使用READ COMMITTED和REPEATABLE READ隔离级别的事务来说，都必须保证读到已经提交了的事务修改过的记录，也就是说假如另一个事务已经修改了记录但是尚未提交，是不能直接读取最新版本的记录的，核心问题就是：READ COMMITTED和REPEATABLE READ隔离级别在不可重复读和幻读上的区别是从哪里来的，其实结合前面的知识，这两种隔离级别关键**是需要判断一下版本链中的哪个版本是当前事务可见的**。
**为此，InnoDB提出了一个ReadView的概念（作用于SQL查询语句），**

这个ReadView中主要包含4个比较重要的内容：
**m_ids：**表示在生成ReadView时当前系统中活跃的读写事务的事务id列表。
**min_trx_id：**表示在生成ReadView时当前系统中活跃的读写事务中最小的事务id，也就是m_ids中的最小值。
**max_trx_id：**表示生成ReadView时系统中应该分配给下一个事务的id值。注意max_trx_id并不是m_ids中的最大值，事务id是递增分配的。比方说现在有id为1，2，3这三个事务，之后id为3的事务提交了。那么一个新的读事务在生成ReadView时，m_ids就包括1和2，min_trx_id的值就是1，max_trx_id的值就是4。
**creator_trx_id：**表示生成该ReadView的事务的事务id。

MVCC多版本控制关键在于：

### 判断某个版本的可见性

先要明白两个基本概念：

高低水位。

![image-20240129204512317](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129204512317.png)

然后基于源码判断规则：

![image-20240129204829822](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129204829822.png)

0,从数据最早版本开始判断（undo log）

1,数据版本的trx_id  = creator_trx_id ,本事务修改，可以访问

2,数据版本的trx_id  < 某RV的min_trx_id ,(未提交事务的最小ID) 说明这个事务修改生成的ReadView已经提交，可以访问

3,数据版本的trx_id  > 某RV的max_trx_id ,(下一个事务ID) 说明这个事务修改生成的ReadView是在本事务开启之后建立的，不能访问

4,数据版本的trx_id  在 min_trx_id 和 max_trx_id之间,看看是否在m_ids（活跃的事务）中，在不可访问，不在，可以访问

5，如果当前版本不可见，就找undo log 链中的下一个版本，继续上面的规则去判断知道出现结果。



#### 1.5.1.4.READ COMMITTED

##### 脏读问题的解决

READ COMMITTED隔离级别的事务在**每次查询开始时都会生成**一个独立的ReadView。

具体源码：innobase/handler/ha_inodb.cc  ha_innobase::external_lock函数 搜 isolation_level

```c++
//如果事务隔离级别为 TRX_ISO_READ_COMMITTED 或更低级别
} else if (trx->isolation_level <= TRX_ISO_READ_COMMITTED &&
           MVCC::is_view_active(trx->read_view)) {
  mutex_enter(&trx_sys->mutex);
    //每次执行事务都会重新开启和关闭一个ReadView
  trx_sys->mvcc->view_close(trx->read_view, true);
    
```

当然这一块   1. read-commited:在每次语句执行的过程中，都关闭read_view, 重新在row_search_for_mysql函数中创建当前的一份read_view。这样就会产生 不可重复读现象发生。

ha_ndbcluster.cc中 :external_lock(THD *thd, int lock_type)
也可git：https://github.com/mysql/mysql-server/blob/8.0/sql/locks/shared_spin_lock.cc

```c++
ha_ndbcluster.cc ：:external_lock( 

If(trx->isolation_lev <= TRX_ISO_READ_COMMITTED && trx -> global_read_view){

/ at low tran isolation lev we let each consistent read set its own snapshot/

read_view_close_for_mysql(trx);
```

在MySQL中，READ COMMITTED和REPEATABLE READ隔离级别的的一个非常大的区别就是它们生成ReadView的时机不同。
我们还是以表teacher 为例，假设现在表teacher 中只有一条由事务id为60的事务插入的一条记录，接下来看一下READ COMMITTED和REPEATABLE READ所谓的生成ReadView的时机不同到底不同在哪里。
READ COMMITTED —— 每次读取数据前都生成一个ReadView
比方说现在系统里有两个事务id分别为80、120的事务在执行：Transaction 80

```
UPDATE teacher  SET name = '诸葛' WHERE number = 1;
UPDATE teacher  SET name = '徐庶' WHERE number = 1;
...
```

此刻，表teacher 中number为1的记录得到的版本链表

假设现在有一个使用READ COMMITTED隔离级别的事务开始执行：

```
使用READ COMMITTED隔离级别的事务

BEGIN;
SELECE1：Transaction 80、120未提交

SELECT * FROM teacher WHERE number = 1; # 得到的列name的值为'天明'
```



这个第一次  SELECE的执行过程如下：
在执行SELECT语句时会先生成一个ReadView：

ReadView的m_ids列表的内容就是[80, 120]，min_trx_id为80，max_trx_id为121，creator_trx_id为0。

然后从版本链中挑选可见的记录，从图中可以看出，最新版本的列name的内容是'**诸葛**'，该版本的trx_id值为80，在m_ids列表内，所以不符合可见性要求（trx_id属性值在ReadView的min_trx_id和max_trx_id之间说明创建ReadView时生成该版本的事务还是活跃的，该版本不可以被访问；如果不在，说明创建ReadView时生成该版本的事务已经被提交，该版本可以被访问），根据roll_pointer跳到下一个版本。
下一个版本的列name的内容是'**徐庶**'，该版本的trx_id值也为80，也在m_ids列表内，所以也不符合要求，继续跳到下一个版本。
下一个版本的列name的内容是'**天明**'，该版本的trx_id值为60，小于ReadView中的min_trx_id值，所以这个版本是符合要求的，最后返回给用户的版本就是这条列name为'**天明**'的记录。

**所以有了这种机制，就不会发生脏读问题！因为会去判断活跃版本，必须是不在活跃版本的才能用，不可能读到没有 commit的记录。**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653285598056/dd356cf81ec14665b7f11c82ec6021e9.png)

##### 不可重复读问题

然后，我们把事务id为80的事务提交一下，然后再到事务id为120的事务中更新一下表teacher 中number为1的记录：

```
Transaction120

BEGIN;

更新了一些别的表的记录

UPDATE teacher  SET name = '徐庶' WHERE number = 1;
UPDATE teacher  SET name = '诸葛' WHERE number = 1;

```

此刻，表teacher 中number为1的记录的版本链

然后再到刚才使用READ COMMITTED隔离级别的事务中继续查找这个number为1的记录，如下：

使用READ COMMITTED隔离级别的事务

```
BEGIN;

SELECE1：Transaction 80、120均未提交

SELECT * FROM teacher WHERE number = 1; # 得到的列name的值为'天明'

SELECE2：Transaction 80提交，Transaction 120未提交

SELECT * FROM teacher WHERE number = 1; # 得到的列name的值为'连'

```

第2次select的时间点



这个SELECE2的执行过程如下：

SELECT * FROM teacher WHERE number = 1;

在执行SELECT语句时会又会单独生成一个ReadView，该ReadView信息如下：

m_ids列表的内容就是[120]（事务id为80的那个事务已经提交了，所以再次生成快照时就没有它了），min_trx_id为120，max_trx_id为121，creator_trx_id为0。
然后从版本链中挑选可见的记录，从图中可以看出，最新版本的列name的内容是'**徐庶**'，该版本的trx_id值为120，在m_ids列表内，所以不符合可见性要求，根据roll_pointer跳到下一个版本。
下一个版本的列name的内容是'诸葛'，该版本的trx_id值为120，也在m_ids列表内，所以也不符合要求，继续跳到下一个版本。
下一个版本的列name的内容是'**徐庶**'，该版本的trx_id值为80，小于ReadView中的min_trx_id值120，所以这个版本是符合要求的，最后返回给用户的版本就是这条列name为'**徐庶**'的记录。

以此类推，如果之后事务id为120的记录也提交了，再次在使用READ COMMITTED隔离级别的事务中查询表teacher 中number值为1的记录时，得到的结果就是'**徐庶**'了，具体流程我们就不分析了。




##### 但会出现不可重复读问题。

明显上面一个事务中两次

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653285598056/b1232c1150a646eda0637a914716e0fc.png)


#### 1.5.1.5.REPEATABLE READ

##### REPEATABLE READ解决不可重复读问题

REPEATABLE READ —— 在**第一次读取数据时生成**一个全局的ReadView

对于使用REPEATABLE READ隔离级别的事务来说，只会在第一次执行查询语句时生成一个ReadView，之后的查询就不会重复生成了。我们还是用例子看一下是什么效果。

比方说现在系统里有两个事务id分别为80、120的事务在执行：Transaction 80

```
UPDATE teacher  SET name = '马' WHERE number = 1;
UPDATE teacher  SET name = '连' WHERE number = 1;
...
```

此刻，表teacher 中number为1的记录得到的版本链表如下

假设现在有一个使用REPEATABLE READ隔离级别的事务开始执行：

```
使用READ COMMITTED隔离级别的事务

BEGIN;
SELECE1：Transaction 80、120未提交

SELECT * FROM teacher WHERE number = 1; # 得到的列name的值为'天明'
```

这个SELECE1的执行过程如下：
在执行SELECT语句时会先生成一个ReadView：

ReadView的m_ids列表的内容就是[80, 120]，min_trx_id为80，max_trx_id为121，creator_trx_id为0。

然后从版本链中挑选可见的记录，从图中可以看出，最新版本的列name的内容是'**连**'，该版本的trx_id值为80，在m_ids列表内，所以不符合可见性要求（trx_id属性值在ReadView的min_trx_id和max_trx_id之间说明创建ReadView时生成该版本的事务还是活跃的，该版本不可以被访问；如果不在，说明创建ReadView时生成该版本的事务已经被提交，该版本可以被访问），根据roll_pointer跳到下一个版本。
下一个版本的列name的内容是'**诸葛**'，该版本的trx_id值也为80，也在m_ids列表内，所以也不符合要求，继续跳到下一个版本。
下一个版本的列name的内容是'**天明**'，该版本的trx_id值为60，小于ReadView中的min_trx_id值，所以这个版本是符合要求的，最后返回给用户的版本就是这条列name为'**天明**'的记录。
之后，我们把事务id为80的事务提交一下，然后再到事务id为120的事务中更新一下表teacher 中number为1的记录：

```
Transaction120

BEGIN;

更新了一些别的表的记录

UPDATE teacher  SET name = '诸葛' WHERE number = 1;
UPDATE teacher  SET name = '天明' WHERE number = 1;

```

此刻，表teacher 中number为1的记录的版本链

然后再到刚才使用REPEATABLE READ隔离级别的事务中继续查找这个number为1的记录，如下：

使用READ COMMITTED隔离级别的事务

```
BEGIN;

SELECE1：Transaction 80、120均未提交

SELECT * FROM teacher WHERE number = 1; # 得到的列name的值为'天明'

SELECE2：Transaction 80提交，Transaction 120未提交

SELECT * FROM teacher WHERE number = 1; # 得到的列name的值为'天明'

```

这个SELECE2的执行过程如下：

因为当前事务的隔离级别为REPEATABLE READ，而之前在执行SELECE1时已经生成过ReadView了，所以此时直接复用之前的ReadView，之前的ReadView的m_ids列表的内容就是[80, 120]，min_trx_id为80，max_trx_id为121，creator_trx_id为0。

**根据前面的分析，返回的值还是'天明'。**

**也就是说两次SELECT查询得到的结果是重复的，记录的列name值都是'天明'，这就是可重复读的含义。**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/64659425cf56414fba3a80c42c0538b7.png)

**总结一下就是：**

**ReadView中的比较规则(前两条)**

1、如果被访问版本的trx_id属性值与ReadView中的creator_trx_id值相同，意味着当前事务在访问它自己修改过的记录，所以该版本可以被当前事务访问。

2、如果被访问版本的trx_id属性值小于ReadView中的min_trx_id值，表明生成该版本的事务在当前事务生成ReadView前已经提交，所以该版本可以被当前事务访问。

#### 1.5.1.6.MVCC下的幻读解决和幻读现象

前面我们已经知道了，REPEATABLE READ隔离级别下MVCC可以解决不可重复读问题，那么幻读呢？MVCC是怎么解决的？幻读是一个事务按照某个相同条件多次读取记录时，后读取时读到了之前没有读到的记录，而这个记录来自另一个事务添加的新记录。
我们可以想想，在REPEATABLE READ隔离级别下的事务T1先根据某个搜索条件读取到多条记录，然后事务T2插入一条符合相应搜索条件的记录并提交，然后事务T1再根据相同搜索条件执行查询。结果会是什么？按照**ReadView中的比较规则(后两条)：**
3、如果被访问版本的trx_id属性值大于或等于ReadView中的max_trx_id值，表明生成该版本的事务在当前事务生成ReadView后才开启，所以该版本不可以被当前事务访问。
4、如果被访问版本的trx_id属性值在ReadView的min_trx_id和max_trx_id之间(min_trx_id &#x3c; trx_id &#x3c; max_trx_id)，那就需要判断一下trx_id属性值是不是在m_ids列表中，如果在，说明创建ReadView时生成该版本的事务还是活跃的，该版本不可以被访问；如果不在，说明创建ReadView时生成该版本的事务已经被提交，该版本可以被访问。

不管事务T2比事务T1是否先开启，事务T1都是看不到T2的提交的。请自行按照上面介绍的版本链、ReadView以及判断可见性的规则来分析一下。
但是，在REPEATABLE READ隔离级别下InnoDB中的MVCC 可以很大程度地避免幻读现象，而不是完全禁止幻读。怎么回事呢？我们来看下面的情况：



我们首先在事务T1中：

```
select * from teacher where number = 30;
```

很明显，这个时候是找不到number = 30的记录的。
我们在事务T2中，执行：

```
insert into teacher values(30,'豹','数据湖');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f1935b415db04ac482e023c6406f8de3.png)

通过执行insert into teacher values(30,'豹','数据湖');，我们往表中插入了一条number = 30的记录。
此时回到事务T1，执行：

```
update teacher set domain='RocketMQ' where number=30;
select * from teacher where number = 30;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/7ca9e16a31d84d5ca72fdb236a95eb28.png)

嗯，怎么回事？事务T1很明显出现了幻读现象。
在REPEATABLE READ隔离级别下，T1第一次执行普通的SELECT 语句时生成了一个ReadView（但是版本链没有），之后T2向teacher 表中新插入一条记录并提交，然后T1也进行了一个update语句。
ReadView并不能阻止T1执行UPDATE 或者DELETE 语句来改动这个新插入的记录，但是这样一来，这条新记录的trx_id隐藏列的值就变成了T1的事务id。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653285598056/92d29ec669db40b1a07fb0b3cc8cb730.png)

之后T1再使用普通的SELECT 语句去查询这条记录时就可以看到这条记录了，也就可以把这条记录返回给客户端。因为这个特殊现象的存在，我们也可以认为MVCC 并不能完全禁止幻读（**就是第一次读如果是空的情况，且在自己事务中进行了该条数据的修改**）。

#### 1.5.1.7.MVCC小结

从上边的描述中我们可以看出来，所谓的MVCC（Multi-Version Concurrency Control ，多版本并发控制）指的就是在使用READ COMMITTD、REPEATABLE READ这两种隔离级别的事务在执行普通的SELECT操作时访问记录的版本链的过程，这样子可以使不同事务的读-写、写-读操作并发执行，从而提升系统性能。

READ COMMITTD、REPEATABLE READ这两个隔离级别的一个很大不同就是：

生成ReadView的时机不同，READ COMMITTD在每一次进行普通SELECT操作前都会生成一个ReadView，而REPEATABLE READ只在第一次进行普通SELECT操作前生成一个ReadView，之后的查询操作都重复使用这个ReadView就好了，从而基本上可以避免幻读现象（**就是第一次读如果ReadView是空的情况中的某些情况则避免不了**）。

总来来说判断readView可见性会有如下流程：

1,undo log的数据中包含的trx_id是否符合min_trx_id和max_trx_id之间

1.1 如果小于min_trx_id说明创建RV 之前 的时候这个trx_id就已经事务提交了,不活跃了，说明可以读。

1.2 如果大于max_trx_id说明这个版本是在创建RV 之后 产生的，不可读。因为创建RV时你这个版本还不存在。

1.3 如果是在这之间的再看步骤2

2,查看trx_id是否包含m_id之中：

2.1 包含说明创建RV的时候，还是活跃（没提交）事务。那么是不可见的，脏读；继续看步骤3

2.2 不包含说明创建RV之前这个事务已经被提交了，那么是可见的。

3,到了这里说明这条数据的变更版本在RV之内，则要查看creator_trx_id与trx_id是否一致:

3.1 一致说明就是当前事务创建的；允许使用；

3.2 否则说明是当前RV的其他事务操作的不能使用;



另外，所谓的MVCC只是在我们进行普通的SEELCT查询时才生效，截止到目前我们所见的所有SELECT语句都算是普通的查询，至于什么是个不普通的查询，后面马上就会讲到（锁定读）。



# 1.事务底层与高可用原理

**事务的基础知识**

**mysql的事务分为显式事务和隐式事务**

* **默认的事务是隐式事务**

* **显式事务由我们自己控制事务的开启，提交，回滚等操作**

  ```
  show variables like 'autocommit';
  ```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/303d192e0c2c42e9b61800ccce6610d5.png)

#### 事务基本语法

**事务开始**

1、begin

2、START TRANSACTION（推荐）

3、begin work

**事务回滚**

rollback

**事务提交**

commit

使用事务插入两行数据，commit后数据还在

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/874c5a5d37c44347827edc01c7646d58.png)

使用事务插入两行数据，rollback后数据没有了

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/80e27d57435b4034a20c3ea4566c7674.png)

## 1.1.redo日志

在事务的实现机制上，MySQL采用的是WAL（Write-ahead logging，预写式日志）机制来实现的。

就是所有的修改都先被写入到日志中，然后再被应用到系统中。通常包含redo和undo两部分信息。

redo log称为重做日志，每当有操作时，在数据变更之前将操作写入redo log，这样当发生掉电之类的情况时系统可以在重启后继续操作。

undo log称为撤销日志，当一些变更执行到一半无法完成时，可以根据撤销日志恢复到变更之间的状态。

MySQL中用redo log来在系统Crash重启之类的情况时修复数据（事务的持久性），而undo log来保证事务的原子性。

### 1.1.1.redo日志及作用

#### 1.1.1.1.redo日志

MySQL的数据目录（使用SHOW VARIABLES LIKE 'datadir'查看）下默认有两个名为ib_logfile0和ib_logfile1的文件，这个就是redo日志

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/f82aa1db359e4d0faf08161eeea1fffa.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/8a984cd488e44f048749014046b0c20b.png)

可以通过下边几个启动参数来调节：

innodb_log_group_home_dir，该参数指定了redo日志文件所在的目录，默认值就是当前的数据目录。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/bc6cf7b9dd3346818ed739692a4d6e2b.png)

innodb_log_file_size，该参数指定了每个redo日志文件的大小，默认值为48MB，

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/554f32b002714f0bb9b60ca09bb15eeb.png)

innodb_log_files_in_group，该参数指定redo日志文件的个数，默认值为2，最大值为100。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/c97da1149f4144c7a1cbbde522e32e00.png)

所以磁盘上的redo日志文件可以不只一个，而是以一个日志文件组的形式出现的。这些文件以ib_logfile[数字]（数字可以是0、1、2...）的形式进行命名。在将redo日志写入日志文件组时，是从ib_logfile0开始写，如果ib_logfile0写满了，就接着ib_logfile1写，同理，ib_logfile1写满了就去写ib_logfile2，依此类推。如果写到最后一个文件也慢了该咋办？那就重新转到ib_logfile0继续写（覆盖写）。

#### 1.1.1.2.redo日志的作用

在Buffer Pool的时候说过，在真正访问MySQL数据之前，需要把在磁盘上的页缓存到内存中的Buffer Pool之后才可以访问。如果我们只在内存的Buffer Pool中修改了页面，假设在事务提交后突然发生了某个故障，导致内存中的数据都失效了，那么这个已经提交了的事务对数据库中所做的更改也就跟着丢失了，这是我们所不能忍受的。那么如何保证这个持久性呢？一个很简单的做法就是在事务提交完成之前把该事务所修改的所有页面都刷新到磁盘，但是这个做法有以下问题：

* **刷新一个完整的数据页太浪费了**

有时候我们仅仅修改了某个页面中的一个字节，但是我们知道在InnoDB中是以页为单位来进行磁盘IO的，也就是说我们在该事务提交时不得不将一个完整的页面从内存中刷新到磁盘，我们又知道一个页面默认是16KB大小，只修改一个字节就要刷新16KB的数据到磁盘上显然是太浪费了。

* **随机IO刷起来比较慢**

一个事务可能包含很多语句，即使是一条语句也可能修改许多页面，该事务修改的这些页面可能并不相邻，这就意味着在将某个事务修改的Buffer Pool中的页面刷新到磁盘时，需要进行很多的随机IO，随机IO比顺序IO要慢，尤其对于传统的机械硬盘来说。

怎么办呢？我们只是想让已经提交了的事务对数据库中数据所做的修改永久生效，即使后来系统崩溃，在重启后也能把这种修改恢复出来。所以我们其实没有必要在每次事务提交时就把该事务在内存中修改过的全部页面刷新到磁盘，只需要把修改了哪些东西记录一下就好。

比方说某个事务将系统表空间中的第100号页面中偏移量为1000处的那个字节的值1改成2我们只需要记录一下：

将第0号表空间的100号页面的偏移量为1000处的值更新为2。

**以上述内容也被称之为重做日志，英文名为redo log，也可以称之为redo日志**。与在事务提交时将所有修改过的内存中的页面刷新到磁盘中相比，只将该事务执行过程中产生的redo日志刷新到磁盘的好处如下：

1、redo日志占用的空间非常小

存储表空间ID、页号、偏移量以及需要更新的值所需的存储空间是很小的。

2、redo日志是顺序写入磁盘的

在执行事务的过程中，每执行一条语句，就可能产生若干条redo日志，这些日志是按照产生的顺序写入磁盘的，也就是使用顺序IO。

### 1.1.2.redo日志格式

通过上边的内容我们知道，redo日志本质上只是记录了一下事务对数据库做了哪些修改。 InnoDB们针对事务对数据库的不同修改场景定义了多种类型的redo日志，但是绝大部分类型的redo日志都有下边这种通用的结构：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/5ce762d5da264c38b9b6d033dfbbeeb6.png)

各个部分的详细释义如下：

type：该条redo日志的类型，redo日志设计大约有53种不同的类型日志。

space ID：表空间ID。

page number：页号。

data：该条redo日志的具体内容。

#### 1.1.2.1.简单的redo日志类型

如果某张表没有主键，并且没有定义不允许存储NULL值的UNIQUE键，那么InnoDB会自动为表添加一个名为row_id的隐藏列作为主键。

为这个row_id隐藏列进行赋值的方式如下：

* 内存中维护一个全局变量，当向某个包含row_id隐藏列的表中插入一条记录时，就会把这个全局变量的值当做新记录的row_id的值，并且把这个全局变量+1；
* 每当这个全局变量的值为256的倍数时，就会将该变量的值刷新到系统表空间页号为7的页面中一个名为Max Row Id的属性中。此时需要把这次对这个页面的修改以redo日志的形式记录下来
* 当系统启动时，会将这个Max Row Id属性加载到内存中。

InnoDB把这种极其简单的redo日志称之为物理日志，并且根据在页面中写入数据的多少划分了几种不同的redo日志类型：

MLOG_1BYTE（type=1）
表示在页面的某个偏移量处写入1字节的redo日志类型。
MLOG_2BYTE（type=2）
表示在页面的某个偏移量处写入2字节的redo日志类型。
MLOG_4BYTE（type=4）
表示在页面的某个偏移量处写入4字节的redo日志类型。
MLOG_8BYTE（type=8）

表示在**页面的某个偏移量**处写入**8字节**的redo日志类型

我们上边提到的Max Row ID属性实际占用8个字节的存储空间，所以在修改页面中的该属性时，会记录一条类型为MLOG_8BYTE的redo日志，MLOG_8BYTE的redo日志结构如下所示：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/d5b1da4cbf9a4806bff7635cd7e71973.png)

**offset代表在页面中的偏移量。**

#### 1.1.2.2.复杂的redo日志类型

有时候执行一条语句会修改非常多的页面，包括系统数据页面和用户数据页面（用户数据指的就是聚簇索引和二级索引对应的B+树）。以一条INSERT语句为例，它除了要向B+树的页面中插入数据，也可能更新系统数据Max Row ID的值，不过对于我们用户来说，平时更关心的是语句对B+树所做更新：

表中包含多少个索引，一条INSERT语句就可能更新多少棵B+树。

针对某一棵B+树来说，既可能更新叶子节点页面，也可能更新非叶子节点页面，也可能创建新的页面（在该记录插入的叶子节点的剩余空间比较少，不足以存放该记录时，会进行页面的分裂，在非叶子节点页面中添加目录项记录）。

画一个复杂的redo日志的示意图就像是这样：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/63a1efee68da4bd8abcc70a4b40b59c2.png)

大家只要记住：redo日志会把事务在执行过程中对数据库所做的所有修改都记录下来，在之后系统崩溃重启后可以把事务所做的任何修改都恢复出来。

### 1.1.3.redo日志的写入过程

#### 1.1.3.1.redo log block和日志缓冲区

InnoDB为了更好的进行系统崩溃恢复，把生成的redo日志都放在了大小为512字节的块（block）中。

我们前边说过，为了解决磁盘速度过慢的问题而引入了Buffer Pool。同理，写入redo日志时也不能直接直接写到磁盘上，实际上在服务器启动时就向操作系统申请了一大片称之为redo log buffer的连续内存空间，翻译成中文就是redo日志缓冲区（内存），我们也可以简称为log buffer。这片内存空间被划分成若干个连续的redo log block，我们可以通过启动参数innodb_log_buffer_size来指定log buffer的大小，该启动参数的默认值为16MB。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/84ed3384e9534081a6cf041109478040.png)

#### 1.1.3.2.redo日志刷盘时机

可是这些日志总在内存里呆着也不是个办法，在一些情况下它们会被刷新到磁盘里，比如：

一、事务提交时，为了保证持久性，必须要把修改这些页面对应的redo日志刷新到磁盘。

不过这里有一个参数 innodb_flush_log_at_trx_commit 可以控制：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/74f79bc7d4d44a7bbe6a6fdc43a40013.png)

该变量有3个可选的值：

**0：**当该系统变量值为0时，表示在事务提交时不立即向磁盘中同步redo日志，这个任务是交给后台线程做的。

这样很明显会加快请求处理速度，但是如果事务提交后服务器挂了，后台线程没有及时将redo日志刷新到磁盘，那么该事务对页面的修改会丢失。

**1：**当该系统变量值为1时，表示在事务提交时需要将redo日志同步到磁盘，可以保证事务的持久性。1也是innodb_flush_log_at_trx_commit的默认值。

**2：**当该系统变量值为2时，表示在事务提交时需要将redo日志写到操作系统的缓冲区中，但并不需要保证将日志真正的刷新到磁盘。

这种情况下如果数据库挂了，操作系统没挂的话，事务的持久性还是可以保证的，但是操作系统也挂了的话，那就不能保证持久性了。

二、InnoDB认为如果当前写入log buffer的redo日志量已经占满了log buffer总容量的大约一半左右，就需要把这些日志刷新到磁盘上。

三、后台有一个线程，大约每秒都会刷新一次log buffer中的redo日志到磁盘。

四、正常关闭服务器时等等。

### 1.1.4.崩溃后的恢复

#### 1.1.4.1.恢复机制

在服务器不挂的情况下，redo日志简直就是个大累赘，不仅没用，反而让性能变得更差。但是万一数据库挂了，就可以在重启时根据redo日志中的记录就可以将页面恢复到系统崩溃前的状态。

MySQL可以根据redo日志中的各种信息，来确定恢复的起点和终点。然后将redo日志中的数据，以哈希表的形式，将一个页面下的放到哈希表的一个槽中。之后就可以遍历哈希表，因为对同一个页面进行修改的redo日志都放在了一个槽里，所以可以一次性将一个页面修复好（避免了很多读取页面的随机IO）。并且通过各种机制，避免无谓的页面修复，比如已经刷新的页面，进而提升崩溃恢复的速度。

#### 1.1.4.2.崩溃后的恢复为什么不用binlog？

1、这两者使用方式不一样

binlog 会记录表所有更改操作，包括更新删除数据，更改表结构等等，主要用于人工恢复数据，而 redo log 对于我们是不可见的，它是 InnoDB 用于保证 crash-safe 能力的，也就是在事务提交后MySQL崩溃的话，可以保证事务的持久性，即事务提交后其更改是永久性的。

**一句话概括：binlog 是用作人工恢复数据，redo log 是 MySQL 自己使用，用于保证在数据库崩溃时的事务持久性。**

2、redo log 是 InnoDB 引擎特有的，binlog 是 MySQL 的 Server 层实现的,所有引擎都可以使用。

3、redo log是物理日志，记录的是“在某个数据页上做了什么修改”，恢复的速度更快；binlog是逻辑日志，记录的是这个语句的原始逻辑，比如“给ID=2这的c字段加1 ”；

4、redo log是“循环写”的日志文件，redo log 只会记录未刷盘的日志，已经刷入磁盘的数据都会从 redo log 这个有限大小的日志文件里删除。binlog 是追加日志，保存的是全量的日志。

5、最重要的是，当数据库crash 后，想要恢复未刷盘但已经写入 redo log 和 binlog 的数据到内存时，binlog 是无法恢复的。虽然 binlog 拥有全量的日志，但没有一个标志让 innoDB 判断哪些数据已经入表(写入磁盘)，哪些数据还没有。

**比如，binlog 记录了两条日志：**

记录1：给 ID=2 这一行的 c 字段加1

记录2：给 ID=2 这一行的 c 字段加1

在记录1入表后，记录2未入表时，数据库crash。重启后，只通过 binlog 数据库无法判断这两条记录哪条已经写入磁盘，哪条没有写入磁盘，不管是两条都恢复至内存，还是都不恢复，对 ID=2 这行数据来说，都不对。

但 redo log 不一样，只要刷入磁盘的数据，都会从 redo log 中抹掉，数据库重启后，直接把 redo log 中的数据都恢复至内存就可以了。

## 1.2.undo日志

### 1.2.1.事务回滚的需求

我们说过事务需要保证原子性，也就是事务中的操作要么全部完成，要么什么也不做。但是偏偏有时候事务执行到一半会出现一些情况，比如：

情况一：事务执行过程中可能遇到各种错误，比如服务器本身的错误，操作系统错误，甚至是突然断电导致的错误。

情况二：程序员可以在事务执行过程中手动输入ROLLBACK语句结束当前的事务的执行。

这两种情况都会导致事务执行到一半就结束，但是事务执行过程中可能已经修改了很多东西，为了保证事务的原子性，我们需要把东西改回原先的样子，这个过程就称之为回滚（英文名：rollback），这样就可以造成这个事务看起来什么都没做，所以符合原子性要求。

每当我们要对一条记录做改动时（这里的改动可以指INSERT、DELETE、UPDATE），都需要把回滚时所需的东西都给记下来。比方说：

你插入一条记录时，至少要把这条记录的主键值记下来，之后回滚的时候只需要把这个主键值对应的记录删掉。

你删除了一条记录，至少要把这条记录中的内容都记下来，这样之后回滚时再把由这些内容组成的记录插入到表中。

你修改了一条记录，至少要把修改这条记录前的旧值都记录下来，这样之后回滚时再把这条记录更新为旧值。

这些为了回滚而记录的这些东西称之为撤销日志，英文名为undo log/undo日志。这里需要注意的一点是，由于查询操作（SELECT）并不会修改任何用户记录，所以在查询操作执行时，并不需要记录相应的undo日志。

当然，在真实的InnoDB中，undo日志其实并不像我们上边所说的那么简单，不同类型的操作产生的undo日志的格式也是不同的。

### 1.2.2.事务id

#### 1.2.2.1.给事务分配id的时机

**读写事务：**

我们可以通过STARTTRANSACTION READ WRITE语句开启一个读写事务，或者使用BEGIN、START TRANSACTION语句开启的事务默认也算是读写事务。

在读写事务中可以对表执行增删改查操作。

如果某个事务执行过程中对某个表执行了增、删、改操作，那么InnoDB存储引擎就会给它分配一个独一无二的事务id，分配方式如下：

对于读写事务来说，只有在它第一次对某个表（包括用户创建的临时表）执行增、删、改操作时才会为这个事务分配一个事务id，否则的话也是不分配事务id的。

有的时候虽然我们开启了一个读写事务，但是在这个事务中全是查询语句，并没有执行增、删、改的语句，那也就意味着这个事务并不会被分配一个事务id。

**上边描述的事务id分配策略是针对MySQL5.7来说的，前边的版本的分配方式可能不同**。

#### 1.2.2.2.事务id生成机制

这个事务id本质上就是一个数字，它的分配策略和我们前边提到的对隐藏列row_id（当用户没有为表创建主键和UNIQUE键时InnoDB自动创建的列）的分配策略大抵相同，具体策略如下：

服务器会在内存中维护一个全局变量，每当需要为某个事务分配一个事务id时，就会把该变量的值当作事务id分配给该事务，并且把该变量自增1。

每当这个变量的值为256的倍数时，就会将该变量的值刷新到系统表空间的页号为5的页面中一个称之为Max Trx ID的属性处，这个属性占用8个字节的存储空间。

当系统下一次重新启动时，会将上边提到的Max Trx ID属性加载到内存中，将该值加上256之后赋值给我们前边提到的全局变量（因为在上次关机时该全局变量的值可能大于Max Trx ID属性值）。

这样就可以保证整个系统中分配的事务id值是一个递增的数字。先被分配id的事务得到的是较小的事务id，后被分配id的事务得到的是较大的事务id。

### 1.2.3.trx_id隐藏列

我们在学习InnoDB记录行格式的时候重点强调过：聚簇索引的记录除了会保存完整的用户数据以外，而且还会自动添加名为trx_id、roll_pointer的隐藏列，如果用户没有在表中定义主键以及UNIQUE键，还会自动添加一个名为row_id的隐藏列。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/a2c9b53565784e26994c2c240646644a.png)

其中的trx_id列就是某个对这个聚簇索引记录做改动的语句所在的事务对应的事务id而已（此处的改动可以是INSERT、DELETE、UPDATE操作）。至于roll_pointer隐藏列我们后边分析。

### 1.2.4.undo日志的格式

为了实现事务的原子性，InnoDB存储引擎在实际进行增、删、改一条记录时，都需要先把对应的undo日志记下来。一般每对一条记录做一次改动，就对应着一条undo日志，但在某些更新记录的操作中，也可能会对应着2条undo日志。

一个事务在执行过程中可能新增、删除、更新若干条记录，也就是说需要记录很多条对应的undo日志，这些undo日志会被从0开始编号，也就是说根据生成的顺序分别被称为第0号undo日志、第1号undo日志、...、第n号undo日志等，这个编号也被称之为undo no。

这些undo日志是被记录到类型为FIL_PAGE_UNDO_LOG的页面中。这些页面可以从系统表空间中分配，也可以从一种专门存放undo日志的表空间，也就是所谓的undo tablespace中分配。先来看看不同操作都会产生什么样子的undo日志。

#### 1.2.4.1.INSERT操作对应的undo日志

当我们向表中插入一条记录时最终导致的结果就是这条记录被放到了一个数据页中。如果希望回滚这个插入操作，那么把这条记录删除就好了，也就是说在写对应的undo日志时，主要是把这条记录的主键信息记上。InnoDB的设计了一个类型为TRX_UNDO_INSERT_REC的undo日志。

我们知道，对于使用InnoDB存储引擎的表来说，它的聚簇索引记录中都包含两个必要的隐藏列（row_id并不是必要的，我们创建的表中有主键或者非NULL的UNIQUE键时都不会包含row_id列）：
trx_id：每次一个事务对某条聚簇索引记录进行改动时，都会把该事务的事务id赋值给trx_id隐藏列。
roll_pointer：每次对某条聚簇索引记录进行改动时，都会把旧的版本写入到undo日志中，然后这个隐藏列就相当于一个指针，可以通过它来找到该记录修改前的信息。

（补充点：undo日志：为了实现事务的原子性，InnoDB存储引擎在实际进行增、删、改一条记录时，都需要先把对应的undo日志记下来。**一般每对一条记录做一次改动，就对应着一条undo日志**，但在某些更新记录的操作中，也可能会对应着2条undo日志。一个事务在执行过程中可能新增、删除、更新若干条记录，也就是说需要记录很多条对应的undo日志，这些undo日志会被从0开始编号，也就是说根据生成的顺序分别被称为第0号undo日志、第1号undo日志、...、第n号undo日志等，这个编号也被称之为undo no。）

为了说明这个问题，我们创建一个演示表

```
CREATE TABLE teacher (
number INT,
name VARCHAR(100),
domain varchar(100),
PRIMARY KEY (number)
) Engine=InnoDB CHARSET=utf8;
```

然后向这个表里插入一条数据：

```
INSERT INTO teacher VALUES(1, '天明', 'JVM系列');
```

现在表里的数据就是这样的：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/2ab2e19d985e462e87c1b6e7c50ebc5a.png)

假设插入该记录的事务id为60，那么此刻该条记录的示意图如下所示：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/c7b3d5e8c3bd4d91942b0891b0db0956.png)

如果记录中的主键只包含一个列，那么在类型为TRX_UNDO_INSERT_REC的undo日志中只需要把该列占用的存储空间大小和真实值记录下来，如果记录中的主键包含多个列，那么每个列占用的存储空间大小和对应的真实值都需要记录下来。

##### roll_pointer的作用

roll_pointer本质上就是一个指向记录对应的undo日志的一个指针。比方说我们向表里插入了2条记录，每条记录都有与其对应的一条undo日志。记录被存储到了类型为FIL_PAGE_INDEX的页面中（就是我们前边一直所说的数据页），undo日志被存放到了类型为FIL_PAGE_UNDO_LOG的页面中。roll_pointer本质就是一个指针，指向记录对应的undo日志。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/1a0260a4e2f54ce6990e045933654c3b.png)

#### 1.2.4.2.DELETE操作对应的undo日志

我们知道插入到页面中的记录会根据记录头信息中的next_record属性组成一个单向链表，我们把这个链表称之为正常记录链表；

往这张表中插入多条记录。每次对记录进行改动，都会记录一条undo日志，每条undo日志也都有一个roll_pointer属性（INSERT操作对应的undo日志没有该属性，因为该记录并没有更早的版本），可以将这些undo日志都连起来，串成一个链表，所以现在的情况就像下图一样：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/c7dc3b48519b4961b04e03594ee80538.png)

被删除的记录其实也会根据记录头信息中的next_record属性组成一个链表，只不过这个链表中的记录占用的存储空间可以被重新利用，所以也称这个链表为垃圾链表。Page Header部分有一个称之为PAGE_FREE的属性，它指向由被删除记录组成的垃圾链表中的头节点。

假设此刻某个页面中的记录分布情况是这样的

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/d652a46b9aa24c0ebdc207418c3bdf6e.png)

我们只把记录的delete_mask标志位展示了出来。从图中可以看出，正常记录链表中包含了3条正常记录，垃圾链表里包含了2条已删除记录。页面的Page Header部分的PAGE_FREE属性的值代表指向垃圾链表头节点的指针。

假设现在我们准备使用DELETE语句把正常记录链表中的最后一条记录给删除掉，其实这个删除的过程需要经历两个阶段：

阶段一：将记录的delete_mask标识位设置为1，这个阶段称之为delete mark。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/e82b8543820446a18e83237324567d21.png)

可以看到，正常记录链表中的最后一条记录的delete_mask值被设置为1，但是并没有被加入到垃圾链表。也就是此时记录处于一个中间状态。在删除语句所在的事务提交之前，被删除的记录一直都处于这种所谓的中间状态。

为啥会有这种奇怪的中间状态呢？其实主要是为了实现MVCC中的事务隔离级别。

阶段二：当该删除语句所在的事务提交之后，会有专门的线程后来真正的把记录删除掉。所谓真正的删除就是把该记录从正常记录链表中移除，并且加入到垃圾链表中，然后还要调整一些页面的其他信息，比如页面中的用户记录数量PAGE_N_RECS、上次插入记录的位置PAGE_LAST_INSERT、垃圾链表头节点的指针PAGE_FREE、页面中可重用的字节数量PAGE_GARBAGE、还有页目录的一些信息等等。这个阶段称之为purge。

把阶段二执行完了，这条记录就算是真正的被删除掉了。这条已删除记录占用的存储空间也可以被重新利用了。

从上边的描述中我们也可以看出来，在删除语句所在的事务提交之前，只会经历阶段一，也就是delete mark阶段（提交之后我们就不用回滚了，所以只需考虑对删除操作的阶段一做的影响进行回滚）。InnoDB中就会产生一种称之为TRX_UNDO_DEL_MARK_REC类型的undo日志。

##### 版本链

同时，在对一条记录进行delete mark操作前，需要把该记录的旧的trx_id和roll_pointer隐藏列的值都给记到对应的undo日志中来，就是我们图中显示的old trx_id和old roll_pointer属性。这样有一个好处，那就是可以通过undo日志的old roll_pointer找到记录在修改之前对应的undo日志。比方说在一个事务中，我们先插入了一条记录，然后又执行对该记录的删除操作，这个过程的示意图就是这样：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656301485030/da38fd7f58ca422c99254f42d42d63d4.png)

从图中可以看出来，执行完delete mark操作后，它对应的undo日志和INSERT操作对应的undo日志就串成了一个链表。这个链表就称之为版本链。

#### 1.2.4.3.UPDATE操作对应的undo日志

在执行UPDATE语句时，InnoDB对更新主键和不更新主键这两种情况有截然不同的处理方案。

##### 不更新主键的情况

在不更新主键的情况下，又可以细分为被更新的列占用的存储空间不发生变化和发生变化的情况。

###### 就地更新（in-place update）

更新记录时，对于被更新的每个列来说，如果更新后的列和更新前的列占用的存储空间都一样大，那么就可以进行就地更新，也就是直接在原记录的基础上修改对应列的值。再次强调一边，是每个列在更新前后占用的存储空间一样大，有任何一个被更新的列更新前比更新后占用的存储空间大，或者更新前比更新后占用的存储空间小都不能进行就地更新。

###### 先删除掉旧记录，再插入新记录

在不更新主键的情况下，如果有任何一个被更新的列更新前和更新后占用的存储空间大小不一致，那么就需要先把这条旧的记录从聚簇索引页面中删除掉，然后再根据更新后列的值创建一条新的记录插入到页面中。

请注意一下，我们这里所说的删除并不是delete mark操作，而是真正的删除掉，也就是把这条记录从正常记录链表中移除并加入到垃圾链表中，并且修改页面中相应的统计信息（比如PAGE_FREE、PAGE_GARBAGE等这些信息）。由用户线程同步执行真正的删除操作，真正删除之后紧接着就要根据各个列更新后的值创建的新记录插入。

这里如果新创建的记录占用的存储空间大小不超过旧记录占用的空间，那么可以直接重用被加入到垃圾链表中的旧记录所占用的存储空间，否则的话需要在页面中新申请一段空间以供新记录使用，如果本页面内已经没有可用的空间的话，那就需要进行页面分裂操作，然后再插入新记录。

**针对UPDATE不更新主键的情况（包括上边所说的就地更新和先删除旧记录再插入新记录），InnoDB设计了一种类型为TRX_UNDO_UPD_EXIST_REC的undo日志。**

##### 更新主键的情况

在聚簇索引中，记录是按照主键值的大小连成了一个单向链表的，如果我们更新了某条记录的主键值，意味着这条记录在聚簇索引中的位置将会发生改变，比如你将记录的主键值从1更新为10000，如果还有非常多的记录的主键值分布在1 ~ 10000之间的话，那么这两条记录在聚簇索引中就有可能离得非常远，甚至中间隔了好多个页面。针对UPDATE语句中更新了记录主键值的这种情况，InnoDB在聚簇索引中分了两步处理：

###### 将旧记录进行delete mark操作

也就是说在UPDATE语句所在的事务提交前，对旧记录只做一个delete mark操作，在事务提交后才由专门的线程做purge操作，把它加入到垃圾链表中。这里一定要和我们上边所说的在不更新记录主键值时，先真正删除旧记录，再插入新记录的方式区分开！

之所以只对旧记录做delete mark操作，是因为别的事务同时也可能访问这条记录，如果把它真正的删除加入到垃圾链表后，别的事务就访问不到了。这个功能就是所谓的MVCC。

###### 创建一条新记录

根据更新后各列的值创建一条新记录，并将其插入到聚簇索引中（需重新定位插入的位置）。

由于更新后的记录主键值发生了改变，所以需要重新从聚簇索引中定位这条记录所在的位置，然后把它插进去。

**针对UPDATE语句更新记录主键值的这种情况：**

**在对该记录进行delete mark操作前，会记录一条类型为TRX_UNDO_DEL_MARK_REC的undo日志；**

**之后插入新记录时，会记录一条类型为TRX_UNDO_INSERT_REC的undo日志，也就是说每对一条记录的主键值做改动时，会记录2条undo日志**。****



## 1.6.	MySQL中的锁

InnoDB中锁非常多，总的来说，可以如下分类：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653286288069/c4dad088c5534409930be499ded99b42.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653286288069/f72d5746a3464c3dae9e71b1d2b35ccc.png)

这些锁都是做什么的？具体含义是什么？我们现在来一一学习。

### 1.6.1.解决并发事务问题

我们已经知道事务并发执行时可能带来的各种问题，最大的一个难点是：一方面要最大程度地利用数据库的并发访问，另外一方面还要确保每个用户能以一致的方式读取和修改数据，尤其是一个事务进行读取操作，另一个同时进行改动操作的情况下。

### 1.6.2.并发事务问题

一个事务进行读取操作，另一个进行改动操作,我们前边说过，这种情况下可能发生脏读、不可重复读、幻读的问题。

怎么解决脏读、不可重复读、幻读这些问题呢？其实有两种可选的解决方案：

#### 1.6.2.1.方案一：读操作MVCC，写操作进行加锁

**事务利用MVCC进行的读取操作称之为一致性读，或者一致性无锁读，也称之为快照读**，但是往往读取的是历史版本数据。所有普通的SELECT语句（plain SELECT）在READ COMMITTED、REPEATABLE READ隔离级别下都算是一致性读。

一致性读并不会对表中的任何记录做加锁操作，其他事务可以自由的对表中的记录做改动。

很明显，采用MVCC方式的话，**读-写操作彼此并不冲突，性能更高**，**采用加锁方式的话，读-写操作彼此需要排队执行，影响性能**。一般情况下我们当然愿意采用MVCC来解决读-写操作并发执行的问题，但是业务在某些情况下，要求必须采用加锁的方式执行。

#### 1.6.2.2方案二：读、写操作都采用加锁的方式

**适用场景：**

业务场景不允许读取记录的旧版本，而是每次都必须去读取记录的最新版本，

比方在银行存款的事务中，你需要先把账户的余额读出来，然后将其加上本次存款的数额，最后再写到数据库中。在将账户余额读取出来后，就不想让别的事务再访问该余额，直到本次存款事务执行完成，其他事务才可以访问账户的余额。这样在读取记录的时候也就需要对其进行加锁操作，这样也就意味着读操作和写操作也像写-写操作那样排队执行。

**脏读**的产生是因为当前事务读取了另一个未提交事务写的一条记录，如果另一个事务在写记录的时候就给这条记录加锁，那么当前事务就无法继续读取该记录了，所以也就不会有脏读问题的产生了。

**不可重复读**的产生是因为当前事务先读取一条记录，另外一个事务对该记录做了改动之后并提交之后，当前事务再次读取时会获得不同的值，如果在当前事务读取记录时就给该记录加锁，那么另一个事务就无法修改该记录，自然也不会发生不可重复读了。

**幻读问题**的产生是因为当前事务读取了一个范围的记录，然后另外的事务向该范围内插入了新记录，当前事务再次读取该范围的记录时发现了新插入的新记录，我们把新插入的那些记录称之为幻影记录。采用加锁的方式解决幻读问题就有不太容易了，因为当前事务在第一次读取记录时那些幻影记录并不存在，所以读取的时候加锁就有点麻烦—— 因为并不知道给谁加锁。InnoDB中是如何解决的，我们后面会讲到。

### 1.6.3锁定读（LockingReads）/LBCC

也称当前读, 读取的是最新版本, 并且对读取的记录加锁, 阻塞其他事务同时改动相同记录，避免出现安全问题。

哪些是当前读呢？select lock in share mode (共享锁)、select for update (排他锁)、update (排他锁)、insert (排他锁/独占锁)、delete (排他锁)、串行化事务隔离级别都是当前读。

当前读这种实现方式，也可以称之为LBCC（基于锁的并发控制，Lock-Based Concurrency Control），怎么做到？

#### 1.6.3.1. 共享锁和独占锁

在使用加锁的方式解决问题时，由于既要允许读-读情况不受影响，又要使写-写、读-写或写-读情况中的操作相互阻塞，MySQL中的锁有好几类：

**共享锁**英文名：Shared Locks，简称S锁。在事务要读取一条记录时，需要先获取该记录的S锁。

假如事务E1首先获取了一条记录的S锁之后，事务E2接着也要访问这条记录：

如果事务E2想要再获取一个记录的S锁，那么事务E2也会获得该锁，也就意味着事务E1和E2在该记录上同时持有S锁。

**独占锁，**也常称**排他锁**，英文名：Exclusive Locks，简称X锁。在事务要改动一条记录时，需要先获取该记录的X锁。

如果事务E2想要再获取一个记录的X锁，那么此操作会被阻塞，直到事务E1提交之后将S锁释放掉。

如果事务E1首先获取了一条记录的X锁之后，那么不管事务E2接着想获取该记录的S锁还是X锁都会被阻塞，直到事务E1提交。

所以我们说S锁和S锁是兼容的，S锁和X锁是不兼容的，X锁和X锁也是不兼容的，画个表表示一下就是这样：

X    不兼容X      不兼容S

S    不兼容X      兼容S

#### 1.6.3.2.锁定读的SELECT语句

MySQ有两种比较特殊的SELECT语句格式：

```
SELECT * from test LOCK IN SHARE MODE;
```

一个事务中开启S锁

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/a2a38c121e4e44e6a2045fec1724254e.png)

另一个事务中开启S锁，可以读

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/b647ccce3edf4313b64b844139d7199d.png)

如果另外一个事务中开启X锁，阻塞！

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/02a271b4b3864be7a8a873888c11fc3d.png)

也就是在普通的SELECT语句后边加LOCK IN SHARE MODE，如果当前事务执行了该语句，那么它会为读取到的记录加S锁，这样允许别的事务继续获取这些记录的S锁（比方说别的事务也使用SELECT ... LOCK IN SHARE MODE语句来读取这些记录），但是不能获取这些记录的X锁（比方说使用SELECT ... FOR UPDATE语句来读取这些记录，或者直接修改这些记录）。

如果别的事务想要获取这些记录的X锁，那么它们会阻塞，直到当前事务提交之后将这些记录上的S锁释放掉。

对读取的记录加X锁：

```
SELECT * from test FOR UPDATE;
```

也就是在普通的SELECT语句后边加FOR UPDATE，如果当前事务执行了该语句，那么它会为读取到的记录加X锁，这样既不允许别的事务获取这些记录的S锁（比方说别的事务使用SELECT ... LOCK IN SHARE MODE语句来读取这些记录），也不允许获取这些记录的X锁（比如说使用SELECT ... FOR UPDATE语句来读取这些记录，或者直接修改这些记录）。

一个事务中开启X锁

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/28116a3e03264a399c6fa5eea78b8497.png)

另外一个事务中的X锁阻塞

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/644044fd54f746b29faa4f3580cce5e9.png)

除非第一个事务提交

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/6e1d9b6a68c749609dc88477960b6fcb.png)

另外一个事务才能获得X锁

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/49662552879242f4b8e34ee640700e93.png)

同样如果另外一个事务执行X锁，使用S锁也不行

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/27229c3d97f74246888b858f2d0c2e70.png)

如果别的事务想要获取这些记录的S锁或者X锁，那么它们会阻塞，直到当前事务提交之后将这些记录上的X锁释放掉。

#### 1.2.1.3. 写操作的锁

平常所用到的写操作无非是DELETE、UPDATE、INSERT这三种：

**DELETE：**

对一条记录做DELETE操作的过程其实是先在B+树中定位到这条记录的位置，然后获取一下这条记录的X锁，然后再执行delete mark操作。我们也可以把这个定位待删除记录在B+树中位置的过程看成是一个获取X锁的锁定读。

**INSERT：**

一般情况下，新插入一条记录的操作并不加锁，InnoDB通过一种称之为隐式锁来保护这条新插入的记录在本事务提交前不被别的事务访问。当然，在一些特殊情况下INSERT操作也是会获取锁的，具体情况我们后边再说。

**UPDATE：**

在对一条记录做UPDATE操作时分为三种情况：

1、如果未修改该记录的键值并且被更新的列占用的存储空间在**修改前后未发生变化**，则先在B+树中定位到这条记录的位置，然后再获取一下记录的X锁，最后在原记录的位置进行修改操作。其实我们也可以把这个定位待修改记录在B+树中位置的过程看成是一个**获取X锁的锁定读**。

2、如果未修改该记录的键值并且至少有一个被更新的列占用的存储空间在**修改前后发生变化**，则先在B+树中定位到这条记录的位置，然后获取一下记录的X锁，将该记录彻底删除掉（就是把记录彻底移入垃圾链表），最后再插入一条新记录。这个定位待修改记录在B+树中位置的过程看成是一个**获取X锁的锁定读**，新插入的记录由INSERT操作提供的**隐式锁进行保护**。

3、如果修改了该记录的键值，则相当于在原记录上做DELETE操作之后再来一次INSERT操作，加锁操作就需要按照DELETE和INSERT的规则进行了。

### 1.6.4锁的粒度

我们前边提到的锁都是针对记录的，也可以被称之为行级锁或者行锁，对一条记录加锁影响的也只是这条记录而已，我们就说这个锁的粒度比较细；其实一个事务也可以在表级别进行加锁，自然就被称之为表级锁或者表锁，对一个表加锁影响整个表中的记录，我们就说这个锁的粒度比较粗。给表加的锁也可以分为共享锁（S锁）和独占锁（X锁）

#### 1.6.4.1.表锁与行锁的比较

**锁定粒度：表锁 > 行锁**

**加锁效率：表锁 > 行锁**

**冲突概率：表锁 > 行锁**

**并发性能：表锁 &#x3c; 行锁**

#### 1.6.4.2.给表加S锁

**如果一个事务给表加了S锁，那么：**

别的事务可以继续获得该表的S锁

别的事务可以继续获得该表中的某些记录的S锁

别的事务不可以继续获得该表的X锁

别的事务不可以继续获得该表中的某些记录的X锁

#### 1.6.4.3.给表加X锁

**如果一个事务给表加了X锁（意味着该事务要独占这个表），那么：**

别的事务不可以继续获得该表的S锁

别的事务不可以继续获得该表中的某些记录的S锁

别的事务不可以继续获得该表的X锁

别的事务不可以继续获得该表中的某些记录的X锁。

为了更好的理解这个表级别的S锁和X锁和后面的意向锁，我们举一个现实生活中的例子。我们用曾经很火爆的互联网风口项目共享Office来说明加锁：

共享Office有栋大楼，楼自然有很多层。办公室都是共享的，客户可以随便选办公室办公。每层楼可以容纳客户同时办公，每当一个客户进去办公，就相当于在每层的入口处挂了一把S锁，如果很多客户进去办公，相当于每层的入口处挂了很多把S锁（类似行级别的S锁）。

有的时候楼层会进行检修，比方说换地板，换天花板，检查水电啥的，这些维修项目并不能同时开展。如果楼层针对某个项目进行检修，就不允许客户来办公，也不允许其他维修项目进行，此时相当于楼层门口会挂一把X锁（类似行级别的X锁）。

上边提到的这两种锁都是针对楼层而言的，不过有时候我们会有一些特殊的需求：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/021b5f9cea2e4bd4a06ec5cca86f440d.png)

A、有投资人要来考察Office的环境。

投资人和公司并不想影响客户进去办公，但是此时不能有楼层进行检修，所以可以在大楼门口放置一把S锁（类似表级别的S锁）。此时：

来办公的客户们看到大楼门口有S锁，可以继续进入大楼办公。

修理工看到大楼门口有S锁，则先在大楼门口等着，啥时候投资人走了，把大楼的S锁撤掉再进入大楼维修。

B、公司要和房东谈条件。

此时不允许大楼中有正在办公的楼层，也不允许对楼层进行维修。所以可以在大楼门口放置一把X锁（类似表级别的X锁）。此时：

来办公的客户们看到大楼门口有X锁，则需要在大楼门口等着，啥时候条件谈好，把大楼的X锁撤掉再进入大楼办公。

修理工看到大楼门口有X锁，则先在大楼门口等着，啥时候谈判结束，把大楼的X锁撤掉再进入大楼维修。

### 1.6.5.意向锁

但是在上面的例子这里头有两个问题：

如果我们想对大楼整体上S锁，首先需要确保大楼中的没有正在维修的楼层，如果有正在维修的楼层，需要等到维修结束才可以对大楼整体上S锁。

如果我们想对大楼整体上X锁，首先需要确保大楼中的没有办公的楼层以及正在维修的楼层，如果有办公的楼层或者正在维修的楼层，需要等到全部办公的同学都办公离开，以及维修工维修完楼层离开后才可以对大楼整体上X锁。

我们在对大楼整体上锁（表锁）时，怎么知道大楼中有没有楼层已经被上锁（行锁）了呢？依次检查每一楼层门口有没有上锁？那这效率也太慢了吧！于是InnoDB提出了一种意向锁（英文名：Intention Locks）：

简单来说**由于一个事务能成功对一张表加表锁的前提，是没有任何一个事务已经锁定这张表的任意一行**。

意向锁就是锁定了某一行则给表加意向锁，有了这个意向锁，我们再来做这个判断就不用去扫描全表扫描，只需要看下这个表级别的意向S和X就行了。是不是更高效了。你可以把它当做是一个标志。

**意向共享锁** ，英文名：Intention Shared Lock，简称IS锁。当事务准备在某条记录上加S锁时，需要先在表级别加一个IS锁。

**意向独占锁** ，英文名：Intention Exclusive Lock，简称IX锁。当事务准备在某条记录上加X锁时，需要先在表级别加一个IX锁。

视角回到大楼和楼层上来：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/524d4de2c0b94fe9a5daa7618b5d5fe1.png)

如果有客户到楼层中办公，那么他先在整栋大楼门口放一把IS锁（表级锁），然后再到楼层门口放一把S锁（行锁）。

如果有维修工到楼层中维修，那么它先在整栋大楼门口放一把IX锁（表级锁），然后再到楼层门口放一把X锁（行锁）。

之后：

如果有投资人要参观大楼，也就是想在大楼门口前放S锁（表锁）时，首先要看一下大楼门口有没有IX锁，如果有，意味着有楼层在维修，需要等到维修结束把IX锁撤掉后才可以在整栋大楼上加S锁。

如果有谈条件要占用大楼，也就是想在大楼门口前放X锁（表锁）时，首先要看一下大楼门口有没有IS锁或IX锁，如果有，意味着有楼层在办公或者维修，需要等到客户们办完公以及维修结束把IS锁和IX锁撤掉后才可以在整栋大楼上加X锁。

注意： 客户在大楼门口加IS锁时，是不关心大楼门口是否有IX锁的，维修工在大楼门口加IX锁时，是不关心大楼门口是否有IS锁或者其他IX锁的。IS和IX锁只是为了判断当前时间大楼里有没有被占用的楼层用的，也就是在对大楼加S锁或者X锁时才会用到。

**总结一下**：IS、IX锁是表级锁，它们的提出仅仅为了在之后加表级别的S锁和X锁时可以快速判断表中的记录是否被上锁，以避免用遍历的方式来查看表中有没有上锁的记录。就是说其实IS锁和IX锁是兼容的，IX锁和IX锁是兼容的。我们画个表来看一下**表级别**的各种锁的兼容性：

| 兼容性 | X      | IX     | S      | IS     |
| ------ | ------ | ------ | ------ | ------ |
| X      | 不兼容 | 不兼容 | 不兼容 | 不兼容 |
| IX     | 不兼容 |        | 不兼容 |        |
| S      | 不兼容 | 不兼容 |        |        |
| IS     | 不兼容 |        |        |        |

锁的组合性：（**意向锁没有行锁**）

| 组合性 | X    | IX   | S    | IS   |
| ------ | ---- | ---- | ---- | ---- |
| 表锁   | 有   | 有   | 有   | 有   |
| 行锁   | 有   |      | 有   |      |

#### 插入意向锁

也是一个 Gap Locks间隙锁，在对行记录的插入前加锁。插入意向锁主要是为了解决多个事务同时插入数据到相同的索引区间，当他们插入的是不同的位置，但是区间相同，则无需彼此等待

#### 自适应锁 Auto-inc locks  

看名字肯定自增ID相关 ，有没有发现过自增ID有时不连续，你可以设置自增ID的连贯性或者增长的效率。在Auto_increment列会产生。可以通过 innodb_autoinc_lock_mode设置

SHOW VARIABLES LIKE 'innodb_autoinc_lock_mode%';   

你可以去查询是什么？ 1 ？ 2  分别表示？  哪种更好？  当然默认是什么呢？（5.7>1  8>2）

0:所有insert语句开始就会拿到表级别的auto_inc锁，结束后释放。语句安全性强可以确保slave与master一致的id。影响并发的插入。每次都会产生表锁。

1:由于插入的个数可以提前得知，对插入做了优化获取批量的值，且不用保存到语句结束，只要语句得到相应的值就可提前释放锁.获取批量的锁，并提前释放。

2:由于现在mysql推荐把二进制的格式设置成row，所以再binlog_format不是statement的情况下最好是此处为2才能更好的性能。不会锁表，并发性能最好。

#### 空间索引的谓语锁（Predicate Locks for Spatial Indexs）

RR（Repeatable  /rɪˈpiːtəbl/ Read  RR 可重复读  ）级别或者Serializable下，next-key锁无法有效保证空间索引的正常，会产生此锁。

### 1.6.6.MySQL中的行锁和表锁

MySQL支持多种存储引擎，不同存储引擎对锁的支持也是不一样的。当然，我们重点还是讨论InnoDB存储引擎中的锁，其他的存储引擎只是稍微看看。

#### 1.6.6.1.其他存储引擎中的锁

对于MyISAM、MEMORY、MERGE这些存储引擎来说，它们只支持表级锁，而且这些引擎并不支持事务，所以使用这些存储引擎的锁一般都是针对当前会话来说的。比方说在Session 1中对一个表执行SELECT操作，就相当于为这个表加了一个表级别的S锁，如果在SELECT操作未完成时，Session 2中对这个表执行UPDATE操作，相当于要获取表的X锁，此操作会被阻塞，直到Session 1中的SELECT操作完成，释放掉表级别的S锁后，Session 2中对这个表执行UPDATE操作才能继续获取X锁，然后执行具体的更新语句。

因为使用MyISAM、MEMORY、MERGE这些存储引擎的表在同一时刻只允许一个会话对表进行写操作，所以这些存储引擎实际上最好用在只读，或者大部分都是读操作，或者单用户的情景下。
另外，在MyISAM存储引擎中有一个称之为Concurrent Inserts的特性，支持在对MyISAM表读取时同时插入记录，这样可以提升一些插入速度。关于更多Concurrent Inserts的细节，详情可以参考文档。

#### 1.6.6.2.InnoDB存储引擎中的锁

InnoDB存储引擎既支持表锁，也支持行锁。表锁实现简单，占用资源较少，不过粒度很粗，有时候你仅仅需要锁住几条记录，但使用表锁的话相当于为表中的所有记录都加锁，所以性能比较差。行锁粒度更细，可以实现更精准的并发控制。下边我们详细看一下。

##### 1.6.6.2.1.InnoDB中的表级锁

###### 1.6.6.2.1.1.表级别的S锁、X锁、元数据锁

在对某个表执行SELECT、INSERT、DELETE、UPDATE语句时，InnoDB存储引擎是不会为这个表添加表级别的S锁或者X锁的。

另外，在对某个表执行一些诸如ALTER TABLE、DROP TABLE这类的DDL语句时，其他事务对这个表并发执行诸如SELECT、INSERT、DELETE、UPDATE的语句会发生阻塞，同理，某个事务中对某个表执行SELECT、INSERT、DELETE、UPDATE语句时，在其他会话中对这个表执行DDL语句也会发生阻塞。这个过程其实是通过在server层使用一种称之为元数据锁（英文名：Metadata Locks，简称MDL）来实现的，一般情况下也不会使用InnoDB存储引擎自己提供的表级别的S锁和X锁。

其实这个InnoDB存储引擎提供的表级S锁或者X锁是相当鸡肋，只会在一些特殊情况下，比方说崩溃恢复过程中用到。不过我们还是可以手动获取一下的，比方说在系统变量autocommit=0，innodb_table_locks = 1时，手动获取InnoDB存储引擎提供的表t的S锁或者X锁可以这么写：

LOCK TABLES t
READ：InnoDB存储引擎会对表t加表级别的S锁。

LOCK TABLES t
WRITE：InnoDB存储引擎会对表t加表级别的X锁。

**请尽量避免在使用InnoDB存储引擎的表上使用LOCK TABLES这样的手动锁表语句，它们并不会提供什么额外的保护，只是会降低并发能力而已。**

###### 1.6.6.2.1.2.表级别的IS锁、IX锁

当我们在对使用InnoDB存储引擎的表的某些记录加S锁之前，那就需要先在表级别加一个IS锁，当我们在对使用InnoDB存储引擎的表的某些记录加X锁之前，那就需要先在表级别加一个IX锁。

IS锁和IX锁的使命只是为了后续在加表级别的S锁和X锁时判断表中是否有已经被加锁的记录，以避免用遍历的方式来查看表中有没有上锁的记录。我们并不能手动添加意向锁，只能由InnoDB存储引擎自行添加。

###### 1.6.6.2.1.3.表级别的AUTO-INC锁

在使用MySQL过程中，我们可以为表的某个列添加AUTO_INCREMENT属性，之后在插入记录时，可以不指定该列的值，系统会自动为它赋上递增的值系统实现这种自动给AUTO_INCREMENT修饰的列递增赋值的原理主要是两个：

1、采用AUTO-INC锁，也就是在执行插入语句时就在表级别加一个AUTO-INC锁，然后为每条待插入记录的AUTO_INCREMENT修饰的列分配递增的值，在该语句执行结束后，再把AUTO-INC锁释放掉。这样一个事务在持有AUTO-INC锁的过程中，其他事务的插入语句都要被阻塞，可以保证一个语句中分配的递增值是连续的。

如果我们的插入语句在执行前不可以确定具体要插入多少条记录（无法预计即将插入记录的数量），比方说使用INSERT ... SELECT、REPLACE ... SELECT或者LOAD DATA这种插入语句，一般是使用AUTO-INC锁为AUTO_INCREMENT修饰的列生成对应的值。

2、采用一个轻量级的锁，在为插入语句生成AUTO_INCREMENT修饰的列的值时获取一下这个轻量级锁，然后生成本次插入语句需要用到的AUTO_INCREMENT列的值之后，就把该轻量级锁释放掉，并不需要等到整个插入语句执行完才释放锁。

如果我们的插入语句在执行前就可以确定具体要插入多少条记录，比方说我们上边举的关于表t的例子中，在语句执行前就可以确定要插入2条记录，那么一般采用轻量级锁的方式对AUTO_INCREMENT修饰的列进行赋值。这种方式可以避免锁定表，可以提升插入性能。

InnoDB提供了一个称之为innodb_autoinc_lock_mode的系统变量来控制到底使用上述两种方式中的哪种来为AUTO_INCREMENT修饰的列进行赋值，当innodb_autoinc_lock_mode值为0时，一律采用AUTO-INC锁；当innodb_autoinc_lock_mode值为2时，一律采用轻量级锁；当innodb_autoinc_lock_mode值为1时，两种方式混着来（也就是在插入记录数量确定时采用轻量级锁，不确定时使用AUTO-INC锁）。

**不过当innodb_autoinc_lock_mode值为2时，可能会造成不同事务中的插入语句为AUTO_INCREMENT修饰的列生成的值是交叉的，在有主从复制的场景中是不安全的。**

```
show variables like 'innodb_autoinc_lock_mode' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653286288069/deb3ad3775c149f2943b98331cf9ed59.png)

MySQL5.7.X中缺省为1。

#### 1.6.7.2.InnoDB中的行级锁

行锁，也称为记录锁，顾名思义就是在记录上加的锁。但是要注意，这个记录指的是通过给索引上的索引项加锁。InnoDB 这种行锁实现特点意味着：**只有通过索引条件检索数据，InnoDB 才使用行级锁，否则，InnoDB 将使用表锁。**

不论是使用主键索引、唯一索引或普通索引，InnoDB都会使用行锁来对数据加锁。

只有执行计划真正使用了索引，才能使用行锁：**即便在条件中使用了索引字段，但是否使用索引来检索数据是由 MySQL 通过判断不同执行计划的代价来决定的，如果 MySQL认为全表扫描效率更高，比如对一些很小的表，它就不会使用索引，这种情况下 InnoDB** **将使用表锁，而不是行锁。**

同时当我们用范围条件而不是相等条件检索数据，并请求锁时，InnoDB会给符合条件的已有数据记录的索引项加锁。

不过即使是行锁，InnoDB里也是分成了各种类型的。换句话说即使对同一条记录加行锁，如果类型不同，起到的功效也是不同的。我们使用前面的teacher，增加一个索引，并插入几条记录。

```
INDEX  `idx_number`(`number`)
```



我们来看看都有哪些常用的行锁类型。

![image-20240130150959103](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240130150959103.png)

**Record Locks**

也叫记录锁，就是仅仅把一条记录锁上，官方的类型名称为：LOCK_REC_NOT_GAP。比方说我们把number值为6的那条记录加一个记录锁：

**条件等值匹配锁住   对应值的行**。

记录锁是有S锁和X锁之分的，当一个事务获取了一条记录的S型记录锁后，其他事务也可以继续获取该记录的S型记录锁，但不可以继续获取X型记录锁；当一个事务获取了一条记录的X型记录锁后，其他事务既不可以继续获取该记录的S型记录锁，也不可以继续获取X型记录锁；

**Gap Locks**

我们说MySQL在REPEATABLE READ隔离级别下是可以解决幻读问题的，解决方案有两种，可以使用MVCC方案解决，也可以采用加锁方案解决。但是在使用加锁方案解决时有问题，就是事务在第一次执行读取操作时，那些幻影记录尚不存在，我们无法给这些幻影记录加上记录锁。InnoDB提出了一种称之为Gap Locks的锁，官方的类型名称为：LOCK_GAP，我们也可以简称为gap锁。

**间隙锁实质上是对索引前后的间隙上锁，不对索引本身上锁。**

锁定当前没有命中 的区间。 比如上图中 查询 id=7时 锁住 (6,9)  (只有RR才存在)

会话1开启一个事务，执行

```
begin;
update teacher set domain ='JVM' where number='6';
```

会对2~6之间和6到10之间进行上锁。



如图中为2~6和  6  ~ 10的记录加了gap锁，意味着不允许别的事务在这条记录前后间隙插入新记录。

```
begin;
insert into teacher value(7,'天明','docker');
```

为什么不能插入？因为记录（7,'天明','docker'）要 插入的话，在索引idx_number上，刚好落在6  ~ 10之间，是有锁的，当然不允许插入。

但是当SQL语句变为：insert
into teacher value(70,'晁','docker');能插入吗？

当然能，因为70这条记录不在被锁的区间内。

**next-key Locks** 

record+gap 锁定一个范围，包含记录本身

锁住命中记录区间+下一个区间（左开右闭）

比如上图中：查询id >5  for update 会锁住   （3，+∞] 

直接查 id=1 for update 加Record Lock精确锁定这一行

查id = 5 for update 加 Gap 锁 锁定 (3,6)区间

查 id >4 and id<6 加 next-key 锁定 (3,6] 和 （6,9] 两个区间

查 id >2 and id<6 呢？ (1,3] 和(3,6]和 （6,9] 三个个区间

Gap锁设计的目的是为了阻止多个事务将记录插入到同一范围内，而这会导致幻读问题的产生，innodb对于行的查询使用next-key lock，Next-locking keying是Record lock和Gap lock的组合。当查询的索引含有唯一属性时，将next-key lock降级为record key。

有两种方式显式关闭gap锁 ，第一种. 将事务隔离级别设置为RC ；第二种. 将参数innodb_locks_unsafe_for_binlog设置为1。

**行锁测试代码**：

```sql
select * from transaction_locking -- 可见4条记录  1 3 6 9 
-- 测试Record锁   事务一

show variables like 'autocommit'; 
  set autocommit=0;   -- 默认自动提交   测试完最好改回去
select * from transaction_locking where a =1 for update;
-- 事务二 修改此行记录会等待锁
select * from transaction_locking where a =1 for update;
update transaction_locking set c='mi'  where a =1 ;

-- 测试 Gap锁  事务一  没有命中 则锁定 (4,6) 区间   阻塞插入的
select * from transaction_locking where a =4 for update;
-- 或者
select * from transaction_locking where a >3 and a<6  for update;
-- 事务二 想在此区间新增行 需等待锁
insert into transaction_locking values(4,3,4);

-- 测试 next-key 锁 事务一 (3,6] 和 (6,9]  如果 <6 的话不会锁住 (6,9)
select * from transaction_locking where a >3 and a<7  for update;
-- 事务二 修改此行记录会等待锁
select * from transaction_locking where a =1 for update;
update transaction_locking set c='mi'  where a =1 ;
```



### 1.6.7.死锁

#### 1.6.7.1.概念

是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁。

举个例子：A和B去按摩洗脚，都想在洗脚的时候，同时顺便做个头部按摩，13技师擅长足底按摩，14擅长头部按摩。

这个时候A先抢到14，B先抢到13，两个人都想同时洗脚和头部按摩，于是就互不相让，扬言我死也不让你，这样的话，A抢到14，想要13，B抢到13，想要14，在这个想同时洗脚和头部按摩的事情上A和B就产生了死锁。怎么解决这个问题呢？

第一种，假如这个时候，来了个15，刚好也是擅长头部按摩的，A又没有两个脑袋，自然就归了B，于是B就美滋滋的洗脚和做头部按摩，剩下A在旁边气鼓鼓的，这个时候死锁这种情况就被打破了，不存在了。

第二种，C出场了，用武力强迫A和B，必须先做洗脚，再头部按摩，这种情况下，A和B谁先抢到13，谁就可以进行下去，另外一个没抢到的，就等着，这种情况下，也不会产生死锁。

所以总结一下：

死锁是必然发生在多操作者（M>=2个）情况下，争夺多个资源（N>=2个，且N&#x3c;=M）才会发生这种情况。很明显，单线程自然不会有死锁，只有B一个去，不要2个，打十个都没问题；单资源呢？只有13，A和B也只会产生激烈竞争，打得不可开交，谁抢到就是谁的，但不会产生死锁。同时，死锁还有几个要求，1、争夺资源的顺序不对，如果争夺资源的顺序是一样的，也不会产生死锁；

2、争夺者拿到资源不放手。

#### 1.6.7.2.MySQL中的死锁

MySQL中的死锁的成因是一样的。

会话1：

```
begin;
select * from
teacher where number = 1 for update;
```

会话2：

```
begin;
select * from
teacher where number = 3 for update;
```

会话1

```
select * from teacher where number = 3 for
update;
```

**可以看到这个语句的执行将会被阻塞**

会话2 ：

```
select * from
teacher where number = 1 for update;
```

MySQL检测到了死锁，并结束了会话2中事务的执行，此时，切回会话1，发现原本阻塞的SQL语句执行完成了。

同时通过

```
show engine  innodb status\G
```

可以看见死锁的详细情况：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653286288069/8c39265a4c3c4205a40a6c815a73ffbc.png)

查看事务加锁的情况，不过一般情况下，看不到哪个事务对哪些记录加了那些锁，需要修改系统变量innodb_status_output_locks（MySQL5.6.16引入），缺省是OFF。

```
show
variables like 'innodb_status_output_locks';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653286288069/691dfae0b8554417b5e4b85c18767dfd.png)

我们需要设置为ON，

```
set global
innodb_status_output_locks = ON;
```

然后开启事务，并执行语句

## 1.7.	**MySQL8新特性**

对于 MySQL 5.7 版本，其将于 2023年 10月31日 停止支持。后续官方将不再进行后续的代码维护。

MySQL 8.0 全内存访问可以轻易跑到 200W QPS，I/O 极端高负载场景跑到 16W QPS，除此之外MySQL 8还新增了很多功能，那么我们来一起看一下。

### 1.7.1. 账户与安全

#### 1.7.1.1. 用户创建和授权

到了MySQL8中，用户创建与授权语句必须是分开执行，之前版本是可以一起执行。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/de3ffd4b519443439bdbd8c543c14a32.png)

**MySQL8的版本**

```
grant all privileges on *.* to 'lijin'@'%' identified by 'Lijin@2022';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/69ff061c543848569f28443f48fd3d2a.png)

```
create user 'lijin'@'%' identified by 'Lijin@2022';
grant all privileges on *.* to 'lijin'@'%'；
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/377e9651c03148b09f1255b47c4f2e19.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/b2a6e6d4d2f741838c8ca70c7da75693.png)

**MySQL5.7的版本**

```
grant all privileges on *.* to 'lijin'@'%' identified by 'Lijin@2022';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/cf816534a0734330acfc5d993b55310b.png)

#### 1.7.1.2. 认证插件更新

MySQL 8.0中默认的身份认证插件是caching_sha2_password，替代了之前的mysql_native_password。

```
show variables like 'default_authentication%';
```

**5.7版本**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/015cd62f5aa14b5887464c8562b5dd98.png)

**8版本**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/13929213dfb0439fa2373b969d19115d.png)

```
select user, host,plugin from mysql.user;
```

这个带来的问题就是如果客户端没有更新，就连接不上！！

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/662464a5e80a4fcb8ad498c5adcc7b80.png)

当然可以通过在MySQL的服务端找到my.cnf的文件，把相关参数进行修改（不过要MySQL重启后才能生效）

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/d8fc4c99b4d444ca8a2793f6f55cb6b8.png)

如果没办法重启服务，还有一种动态的方式：

```
alter user 'lijin'@'%' identified with mysql_native_password by 'Lijin@2022';
select host,user from mysql.user;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/4a96e29ae52f46d7815fc1af6fb2f151.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/1abfde3fba0a4945b526d51ba098bb26.png)

使用老的Navicat for MySQL也能访问

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/43c1bfc3251e4fa68354a57d9a15bd5e.png)

#### 1.7.1.3. 密码管理

MySQL 8.0开始允许限制重复使用以前的密码（修改密码时）。

并且还加入了密码的修改管理功能

```
show variables like 'password%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/06b3320142bd41459b9ace0126211d88.png)

修改策略（全局级）

```
set persist password_history=3;        --修改密码不能和最近3次一致
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/e85e65e80db64732b894b7a116401335.png)

修改策略（用户级）

```
alter user 'lijin'@'%' password history 3;
```

```
select user, host,Password_reuse_history from mysql.user;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/e7f298fd623a497b9b4af57d5afb0a2c.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/6e3f3b85114d492faa8eadaea67038f4.png)使用重复密码修改用户密码(指定lijin用户)

```
alter user 'lijin'@'%' identified by 'Lijin@2022';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/e7d506e7e3e044238354b7a1db369012.png)如果我们把全局的参数改为0，则对于root用户可以反复的修改密码

```
alter user 'root'@'localhost' identified by '789456';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/8eac02053e2f4e0e9686d997e2431c60.png)

password_reuse_interval   则是按照天数来限定（不允许重复的）

password_require_current    是否需要校验旧密码（off 不校验、 on校验）(针对非root用户)

```
set persist password_require_current=on;
```

### 1.7.2. 索引增强

#### 1.7.2.1. 隐藏索引

MySQL 8.0开始支持隐藏索引 (invisible index)，不可见索引.

隐藏索引不会被优化器使用，但仍然需要进行维护。
应用场景: 软删除、灰度发布。

软删除：就是我们在线上会经常删除和创建索引，如果是以前的版本，我们如果删除了索引，后面发现删错了，我又需要创建一个索引，这样做的话就非常影响性能。在MySQL8中我们可以这么操作，把一个索引变成隐藏索引（索引就不可用了，查询优化器也用不上），最后确定要进行删除这个索引我们才会进行删除索引操作。

灰度发布：也是类似的，我们想在线上进行一些测试，可以先创建一个隐藏索引，不会影响当前的生产环境，然后我们通过一些附加的测试，发现这个索引没问题，那么就直接把这个索引改成正式的索引，让线上环境生效。

**使用案例（灰度发布）：**

```
create table t1(i int,j int);  --创建一张t1表
create index i_idx on t1(i);  --创建一个正常索引
create index j_idx on t1(j) invisible;  --创建一个隐藏索引
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/c73a1f8ec0714350aa7ba3cca4b510ef.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/b0acbc1caa464f3082cc44f44838bee7.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/04da87a0e2ed4fb2bf8e2393b67a30f1.png)

```
show index from t1\G         --查看索引信息
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/11f5ca11849c4323be34c1f3713d9a2a.png)

使用查询优化器看下：

```
explain select * from t1 where i=1;
explain select * from t1 where j=1;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/168794969d3b42a2ad224643c6d1cfc7.png)

这里可以看到隐藏索引不会用上。

这里可以通过优化器的开关，打开一个设置，方便我们对隐藏索引进行设置。

```
select @@optimizer_switch\G;   --查看 各种参数
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/0ab72a3fea784b3397319fadde1293b0.png)

红色的部分就是默认查询优化器对隐藏索引不可见，我们可以通过参数进行修改。确保我们可以用隐藏索引进行测试。

```
set session optimizer_switch="use_invisible_indexes=on';   --在会话级别设置查询优化器可以看到隐藏索引
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/d4b7225269b64c728ed749f7b2f5d79b.png)

再使用查询优化器看下：

```
explain select * from t1 where j=1;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/dba6db5fe1e04e418fccd1f47718df9f.png)

把隐藏索引变成可见索引（正常索引）

```
alter table t1 alter index j_idx visible;   --变成可见
alter table t1 alter index j_idx invisible;   --变成不可见(隐藏索引)
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/e4735a743ec14fcba847a9fac18b0798.png)

**最后一点，不能把主键设置成不可见的索引（隐藏索引）（MySQL做了限制）**

#### 1.7.2.2. 降序索引

MySQL 8.0开始真正支持降序索引 (descendingindex) 。只有InnoDB存储引擎支持降序索引，只支持BTREE降序索引。另外MySQL8.0不再对GROUP BY操作进行隐式排序。

在MySQL中创建一个t2表

```
create table t2(c1 int,c2 int,index idx1(c1 asc,c2 desc));

show create table t2\G

```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/75d8a1f112174a0eae3bdcc329844c80.png)

如果是5.7中，则没有显示升序还是降序信息

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/44eda4306a624a77ae6f4c9bf3811143.png)

我们插入一些数据，给大家演示下降序索引的使用

```
insert into t2(c1,c2) values(1,100),(2,200),(3,150),(4,50);
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/6c688fd5a39342a08158c5cdecc8592b.png)

看下索引使用情况

```
explain select * from t2 order by c1,c2 desc;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/74a77cd932174740a18b3b6b28e19617.png)

我们在5.7对比一下

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/9dfcf7f4f605455b851f3ae64c5b2fa5.png)

这里说明，这里需要一个额外的排序操作，才能把刚才的索引利用上。

我们把查询语句换一下

```
explain select * from t2 order by c1 desc,c2 ;
```

MySQL8中使用了

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/00d9db6d7c71430a955e7107a0678461.png)

另外还有一点，就是group by语句在 8之后不再默认排序

```
select count(*),c2 from t2 group by c2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/e51a002e1f034c15bad26b7781532518.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/4bbbf1e99fa847479e232377e5d66a77.png)

在8要排序的话，就需要手动把排序语句加上

```
select count(*),c2 from t2 group by c2 order by c2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/23c4a24d51db40e4aaae81792d4b8a40.png)

#### 1.7.2.3. 函数索引

之前我们知道，如果在查询中加入了函数，索引不生效，所以MySQL8引入了函数索引。

MySQL 8.0.13开始支持在索引中使用函数（表达式)的值。支持降序索引，支持JSON 数据的索引
函数索引基于虚拟列功能实现。

**使用函数索引（表达式）**

```
create table t3(c1 varchar(10),c2 varchar(10));
create index idx_c1 on t3(c1);   --普通索引
create index func_idx on t3( (UPPER(c2)) );   --一个大写的函数索引

```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/47d2fd6adec142cf9dfde5c0cb677495.png)

```
show index from t3\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/d8508066bd504ba0897c5a2d25b85bf5.png)

```
explain select * from t3 where upper(c1)='ABC' ;  
explain select * from t3 where upper(c2)='ABC' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/7bfb171eb5c3483ba2d8ec79399c8261.png)

**使用函数索引（JSON）**

```
create table t4(data json，index((CAST(data->>'$.name' as char(25)) )));
explain select * from t4 where CAST(data->>'$.name' as char(25)) = 'lijin ';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/45a6485744a9438da17953c4df4d83fd.png)

**函数索引基于虚拟列功能实现**

函数索引在MySQL中相当于新增了一个列，这个列会根据你的函数来进行计算结果，然后使用函数索引的时候就会用这个计算后的列作为索引。

### 1.7.3. 通用表表达式（CTE）

MySQL8.0开始支持通用表表达式(CTE）(common table expression)，即WITH子句。

**简单入门：**

以下SQL就是一个简单的CTE表达式，类似于递归调用，这段SQL中，首先执行select 1 然后得到查询结果后把这个值n送入 union all下面的 select n+1 from cte where n &#x3c;10,然后一直这样递归调用union all下面sql语句。

```
WITH recursive cte(n) as 
( select 1
  union ALL
  select n+1 from cte where n<10
)
select * from cte;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/7f73594320584b3ca192eec1fdee9389.png)

**案例介绍：**

一个staff表，里面有id，有name还有一个 m_id，这个是对应的上级id。数据如下：



如果我们想查询出每一个员工的上下级关系，可以使用以下方式

递归CTE：

```
with recursive staff_view(id,name,m_id) as
(select id ,name ,cast(id as char(200)) 
 from staff where m_id =0
 union ALL 
 select s2.id ,s2.name,concat(s1.m_id,'-',s2.id)
 from staff_view as s1 join  staff as s2
 on s1.id = s2.m_id
)
select * from staff_view order by id
```



使用通用表表达式的好处就是上下级层级就算有4，5，6甚至更多层，都可以帮助我们遍历出来，而老的方式的写法SQL语句就要调整。

**总结：**

通用表表达式与派生表类似，就像语句级别的临时表或视图。CTE可以在查询中多次引用，可以引用其他CTE，可以递归。CTE支持SELECT/INSERT/UPDATE/DELETE等语句。

### 1.7.4. 窗口函数

MySQL 8.0支持窗口函数(Window Function)，也称分析函数。窗口函数与分组聚合函数类似，但是每一行数据都生成一个结果。聚合窗口函数: SUM /AVG / COUNT /MAX/MIN等等。

案例如下：sales表结构与数据如下：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/55a0f2e91f0b4ff99d807c997899bd85.png)

普通的分组、聚合（以国家统计）

```
SELECT country,sum(sum)
FROM sales
GROUP BY country
order BY country;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/2f621f4802de415aa8e41152f0e96e67.png)

窗口函数（以国家汇总）

```
select year,country,product,sum,
	sum(sum) over (PARTITION by country) as country_sum
 from sales
order by country,year,product,sum;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/119d39d7e7b4425bb79873cf1e532d30.png)

窗口函数（计算平局值）

```
select year,country,product,sum,
			sum(sum) over (PARTITION by country) as country_sum,
			avg(sum) over (PARTITION by country) as country_avg
 from sales
order by country,year,product,sum;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/b1efa7b8456e43949f4b46aec9b12a70.png)

专用窗口函数：

* 序号函数：ROW_NUMBER()、RANK()、DENSE_RANK()
* 分布函数：PERCENT_RANK()、CUME_DIST()
* 前后函数：LAG()、LEAD()
* 头尾函数：FIRST_VALUE()、LAST_VALUE()
* 其它函数：NTH_VALUE()、NTILE()

![](https://img-blog.csdnimg.cn/img_convert/81e045c22f5b474b17ba33c0c2250c49.png)

**窗口函数（排名）**

用于计算分类排名的排名窗口函数，以及获取指定位置数据的取值窗口函数

```
SELECT
	YEAR,
	country,
	product,
	sum,
	row_number() over (ORDER BY sum) AS 'rank',
        rank() over (ORDER BY sum) AS 'rank_1'
FROM
	sales;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/5cca667ce4344608a49ea780d7a69ba3.png)

```
SELECT
	YEAR,
	country,
	product,
	sum,
	sum(sum) over (PARTITION by country order by sum rows unbounded preceding) as sum_1
FROM
	sales order by country,sum;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/24c5c7cd8cf44dee84e869ee5dfaadc3.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/a96976f74acc4b3ab445bb22e6cdece7.png)

当然可以做的操作很多，具体见官网：

[https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html]()

### 1.7.5. 原子DDL操作

MySQL 8.0 开始支持原子 DDL 操作，其中与表相关的原子 DDL 只支持 InnoDB 存储引擎。一个原子 DDL 操作内容包括：更新数据字典，存储引擎层的操作，在 binlog 中记录 DDL 操作。支持与表相关的 DDL：数据库、表空间、表、索引的 CREATE、ALTER、DROP 以及 TRUNCATE TABLE。支持的其他 DDL ：存储程序、触发器、视图、UDF 的 CREATE、DROP 以及ALTER 语句。支持账户管理相关的 DDL：用户和角色的 CREATE、ALTER、DROP 以及适用的 RENAME，以及 GRANT 和 REVOKE 语句。

```
drop table t1,t2;   
```

上面这个语句，如果只有t1表，没有t2表。在MySQL5.7与8 的表现是不同的。

5.7会删除t1表。而在8中因为报错了，整个是一个原子操作，所以不会删除t1表。

### 1.7.6. JSON增强

具体看官网信息，英文好的直接看，英文不好的找个翻译工具即可看懂

[MySQL :: MySQL 8.0 Reference Manual :: 11.5 The JSON Data Type](https://dev.mysql.com/doc/refman/8.0/en/json.html)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/1d64831a19c4488089e934b96119686e.png)

### 1.7.7. InnoDB其他改进功能

**自增列持久化**

MySQL 5.7 以及早期版本，InnoDB 自增列计数器（AUTO_INCREMENT）的值只存储在内存中。MySQL 8.0 每次变化时将自增计数器的最大值写入 redo log，同时在每次检查点将其写入引擎私有的系统表。解决了长期以来的自增字段值可能重复的 bug。

**死锁检查控制**

MySQL 8.0 （MySQL 5.7.15）增加了一个新的动态变量，用于控制系统是否执行 InnoDB 死锁检查。对于高并发的系统，禁用死锁检查可能带来性能的提高。

```
innodb_deadlock_detect
```

**锁定语句选项**

SELECT ... FOR SHARE 和 SELECT ... FOR UPDATE 中支持 NOWAIT、SKIP LOCKED 选项。对于 NOWAIT，如果请求的行被其他事务锁定时，语句立即返回。对于 SKIP LOCKED，从返回的结果集中移除被锁定的行。

**InnoDB 其他改进功能。**

* 支持部分快速 DDL，ALTER TABLE ALGORITHM=INSTANT;
* InnoDB 临时表使用共享的临时表空间 ibtmp1。
* 新增静态变量 innodb_dedicated_server，自动配置 InnoDB 内存参数：innodb_buffer_pool_size/innodb_log_file_size 等。
* 默认创建 2 个 UNDO 表空间，不再使用系统表空间。
* 支持 ALTER TABLESPACE ... RENAME TO 重命名通用表空间。

# MySQL8新特性底层原理

## 降序索引

### 什么是降序索引

MySQL 8.0开始真正支持降序索引 (descendingindex) 。只有InnoDB存储引擎支持降序索引，只支持BTREE降序索引。另外MySQL8.0不再对GROUP BY操作进行隐式排序。

在MySQL中创建一个t2表

```
create table t2(c1 int,c2 int,index idx1(c1 asc,c2 desc));

show create table t2\G

```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/75d8a1f112174a0eae3bdcc329844c80.png)

如果是5.7中，则没有显示升序还是降序信息

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/44eda4306a624a77ae6f4c9bf3811143.png)

我们插入一些数据，给大家演示下降序索引的使用

```
insert into t2(c1,c2) values(1,100),(2,200),(3,150),(4,50);
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/6c688fd5a39342a08158c5cdecc8592b.png)

看下索引使用情况

```
explain select * from t2 order by c1,c2 desc;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/74a77cd932174740a18b3b6b28e19617.png)

我们在5.7对比一下

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/9dfcf7f4f605455b851f3ae64c5b2fa5.png)

这里说明，这里需要一个额外的排序操作，才能把刚才的索引利用上。

我们把查询语句换一下

```
explain select * from t2 order by c1 desc,c2 ;
```

MySQL8中使用了

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/00d9db6d7c71430a955e7107a0678461.png)

另外还有一点，就是group by语句在 8之后不再默认排序

```
select count(*),c2 from t2 group by c2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/e51a002e1f034c15bad26b7781532518.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/4bbbf1e99fa847479e232377e5d66a77.png)

在8要排序的话，就需要手动把排序语句加上

```
select count(*),c2 from t2 group by c2 order by c2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1653544165079/23c4a24d51db40e4aaae81792d4b8a40.png)

到此为止，大家应该对升序索引和降序索引有了一个大概的了解，但并没有真正理解，因为大家并不知道升序索引与降序索引底层到底是如何实现的。

### 降序索引的底层实现

升序索引对应的B+树

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656320896043/b595577948f94b2b84de3d79557eb9fc.png)

降序索引对应的B+树 

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656320896043/d9b945594d154f63b167b3c6c150a99b.png)

如果没有降序索引，查询的时候要实现降序的数据展示，那么就需要把原来默认是升序排序的数据处理一遍（比如利用压栈和出栈操作），而降序索引的话就不需要，所以在优化一些SQL的时候更加高效。

还有一点，现在 **只有Innodb存储引擎支持降序索引** 。

## Doublewrite Buffer的改进

**MySQL5.7**![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656320896043/d462b4c147bc41148f82bee5564c02b3.png)

**MySQL8.0**

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656320896043/2b08d8cf75e64ceb909b03ce818cb287.png)

在MySQL 8.0.20 版本之前，doublewrite 存储区位于系统表空间，从 8.0.20 版本开始，doublewrite 有自己独立的表空间文件，这种变更，能够降低doublewrite的写入延迟，增加吞吐量，为设置doublewrite文件的存放位置提供了更高的灵活性。

因为系统表空间在存储中就是一个文件，那么doublewrite必然会受制于这个文件的读写效率（其他向这个文件的读写操作，比如统计、监控等数据操作）

**系统表空间(system tablespace)**

这个所谓的系统表空间可以对应文件系统上一个或多个实际的文件，默认情况下，InnoDB会在数据目录下创建一个名为ibdata1(在你的数据目录下找找看有木有)、大小为12M的文件，这个文件就是对应的系纳表空间在文件系统上的表示。



而单独的文件必然效率比放在系统表空间效率要高！！！

**新增的参数：**

**innodb_doublewrite_dir**

指定doublewrite文件存放的目录，如果没有指定该参数，那么与innodb数据目录一致(innodb_data_home_dir)，如果这个参数也没有指定，那么默认放在数据目录下面(datadir)。

**innodb_doublewrite_files**

指定doublewrite文件数量，默认情况下，每个buffer pool实例，对应2个doublewrite文件。

**innodb_doublewrite_pages**

一次批量写入的doublewrite页数量的最大值，默认值、最小值与innodb_write_io_threads参数值相同，最大值512。

**innodb_doublewrite_batch_size**

一次批量写入的页数量。默认值为0，取值范围0到256。

## redo log 无锁优化

[MySQL :: MySQL 8.0: New Lock free, scalable WAL design



[](https://dev.mysql.com/blog-archive/mysql-8-0-new-lock-free-scalable-wal-design/)





# 1.MySQL体系架构

## 1.1.MySQL的分支与变种

MySQL变种有好几个，主要有三个久经考验的主流变种：Percona Server，MariaDB和 Drizzle。它们都有活跃的用户社区和一些商业支持，均由独立的服务供应商支持。同时还有几个优秀的开源关系数据库，值得我们了解一下。

### 1.1.1.Drizzle

Drizzle是真正的MySQL分支，而且是完全开源的产品，而非只是个变种或增强版本。它并不与MySQL兼容不能简单地将MySQL后端替换为Drizzle。

Drizzle与MySQL有很大差别，进行了一些重大更改，甚至SQL语法的变化都非常大，设计目标之一是提供一种出色的解决方案来解决高可用性问题。在实现上，Drizzle清除了一些表现不佳和不必要的功能，将很多代码重写，对它们进行了优化，甚至将所用语言从C换成了C++。

此外，Drizzle另一个设计目标是能很好的适应具有大量内容的多核服务器、运行Linux的64位机器、云计算中使用的服务器、托管网站的服务器和每分钟接收数以万计点击率的服务器并且大幅度的削减服务器成本。

### 1.1.2.MariaDB

在Sun收购MySQL后，Monty Widenius，这位MySQL的创建者，因不认同MySQL开发流程而离开Sun。他成立了Monty程序公司，创立了MariaDB。MariaDB的目标是社区开发，Bug修复和许多的新特性实际上，可以将MariaDB视为MySQL的扩展集，它不仅提供MySQL提供的所有功能，还提供其他功能。MariaDB是原版MySQL的超集，因此已有的系统不需要任何修改就可以运行。

诸如Google，Facebook、维基百科等公司或者网站所使用了MariaDB。不过Monty公司不是以赢利为目的，而是由产品驱动的，这可能会带来问题，因为没有赢利的公司不一定能长久维持下去。

### 1.1.3.Percona Server

由领先的MySQL咨询公司Percona发布，Percona公司的口号就是“The Database Performance Experts”，Percona的创始人也就是《高性能MySQL》书的作者。

Percona Server是个与MySQL向后兼容的替代品，它尽可能不改变SQL语法、客户端/服务器协议和磁盘上的文件格式。任何运行在MySQL上的都可以运行在Percona Server上而不需要修改。切换到Percona Server只需要关闭MySQL和启动PerconaServer，不需要导出和重新导入数据。

Percona Server有三个主要的目标：透明，增加允许用户更紧密地查看服务器内部信息和行为的方法。比如慢查询日志中特别增加的详细信息；性能，Percona Server包含许多性能和可扩展性方面的改进，还加强了性能的可预测性和稳定性。其中主要集中于InnoDB；操作灵活性，Percona Server使操作人员和系统管理员在让MySQL作为架构的一部分而可靠并稳定运行时提供了很多便利。

一般来说，Percona Server中的许多特性会在后来的标准MySQL中出现。

国内公司阿里内部就运行了上千个Percona Server的实例。

## 1.2.MySQL的替代

### 1.2.1.Postgre SQL

PostgreSQL称自己是世界上最先进的开源数据库，同时也是个一专多长的全栈数据库。最初是1985年在加利福尼亚大学伯克利分校开发的。

PostgreSQL 的稳定性极强，在崩溃、断电之类的灾难场景下依然可以保证数据的正确；在高并发读写，负载逼近极限下，PostgreSQL的性能指标仍可以维持双曲线甚至对数曲线，到顶峰之后不再下降，表现的非常稳定，而 MySQL 明显出现一个波峰后下滑；

PostgreSQL多年来在GIS(地理信息)领域处于优势地位，因为它有丰富的几何类型，实际上不止几何类型，PostgreSQL有大量字典、数组、bitmap 等数据类型，相比之下mysql就差很多。所以总的来说，PostgreSQL更学术化一些，在绝对需要可靠性和数据完整性的时候，PostgreSQL是更好的选择。但是从商业支持、文档资料、易用性，第三方支持来说，MySQL无疑更好些。

### 1.2.2.SQLite

SQLite是世界上部署最广泛的数据库引擎，为物联网（IoT）下的数据库首选，并且是手机，PDA，甚至MP3播放器的下的首选。SQLite代码占用空间小，并且不需要数据库管理员的维护。SQLite没有单独的服务器进程，提供的事务也基本符合ACID。当然，简单也就意味着功能和性能受限。

# 2.MySql基础

## 2.1.MySQL体系架构

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/7b5248b4b05242f3ac3950fa4ada202b.png)

可以看出MySQL是由**连接池、管理工具和服务、SQL接口、解析器、优化器、缓存、存储引擎、文件系统**组成。

**连接池**

由于每次建立建立需要消耗很多时间，连接池的作用就是将这些连接缓存下来，下次可以直接用已经建立好的连接，提升服务器性能。

**管理工具和服务**

系统管理和控制工具，例如备份恢复、Mysql复制、集群等

**SQL接口**

接受用户的SQL命令，并且返回用户需要查询的结果。比如select ... from就是调用SQL接口

**解析器**

SQL命令传递到解析器的时候会被解析器验证和解析。解析器主要功能：1、将SQL语句分解成数据结构，后续步骤的传递和处理就是基于这个结构的。2、将SQL语句分解成数据结构，后续步骤的传递和处理就是基于这个结构的。

**优化器**

查询优化器，SQL语句在查询之前会使用查询优化器对查询进行优化。

**缓存器**

查询缓存，如果查询缓存有命中的查询结果，查询语句就可以直接去查询缓存中取数据。这个缓存机制是由一系列小缓存组成的。比如表缓存，记录缓存，key缓存，权限缓存等。

**存储引擎(后面会细讲)**

**文件系统(后面会细讲)**

#### 查询语句流程图：

![image-20240127190737253](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240127190737253.png)





### 2.1.1.连接层

当MySQL启动（MySQL服务器就是一个进程），等待客户端连接，每一个客户端连接请求，服务器进程会创建一个线程专门处理与这个客户端的交互。当客户端与该服务器断开之后，不会立即撤销线程，只会把他缓存起来等待下一个客户端请求连接的时候，将其分配给该客户端。每个线程独立，拥有各自的内存处理空间。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/f7cab56271044db4be65a9ba436492c8.png)

以下命令可以查看最大的连接数：

```
show VARIABLES like '%max_connections%' 
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/eeb70573918e4e8594e07f3150572083.png)

### mysql客户端和服务器通讯

mysql单个客户端跟服务器的通讯在任何一个时刻，都是不能同时发生的，要么客户端向服务器发送数据，要么服务器向客户端发送数据！我们知道，当一个查询语句提交给服务器后，你是不能做其他事情的，只能等待结果，这也是为什么要进行sql语句优化，影响性能

### 连接状态查询

对于mysql的连接，任何时刻都会有一个状态，这个状态表示mysql当前正在做什么！！但是在查询的整个生命周期中，状态会发生变化，有以下这些状态

- sleep：线程正在等待客户端发送新的请求；
- query：线程正在执行查询或者正在将结果发送给客户端；
- locked：在mysql服务器层，该线程正在等待表锁。在存储引擎级别实现的锁，例如InnoDB的行锁，并不会体现在线程状态中。对于MyISAM来说这是一个比较典型的状态。
- analyzing and statistics：线程正在收集存储引擎的统计信息，并生成查询的执行计划；
- copying to tmp table：线程在执行查询，并且将其结果集复制到一个临时表中，这种状态一般要么是做group by操作，要么是文件排序操作，或者union操作。如果这个状态后面还有on
  disk标记，那表示mysql正在将一个内存临时表放到磁盘上。
- sorting Result：线程正在对结果集进行排序。
- sending data：线程可能在多个状态间传送数据，或者在生成结果集，或者在想客户端返回数据。

我们可以通过

```mysql
show full processlist
```

查询！

### 2.1.2.Server层(SQL处理层)

这一层主要功能有：SQL语句的解析、优化，缓存的查询，MySQL内置函数的实现，跨存储引擎功能（所谓跨存储引擎就是说每个引擎都需提供的功能（引擎需对外提供接口）），例如：存储过程、触发器、视图等。

当然作为一个SQL的执行流程如下：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/014fc8e5b6ad4a50aeaeb76d0b794a44.png)

1.如果是查询语句（select语句），首先会查询缓存是否已有相应结果，有则返回结果，无则进行下一步（如果不是查询语句，同样调到下一步）

2.解析查询，创建一个内部数据结构（解析树），这个解析树主要用来SQL语句的语义与语法解析；

3.优化：优化SQL语句，例如重写查询，决定表的读取顺序，以及选择需要的索引等。这一阶段用户是可以查询的，查询服务器优化器是如何进行优化的，便于用户重构查询和修改相关配置，达到最优化。这一阶段还涉及到存储引擎，优化器会询问存储引擎，比如某个操作的开销信息、是否对特定索引有查询优化等。

#### 缓存（已遗弃）

```
show variables like '%query_cache_type%'   -- 默认不开启

show variables like '%query_cache_size%'  --默认值1M

SET GLOBAL query_cache_type = 1; --会报错
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/cc55a235284845dc8436681dbdc6c590.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/c81fcfa504814ff09f92a4b588a215bd.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/511fee3bd5a648f790e9afd3475a311d.png)

query_cache_type只能配置在my.cnf文件中！

**缓存在生产环境建议不开启，除非经常有sql完全一模一样的查询**

**缓存****严格要求2****次SQL****请求要完全一样，包括SQL****语句，连接的数据库、协议版本、字符集等因素都会影响**

**从8.0开始，MySQL不再使用查询缓存，那么放弃它的原因是什么呢？**

MySQL查询缓存是查询结果缓存。它将以SEL开头的查询与哈希表进行比较，如果匹配，则返回上一次查询的结果。进行匹配时，查询必须逐字节匹配，例如 SELECT * FROM e1; 不等于select * from e1;

此外，一些不确定的查询结果无法被缓存，任何对表的修改都会导致这些表的所有缓存无效。因此，适用于查询缓存的最理想的方案是只读，特别是需要检查数百万行后仅返回数行的复杂查询。如果你的查询符合这样一个特点，开启查询缓存会提升你的查询性能。

随着技术的进步，经过时间的考验，MySQL的工程团队发现启用缓存的好处并不多。

首先，查询缓存的效果取决于缓存的命中率，只有命中缓存的查询效果才能有改善，因此无法预测其性能。

其次，查询缓存的另一个大问题是它受到单个互斥锁的保护。在具有多个内核的服务器上，大量查询会导致大量的互斥锁争用。

通过基准测试发现，大多数工作负载最好禁用查询缓存(5.6的默认设置)：按照官方所说的：造成的问题比它解决问题要多的多，弊大于利就直接砍掉了。

#### 词法解析

词法解析就是把一个完整的SQL语句打碎成一个个的单词。

#### 语法解析

进行语法解析，判断输入的这个 SQL 语句是否满足 MySQL 语法。然后生成下面这样一颗语法树：

![image-20240127193349345](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240127193349345.png)

### 预处理器

解析器不会去检查查询的表名、列名是否正确，是否有表的权限等，所以我们需要用到处理器去进行进一步检查解析树是否合法，它会检查生成的解析树，解决解析器无法解析的语义。比如，它会检查表和列名是否存在，检查名字和别名，保证没有歧义。

### 优化器

当上述步骤完成，则sql语句认为是合法并且是可执行的，并且可以有很多的执行方式，并且返回相同的结果，优化器会把一条sql语句转化成执行计划，并且找到其中最好的执行计划！

MySQL的优化器能处理哪些优化类型呢？

举两个简单的例子：

1、当我们对多张表进行关联查询的时候，以哪个表的数据作为基准表。

2、有多个索引可以使用的时候，选择哪个索引。

实际上，对于每一种数据库来说，优化器的模块都是必不可少的，他们通过复杂的算法实现尽可能优化查询效率的目标。

到此我们就得到了一个执行计划，是不是要交给执行器

### 执行器

利用存储引擎提供的相应的API来完成操作。并且把数据返回给客户端

### 2.1.3.存储引擎层

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/3f4669af24cd4fe29bf6319244573841.png)

从体系结构图中可以发现，MySQL数据库区别于其他数据库的最重要的一个特点就是其插件式的表存储引擎。MySQL插件式的存储引擎架构提供了一系列标准的管理和服务支持，这些标准与存储引擎本身无关，可能是每个数据库系统本身都必需的，如SQL分析器和优化器等，而存储引擎是底层物理结构和实际文件读写的实现，每个存储引擎开发者可以按照自己的意愿来进行开发。**需要特别注意的是，存储引擎是基于表的，而不是数据库。**

插件式存储引擎的好处是，每个存储引擎都有各自的特点，能够根据具体的应用建立不同存储引擎表。由于MySQL数据库的开源特性，用户可以根据MySQL预定义的存储引擎接口编写自己的存储引擎。若用户对某一种存储引擎的性能或功能不满意，可以通过修改源码来得到想要的特性，这就是开源带给我们的方便与力量。

由于MySQL数据库开源特性，存储引擎可以分为MySQL官方存储引擎和第三方存储引擎。有些第三方存储引擎很强大，**如大名鼎鼎的InnoDB存储引擎（最早是第三方存储引擎，后被Oracle收购)**，其应用就极其广泛，甚至是MySQL数据库OLTP(Online Transaction Processing在线事务处理）应用中使用最广泛的存储引擎。

存储引擎就是我们的数据真正存放的地方，在MySQL里面支持不同的存储引擎。现默认的存储引擎为InnoDB

这个大家可以为我们文件的格式，虽然内容是一样的，但是存储的文件方式可以有很多，就像我们文本数据信息，我们可以存储.txt，也可以存储为.sql，也可以存储为.js，也可以是md! 只是存储方式不一样，在格式，大小，速度方面有不同!

可直接命令查看：

![img](https://pics4.baidu.com/feed/54fbb2fb43166d2206136603e7a401f19152d24a.jpeg@f_auto?token=0d26e12ee6bd0e7e2f1f66cf7cb5a113&s=4D52AB42C3B4B26A54D9050E000030C1)



#### 2.1.3.1.MySQL官方引擎概要

官网地址：https://dev.mysql.com/doc/refman/5.7/en/storage-engines.html

MySQL 5.7 Supported Storage Engines

- [InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html): The default storage engine  in MySQL 5.7. InnoDB is a transaction-safe (ACID compliant) storage engine for MySQL that has commit, rollback, and crash-recovery capabilities to protect user data. InnoDB row-level locking (without escalation to coarser granularity locks) and Oracle-style consistent nonlocking reads increase multi-user concurrency and performance

大家有没有听说过MySQL 越来约像ORACLE了？

面试你也可以聊一聊。

前面讲过MySQL 历史 2003年开始集成InnoDB,

 但是InnoDB由芬兰Innobase Oy公司所开发> 2005年10月10日被Oracle并购  ； 

那这个引擎被收购跟我们mysql有啥关系呢。老东家被收购你还用那不是有问题了吗？

因为瑞典  MySQL AB公司 >2008归> SUN   >非常巧的是  2009> Oracle 收购了 SUN公司

最终mysql 和  innodb 又团聚了

**关键看下InnoDB 和 MyISAM 和 Memory.**

- InnoDB stores user data in clustered indexes to reduce I/O for common queries based on primary keys. To maintain data integrity, InnoDB also supports FOREIGN KEY referential-integrity constraints. For more information about InnoDB, see [Chapter 14, *The InnoDB Storage Engine*](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html).
- [MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html): These tables have a small footprint. [Table-level locking](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_table_lock) limits the performance in read/write workloads, so it is often used in read-only or read-mostly workloads in Web and data warehousing configurations.
- [Memory](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html): Stores all data in RAM, for fast access in environments that require quick lookups of non-criticaldata

This engine was formerly known as the HEAP engine. Its use cases are decreasing; InnoDB with its buffer pool memory area provides a general-purpose and durable way to keep most or all data in memory, andNDBCLUSTER provides fast key-value lookups for huge distributed data sets.)

[Archive](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html): These compact , unindexed tables are intended for storing and retrieving large amounts of seldom-referenced historical, archived, or security audit information.

这些紧凑的、无索引的表用于存储和检索大量很少引用的历史、归档或安全审计信息。

##### 类比图：

![image-20240127200806130](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240127200806130.png)



**接下来详细介绍**

**InnoDB存储引擎**(后面深入讲解)

InnoDB是MySQL的默认事务型引擎，也是最重要、使用最广泛的存储引擎。它被设计用来处理大量的短期(short-lived)事务，短期事务大部分情况是正常提交的，很少会被回滚。InnoDB的性能和自动崩溃恢复特性，使得它在非事务型存储的需求中也很流行。除非有非常特别的原因需要使用其他的存储引擎，否则应该优先考虑InnoDB引擎。如果要学习存储引擎，InnoDB也是一个非常好的值得花最多的时间去深入学习的对象，收益肯定比将时间平均花在每个存储引擎的学习上要高得多。所以InnoDB引擎也将是我们学习的重点。

**特点:**
DML操作遵循ACID模型，支持事务﹔
行级锁，提高并发访问性能;
支持外键FOREIGN KEY约束，保证数据的完整性和正确性;
**文件:**
xxx.ibd: xxx代表的是表名，innoDB引擎的每张表都会对应这样一个表空间文件，存储该表的表结构(frm、sdi)、数据和索引。
参数: innodb_file_per_table

**MylSAM存储引擎**

在MySQL 5.1及之前的版本，MyISAM是默认的存储引擎。MyISAM提供了大量的特性，包括全文索引、压缩、空间函数（GIS）等，但MyISAM不支持事务和行级锁，而且有一个毫无疑问的缺陷就是崩溃后无法安全恢复。尽管MyISAM引擎不支持事务、不支持崩溃后的安全恢复，但它绝不是一无是处的。对于只读的数据，或者表比较小、可以忍受修复（repair）操作，则依然可以继续使用MyISAM（但请不要默认使用MyISAM，而是应当默认使用InnoDB)。但是MyISAM对整张表加锁，而不是针对行。读取时会对需要读到的所有表加共享锁,写入时则对表加排他锁。MyISAM很容易因为表锁的问题导致典型的的性能问题。

**特点:**
不支持事务，不支持外键;
支持表锁，不支持行锁访问速度快
**文件:**
xxx.sdi:存储表结构信息
xxx.MYD:存储数据
xxx.MYI:存储索引

**Memory 引擎**

如果需要快速地访问数据，并且这些数据不会被修改，重启以后丢失也没有关系，那么使用Memory表(以前也叫做HEAP表）是非常有用的。Memory表至少比MyISAM 表要快一个数量级，因为每个基于MEMORY存储引擎的表实际对应一个磁盘文件。该文件的文件名与表名相同，类型为frm类型。该文件中只存储表的结构。而其数据文件，都是存储在内存中，这样有利于数据的快速处理，提高整个表的效率，不需要进行磁盘I/O。所以Memory表的结构在重启以后还会保留，但数据会丢失。

Memory表支持 Hash索引，因此查找操作非常快。虽然Memory表的速度非常快，但还是无法取代传统的基于磁盘的表。Memroy表是表级锁，因此并发写入的性能较低。它不支持BLOB或TEXT类型的列，并且每行的长度是固定的，所以即使指定了VARCHAR 列，实际存储时也会转换成CHAR，这可能导致部分内存的浪费。

**特点:**
内存存放
hash索引（默认)
**文件:**
Xxx.sdi:存储表结构信息

**Mrg_MylSAM**

Merge存储引擎，是一组MyIsam的组合，也就是说，他将MyIsam引擎的多个表聚合起来，但是他的内部没有数据，真正的数据依然是MyIsam引擎的表中，但是可以直接进行查询、删除更新等操作。

**Archive引擎**

Archive存储引擎只支持INSERT和SELECT操作，在MySQL 5.1之前也不支持索引。Archive引擎会缓存所有的写并利用zlib对插入的行进行压缩，所以比MyISAM表的磁盘I/O更少。但是每次SELECT查询都需要执行全表扫描。所以Archive表适合日志和数据采集类应用，这类应用做数据分析时往往需要全表扫描。或者在一些需要更快速的INSERT操作的场合下也可以使用。Archive引擎不是一个事务型的引擎，而是一个针对高速插入和压缩做了优化的简单引擎。

**Blackhole引擎**

Blackhole引擎没有实现任何的存储机制，它会丢弃所有插入的数据，不做任何保存。但是服务器会记录Blackhole表的日志，所以可以用于复制数据到备库，或者只是简单地记录到日志。这种特殊的存储引擎可以在一些特殊的复制架构和日志审核时发挥作用。但这种引擎在应用方式上有很多问题，因此并不推荐。

**CSV引擎**

CSV引擎可以将普通的CSV文件(逗号分割值的文件）作为MySQL的表来处理，但这种表不支持索引。CSV引擎可以在数据库运行时拷入或者拷出文件。可以将Excel等的数据存储为CSV文件，然后复制到MySQL数据目录下，就能在MySQL 中打开使用。同样，如果将数据写入到一个CSV引擎表，其他的外部程序也能立即从表的数据文件中读取CSV格式的数据。因此CSV引擎可以作为一种数据交换的机制，非常有用。

**Federated引擎**

Federated引擎是访问其他MySQL服务器的一个代理，它会创建一个到远程MySQL服务器的客户端连接，并将查询传输到远程服务器执行，然后提取或者发送需要的数据。最初设计该存储引擎是为了和企业级数据库如Microsoft SQL Server和 Oracle的类似特性竞争的，可以说更多的是一种市场行为。尽管该引擎看起来提供了一种很好的跨服务器的灵活性，但也经常带来问题，因此默认是禁用的。

**NDB集群引擎**

使用MySQL服务器、NDB集群存储引擎，以及分布式的、share-nothing 的、容灾的、高可用的NDB数据库的组合，被称为MySQL集群（(MySQL Cluster)。

#### 2.1.3.2.值得了解的第三方引擎

**Percona的 XtraDB存储引擎**

基于InnoDB引擎的一个改进版本，已经包含在Percona Server和 MariaDB中，它的改进点主要集中在性能、可测量性和操作灵活性方面。XtraDB可以作为InnoDB的一个完全的替代产品，甚至可以兼容地读写InnoDB的数据文件，并支持InnoDB的所有查询。

**TokuDB引擎**

使用了一种新的叫做分形树(Fractal Trees)的索引数据结构。该结构是缓存无关的，因此即使其大小超过内存性能也不会下降，也就没有内存生命周期和碎片的问题。TokuDB是一种大数据（Big Data)存储引擎，因为其拥有很高的压缩比，可以在很大的数据量上创建大量索引。现在该引擎也被Percona公司收购。

**Tips**  **：** 分形树，是一种写优化的磁盘索引数据结构。  分形树的写操作（Insert/Update/Delete）性能比较好，同时它还能保证读操作近似于B+树的读性能。据测试结果显示， TokuDB分形树的写性能优于InnoDB的B+树，读性能略低于B+树。分形树核心思想是利用节点的MessageBuffer缓存更新操作，充分利用数据局部性原理，将随机写转换为顺序写，这样极大的提高了随机写的效率。

**Infobright**

MySQL默认是面向行的，每一行的数据是一起存储的，服务器的查询也是以行为单位处理的。而在大数据量处理时，面向列的方式可能效率更高，比如HBASE就是面向列存储的。

Infobright是最有名的面向列的存储引擎。在非常大的数据量（数十TB)时，该引擎工作良好。Infobright是为数据分析和数据仓库应用设计的。数据高度压缩，按照块进行排序，每个块都对应有一组元数据。在处理查询时，访问元数据可决定跳过该块，甚至可能只需要元数据即可满足查询的需求。但该引擎不支持索引，不过在这么大的数据量级，即使有索引也很难发挥作用，而且块结构也是一种准索引 (quasi-index)。Infobright需要对MySQL服务器做定制，因为一些地方需要修改以适应面向列存储的需要。如果查询无法在存储层使用面向列的模式执行，则需要在服务器层转换成按行处理，这个过程会很慢。Infobright有社区版和商业版两个版本。

**定制化存储引擎**

详见官方API：https://dev.mysql.com/doc/dev/mysql-server/latest/

15.10 Other Storage Engines

Other storage engines may be available from third parties and community members that have used the Custom Storage Engine interface.

Third party engines are not supported by MySQL. For further information, documentation, installation guides, bug reporting or for any help or assistance with these engines, please contact the developer of the engine directly.

For more information on developing a customer storage engine that can be used with the Pluggable Storage Engine Architecture, see [MySQL Internals: Writing a Custom Storage Engine](https://dev.mysql.com/doc/internals/en/custom-engine.html).



#### 2.1.3.3.选择合适的引擎

这么多存储引擎，我们怎么选择?大部分情况下，InnoDB都是正确的选择，所以在MySQL 5.5版本将InnoDB作为默认的存储引擎了。对于如何选择存储引擎，可以简单地归纳为一句话:“**除非需要用到某些InnoDB不具备的特性，并且没有其他办法可以替代，否则都应该优先选择InnoDB引擎**”。比如，MySQL中只有MyISAM支持地理空间搜索。

当然，如果不需要用到InnoDB的特性，同时其他引擎的特性能够更好地满足需求，也可以考虑一下其他存储引擎。举个例子，如果不在乎可扩展能力和并发能力，也不在乎崩溃后的数据丢失问题，却对InnoDB的空间占用过多比较敏感，这种场合下选择MyISAM就比较合适。

**除非万不得已，否则建议不要混合使用多种存储引擎，否则可能带来一系列复杂的问题**，以及一些潜在的bug和边界问题。存储引擎层和服务器层的交互已经比较复杂，更不用说混合多个存储引擎了。至少，混合存储对一致性备份和服务器参数配置都带来了一些困难。

#### 2.1.3.4.表引擎的转换

有很多种方法可以将表的存储引擎转换成另外一种引擎。每种方法都有其优点和缺点。常用的有三种方法

**ALTER TABLE**

将表从一个引擎修改为另一个引擎最简单的办法是使用ALTER TABLE 语句。下面的语句将mytable的引擎修改为InnoDB :

```
ALTER TABLE mytable ENGINE = InnoDB;
```

上述语法可以适用任何存储引擎。但需要执行很长时间，在实现上，MySQL会按行将数据从原表复制到一张新的表中，在复制期间可能会消耗系统所有的I/O能力，同时原表上会加上读锁。所以，在繁忙的表上执行此操作要特别小心。

**导出与导入**

还可以使用mysqldump工具将数据导出到文件，然后修改文件中CREATE TABLE语句的存储引擎选项，注意同时修改表名，因为同一个数据库中不能存在相同的表名，即使它们使用的是不同的存储引擎。

**CREATE和 SELECT**

先创建一个新的存储引擎的表，然后利用INSERT…SELECT语法来导数据:

```
CREATE TABLE innodb_table LIKE myisam_table;
ALTER TABLE innodb_table ENGINE=InnoDB;
INSERT INTO innodb_table SELECT * FROM myisam_table;
```

如果数据量很大，则可以考虑做分批处理，针对每一段数据执行事务提交操作。

#### 2.1.3.5.检查MySQL的引擎

看我的MySQL现在已提供什么存储引擎:

```
show engines;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/391b00ec032a4a38bd999e262c7501b2.png)

看我的MySQL当前默认的存储引擎:

```
show variables like '%storage_engine%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/49297a01dc5d42929ee59e2d43fca04e.png)

#### 2.1.3.6.MyISAM和InnoDB比较

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/859c96ec674b463b815664640120abee.png)

## 更新语句的差异

写语句也会走上面相关的流程：连接、解析器、处理器、优化器、执行器。

但是交给执行器拿到数据后，后续操作跟读会有很大区别，会有相关日志操作

### redoLog（重做日志）

思考一个问题：因为刷脏不是实时的，如果Buffer Pool里面的脏页还没有刷入磁盘时，数据库宕机或者重启，这些数据就会丢失。为了避免这个问题，InnoDB把所有对页面的修改操作专门写入一个日志文件。

如果有未同步到磁盘的数据，数据库在启动的时候，会从这个日志文件进行恢复操作（实现crash-safe）。我们说的事务的ACID里面D（持久性），就是用它来实现的。

redo log包括两部分：一是内存中的日志缓冲(redo log buffer)，该部分日志是易失性的；二是磁盘上的重做日志文件(redo log file)，该部分日志是持久的。

redo log有什么特点？

- redo log是InnoDB存储引擎实现的，并不是所有存储引擎都有。支持崩溃恢复是InnoDB的一个特性。
- redo log不是记录数据页更新之后的状态，而是记录的是“在某个数据页上做了什么修改”。属于物理日志。
- redo log的大小是固定的，前面的内容会被覆盖，一旦写满，就会触发buffer pool到磁盘的同步，以便腾出空间记录后面的修改。
- innodb_flush_log_at_trx_commit 这个参数设置成 1 的时候，表示每次事务的 redo log 都直接从redo log buffer持久化到磁盘。刷盘越快，越安全，但是也会越消耗性能。

| 值                        | 含义                                                         |
| ------------------------- | ------------------------------------------------------------ |
| 0（延迟写）               | log buffer将每秒一次地写入log file中，并且log file的flush操作同时进行。该模式下，在事务提交的时候，不会主动触发写入磁盘的操作。 |
| 1（默认，实时写，实时刷） | 每次事务提交时MySQL都会把log buffer的数据写入log file，并且刷到磁盘中去。 |
| 2（实时写，延迟刷）       | 每次事务提交时MySQL都会把log buffer的数据写入log file。但是flush操作并不会同时进行。该模式下，MySQL会每秒执行一次 flush操作。 |

**那么redo log Buffer什么时候同步到磁盘？**

1.redo log buffer 使用量达到了参数`innndb_log_buffer_size`的一半时，会触发落盘。

2.后台线程，每隔一段时间（1s）就会将redo log block刷新到磁盘文件中去。

3.Mysql正常关闭

4.事务提交时，可配 innodb_flush_log_at_trx_commit参数

该参数有几个选项：0、1、2

- 想要保证ACID四大特性推荐设置为1：表示当你commit时，MySQL必须将rodolog-buffer中的数据刷新进磁盘中。确保只要commit是成功的，磁盘上就得有对应的rodolog日志。这也是最安全的情况。

- 设置为0：每秒写一次日志并将其刷新到磁盘。

- 设置为2：表示当你commit时，将redolog-buffer中的数据刷新进OS Cache中，然后依托于操作系统每秒刷新一次的机制将数据同步到磁盘中，也存在丢失的风险。

### undoLog（回滚日志）

undo log（撤销日志或回滚日志）记录了事务发生之前的数据状态，分为insert undo log和update undo log。如果修改数据时出现异常，可以用undo log来实现回滚操作（保持原子性）。

写undo log 也会产生redo log

可以理解为undo log记录的是反向的操作，比如insert会记录delete，update会记录update原来的值，跟redolog记录在哪个物理页面做了什么操作不同，所以叫做逻辑格式的日志。

show global variables like '%undo%';

| 值                       | 含义                                                         |
| ------------------------ | ------------------------------------------------------------ |
| innodb_undo_directory    | undo 文件的路径                                              |
| innodb_undo_log_truncate | 设置为1，即开启在线回收（收缩）undo log日志文件              |
| innodb_max_undo_log_size | 如果innodb_undo_log_truncate设置为1，超过这个大小的时候会触发truncate回收（收缩）动作，如果page大小是16KB，truncate后空间缩小到10M。默认1073741824字节=1G。 |
| innodb_undo_logs         | 回滚段的数量， 默认128，这个参数已经过时。                   |
| innodb_undo_tablespaces  | 设置undo独立表空间个数，范围为0-95， 默认为0，0表示表示不开启独立undo表空间 且 undo日志存储在ibdata文件中。这个参数已经过时。 |

redo Log和undo Log与事务密切相关，统称为事务日志。

### binLog（归档日志）

binlog是MySQL的Server层实现的，所有引擎都可以使用。

inlog以事件的形式记录了所有的DDL和DML语句（因为它记录的是操作而不是数据值，属于逻辑日志），可以用来做主从复制和数据恢复。

跟redo log不一样，它的文件内容是可以追加的，没有固定大小限制。

在开启了binlog功能的情况下，我们可以把binlog导出成SQL语句，把所有的操作重放一遍，来实现数据的恢复。

binlog的另一个功能就是用来实现主从复制，它的原理就是从服务器读取主服务器的binlog，然后执行一遍。

```mysql
show binlog events    只查看第一个binlog文件的内容
show BINLOG EVENTS in 'binlog.000019'    查看指定binlog文件的内容
show binary logs   获取binlog文件列表
show master status   查看当前正在写入的binlog文件
```

 刚才我们讲的redoLog属于InnoDB独有的，因为redolog的目的是为了事务里面的持久性，说到就要做到，所以它的实现是在InnoDB存储引擎去实现

但是BinLog就不只是InnoDB独有的，而是在我们的Service层实现的。

binlog是我们的二进制日志文件，记录了Mysql的所有的DML操作，我们可以通过binlog日志做数据恢复、增量备份、主从复制等！



#### **那么为什么要2个了？**

innodb利用wal技术进行数据恢复，write ahead logging技术依赖于物理日志进行数据恢复，binlog不是物理日志是逻辑日志，因此无法使用

redolog是循环写，写到末尾要回到开头继续写，这样的日志无法保留历史记录，无法进行数据复制。



#### 为什么需要两阶段提交？ 

举例： 如果我们执行的是把name改成 天明，如果写完redo log，还没有写binlog的时候，MySQL重启了。 因为redo
log可以在重启的时候用于恢复数据，所以写入磁盘的是盆鱼宴。但是binlog里面没有记录这个逻辑日志，所以这时候用binlog去恢复数据或者同步到从库，就会出现数据不一致的情况。
所以在写两个日志的情况下，binlog就充当了一个事务的协调者。通知InnoDB来执行prepare或者commit或者rollback。 如果第⑥步写入binlog失败，就不会提交。
简单地来说，这里有两个写日志的操作，类似于分布式事务，不用两阶段提交，就不能保证都成功或者都失败。

在崩溃恢复时，判断事务是否需要提交： 

1、binlog无记录，redolog无记录： 在redolog写之前crash，恢复操作：回滚事务 

2、binlog无记录，redolog状态prepare：
在binlog写完之前的crash，恢复操作：回滚事务

3、binlog有记录，redolog状态prepare： 在binlog写完提交事务之前的crash，恢复操作：提交事务 

4、binlog有记录，redolog状态commit： 正常完成的事务，不需要恢复



#### 为什么有一个binlog 日志记录DDL 还需要 一个redo重做呢？  

####  或者这两个日志有什么区别呢？

首先：

记录完redo时是prepare状态，等记录bin之后变为commit状态，这个操作称之为 二段式提交。

这样做的目的是避免在写binlog时宕机，靠这个文件去做主从同步会导致不一致。

具体步骤：处于prepare状态的redo会记录2PC的XID（两log共同的字段），binlog写入后也会记录，同时给redo打上commit标识。

然后：

1.binlog 日志 server层所有存储引擎共有   

2.redo 环形固定大小，循环写。记录的物理日志 （在某个数据页上做了某个修改）

   	bin 无限大小，追加写。记录的逻辑日志 （给某个ID行的数据做修改）无法确定书否落盘，不清楚哪些需要恢复。

3.redo会刷掉已落盘的数据  当数据库 crash 宕机，主从同步就行不通了。

想要恢复，需要结合这两个日志。因为bin虽然全量日志但无法标识是否落盘。而redo是innoDB特有而且落盘会覆盖掉。

Sharding-JDBC 分布式事务 根据多个库的ACK返回判断是否commit与rollback各库也是采用 2PC机制

恢复的判断规则：

如果redo 既有prepare 又有commit的，就直接提交

如果只有prepare 没有commit 的，就拿xid去binlog 找对应的事务。binlog 无记录就回滚，有记录就提交

不这么做的问题。比如：同一阶段提交，redo 写完提交，写bin的时候进程崩溃，由于bin没有认知，使用 redo + bin 恢复(或者主从同步)的数据就是数据库的旧数据

  如果先写bin 在bin写完提交后崩溃，由于没有redo，奔溃恢复（不能重做此）之后这个事务需要回滚，再之后用redo+bin 来恢复就多出一个事务，且回滚的结果不是原来的



#### 主从同步原理：

主要是利用到binlog  + redo日志。
binlog日志：
它是mysql用来记录db改变的日志，
比如某条数据的值从0改为1 (DML语句)
比如某张表被删除了 (DDL语句)
binlog 有三种形式：
(1)statement:记录具体引起改动的操作语句，比如insert xxxxx....
(2)row:基于数据行的，原来数据行是xx值改为了yy 值，这种一般占用空间比较大
(3)mixed:混合模式，由服务自己来决定此次变更采用哪种形式。
当sql操作写入binlog，就已经算作sql执行成功了，而不是写入到对应磁盘中（刷盘）。所以binlog中对应的值，我们可以理解为就是mysql的一个映射，同步mysql数据不同捞磁盘中的数据进行同步，而只需要同步binlog日志就行。
具体的同步原理如下：
（1）主从同步设置好之后（进行相关的诸如ip，端口，服务id，等操作设置后）
（2）相关变动会写入到binlog中
（3）maser会启动一个线程：**binlog dumplog 线程**，这个线程会通知从机，当前存在SQL变更，并将binlog的变动发送到从机上
（4）从机收到请求后，会启动线程：**i/o线程** ，该线程会将收到的binlog日志加载到中继日志delay log中
（5）从机中的另外一个线程：**SQL 线程**会读取relay日志中的信息，刷新到从机中

##### 具体可见下图

![image-20240129132802894](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129132802894.png)













#### 总结更新流程：

![image-20240127224030294](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240127224030294.png)







## 2.2.MySQL中的目录和文件

### 2.2.1.bin目录

在MysQL的安装目录下有一个特别特别重要的bin目录，这个目录下存放着许多可执行文件。

其他系统中的可执行文件与此的类似。这些可执行文件都是与服务器程序和客户端程序相关的。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/17fab658bb7a4707a7227109ecfc0d7b.png)

#### 2.2.1.1.启动MySQL服务器程序

在UNIX系统中用来启动MySOL服务器程序的可执行文件有很多，大多在MySQL安装目录的bin目录下。

**mysqld**

mysqld这个可执行文件就代表着MySOL服务器程序，运行这个可执行文件就可以直接启动一个服务器进程。但这个命令不常用。

**mysqld_safe**

mysqld safe是一个启动脚本，它会间接的调用mysqld，而且还顺便启动了另外一个监控进程，这个监控进程在服务器进程挂了的时候，可以帮助重启它。另外,使用mysqld_safe启动服务器程序时，它会将服务器程序的出错信息和其他诊断信息重定向到某个文件中，产生出错日志，这样可以方便我们找出发生错误的原因。

**mysql.server**

mysql.server也是一个启动脚本，它会间接的调用mysqld_safe，在调用mysql.server时在后边指定start参数就可以启动服务器程序了

就像这样:

```
mysql.server start
```

需要注意的是，这个mysql.server文件其实是一个链接文件，它的实际文件是support-files/mysql.server，所以如果在bin目录找不到，到support-files下去找找，而且如果你愿意的话，自行用ln命令在bin创建一个链接。

另外，我们还可以使用mysql.server命令来关闭正在运行的服务器程序，只要把start参数换成stop就好了:

```
mysql.server stop
```

**mysqld_multi**

其实我们一台计算机上也可以运行多个服务器实例，也就是运行多个NySQL服务器进程。mysql_multi可执行文件可以对每一个服务器进程的启动或停止进行监控。

#### 2.2.1.2.客户端程序

在我们成功启动MysTL服务器程序后，就可以接着启动客户端程序来连接到这个服务器喽， bin目录下有许多客户端程序，比方说mysqladmin、mysqldump、mysqlcheck等等。

我们常用的是可执行文件mysql，通过这个可执行文件可以让我们和服务器程序进程交互，也就是发送请求，接收服务器的处理结果。

mysqladmin执行管理操作的工具，检查服务器配置、当前运行状态，创建、删除数据库、设置新密码。

mysqldump数据库逻辑备份程序。

mysqlbackup备份数据表、整个数据库、所有数据库，一般来说mysqldump备份、mysql还原。

### 2.2.2.启动选项和参数

#### 2.2.2.1.配置参数文件

当MySQL实例启动时，数据库会先去读一个配置参数文件，用来寻找数据库的各种文件所在位置以及指定某些初始化参数，这些参数通常定义了某种内存结构有多大等。在默认情况下，MySQL实例会按照-定的顺序在指定的位置进行读取，用户只需通过命令mysql --help|grep my.cnf来寻找即可。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/767392726c854d33b241a2f48dbdac49.png)

当然，也可以在启动MySQL时，指定配置文件（非yum安装）：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/434a30389c9949be885596c768d84f91.png)

这个时候，就会以启动时指定的配置文件为准。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/5857cd97bdd74f0a94195720fef08eb6.png)

MySQL数据库参数文件的作用和Oracle数据库的参数文件极其类似，不同的是，Oracle实例在启动时若找不到参数文件，是不能进行装载(mount）操作的。MySQL稍微有所不同，MySQL实例可以不需要参数文件，这时所有的参数值取决于编译MySQL时指定的默认值和源代码中指定参数的默认值。

MySQL数据库的参数文件是以文本方式进行存储的。可以直接通过一些常用的文本编辑软件进行参数的修改。

#### 2.2.2.2.参数的查看和修改

可以通过命令show variables查看数据库中的所有参数，也可以通过LIKE来过滤参数名，前面查找数据库引擎时已经展示过了。从 MySQL 5.1版本开始，还可以通过information_schema架构下的GLOBAL_VARIABLES视图来进行查找，推荐使用命令
show variables，使用更为简单，且各版本的 MySQL数据库都支持。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/695332512b114ad18df5a44d942ee15d.png)

参数的具体含义可以参考MySQL官方手册：

**https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html**

但是课程中遇到的参数会进行讲解。

MySQL数据库中的参数可以分为两类:动态(dynamic）参数和静态(static）参数。同时从作用范围又可以分为全局变量和会话变量。

动态参数意味着可以在 MySQL实例运行中进行更改，静态参数说明在整个实例生命周期内都不得进行更改，就好像是只读(read only)的。

全局变量（GLOBAL）影响服务器的整体操作。

会话变量（SESSION/LOCAL）影响某个客户端连接的操作。

举个例子，用default_storage_engine来说明，在服务器启动时会初始化一个名为default_storage_engine，作用范围为GLOBAL的系统变量。之后每当有一个客户端连接到该服务器时，服务器都会单独为该客户端分配一个名为default_storage_engine，作用范围为SESSION的系统变量，该作用范围为SESSION的系统变量值按照当前作用范围为GLOBAL的同名系统变量值进行初始化。

可以通过SET命令对动态的参数值进行修改。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/2813499586944dfe93e4dbeeb2ec3e26.png)

SET的语法如下：

```
set [global || session ] system_var_name= expr
或者
set [@@global. || @@session.] system_var_name= expr
比如：
set read_buffer_size=524288;
set session read_buffer_size=524288;
set @@global.read_buffer_size=524288;
```

MySQL所有动态变量的可修改范围，可以参考MySQL官方手册的 Dynamic System Variables 的相关内容：

**https://dev.mysql.com/doc/refman/5.7/en/dynamic-system-variables.html**

对于静态变量，若对其进行修改，会得到类似如下错误:![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/2439885a15e1434bb6b93f520c6e3dd1.png)

### 2.2.3.数据目录

我们知道像InnoDB、MyIASM这样的存储引擎都是把表存储在磁盘上的，而操作系统用来管理磁盘的那个东东又被称为文件系统，所以用专业一点的话来表述就是:像InnoDB、MyISAM这样的存储引擎都是把表存储在文件系统上的。当我们想读取数据的时候，这些存储引擎会从文件系统中把数据读出来返回给我们，当我们想写入数据的时候，这些存储引擎会把这些数据又写回文件系统。

#### 2.2.3.1.确定MySQL中的数据目录

那说了半天，到底MySQL把数据都存到哪个路径下呢?其实数据目录对应着一个系统变量datadir，我们在使用客户端与服务器建立连接之后查看这个系统变量的值就可以了：

```
show variables like 'datadir';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/46dc38b0a1ba4285b95cff587b554cba.png)

当然这个目录可以通过配置文件进行修改，由我们自己进行指定。

#### 2.2.3.2.数据目录中放些什么？

MySOL在运行过程中都会产生哪些数据呢?当然会包含我们创建的数据库、表、视图和触发器等用户数据，除了这些用户数据，为了程序更好的运行，MySQL也会创建一些其他的额外数据

##### 2.2.3.2.1.数据库在文件系统中的表示

```
create database lijin charset=utf8;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/a7c1befb816f4a31bfd382ffab4bac3e.png)cd

每当我们使用CREATE DATABASE语句创建一个数据库的时候，在文件系统上实际发生了什么呢?其实很简单，每个数据库都对应数据目录下的一个子目录，或者说对应一个文件夹，我们每当我们新建一个数据库时，MySQL会帮我们做这两件事儿:

1．在数据目录下创建一个和数据库名同名的子目录（或者说是文件夹)。

2．在该与数据库名同名的子目录下创建一个名为db.opt的文件，这个文件中包含了该数据库的各种属性，比方说该数据库的字符集和比较规则是个啥。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/c6685e545d434efeaad3004b8fcbd5c7.png)

比方说我们查看一下在我的计算机上当前有哪些数据库︰

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/fe3701bd5ff740909c5726761270ed00.png)

可以看到在当前有5个数据库，其中mysqladv数据库是我们自定义的，其余4个数据库是属于MySQL自带的系统数据库。我们再看一下数据目录下的内容:

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/001702e6d19e48d1afd265e34070fd77.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/b4c7f5dedfef4da5be2333596036a50b.png)

当然这个数据目录下的文件和子目录比较多，但是如果仔细看的话，除了information_schema这个系统数据库外，其他的数据库在数居目录下都有对应的子目录。这个information_schema比较特殊，我们后面再讲它的作用。

##### 2.2.3.2.2.表在文件系统中的表示

我们的数据其实都是以记录的形式插入到表中的，每个表的信息其实可以分为两种:

1.表结构的定义

2．表中的数据

表结构就是该表的名称是啥，表里边有多少列，每个列的数据类型是啥，有啥约束条件和索引，用的是啥字符集和比较规则各种信息，这些信息都体现在了我们的建表语句中了。为了保存这些信息，InnoDB和MyIASM这两种存储引擎都在数据目录下对应的数据库子目录下创建了一个专门用于描述表结构的文件，文件名是这样:表名.frm

比方说我们在lijin数据库下创建一个名为test的表:

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/ed9aba39513946eb8178b748ff282276.png)

那在数据库mysqladv对应的子目录下就会创建一个名为test.frm的用于描述表结构的文件。这个后缀名为.fm是以二进制格式存储的。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/7c5d560556494602995b1ac439beb85b.png)cd

那表中的数据存到什么文件中了呢?在这个问题上，不同的存储引擎就产生了有所不同，下边我们分别看一下InnoDB和MyISAM是用什么文件来保存表中数据的。

##### 2.2.3.2.3.lnnoDB是如何存储表数据的

InnoDB的数据会放在一个表空间或者文件空间（英文名: table space或者file space)的概念，这个表空间是一个抽象的概念，它可以对应文件系统上一个或多个真实文件〈不同表空间对应的文件数量可能不同)。每一个表空间可以被划分为很多很多很多个页，我们的表数据就存放在某个表空间下的某些页里。表空间有好几种类型。

**系统表空间(system tablespace)**

这个所谓的系统表空间可以对应文件系统上一个或多个实际的文件，默认情况下，InnoDB会在数据目录下创建一个名为ibdata1(在你的数据目录下找找看有木有)、大小为12M的文件，这个文件就是对应的系纳表空间在文件系统上的表示。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/6d3767c7708848ddb0b110e20df12388.png)

这个文件是所谓的自扩展文件，也就是当不够用的时候它会自己增加文件大小，当然，如果你想让系统表空间对应文件系统上多个实际文件，或者仅仅觉得原来的ibdata1这个文件名难听，那可以在MySQL启动时配置对应的文件路径以及它们的大小，我们也可以把系统表空间对应的文件路径不配置到数据目录下，甚至可以配置到单独的磁盘分区上。

需要注意的一点是，在一个MySQL服务器中，系统表空间只有一份。从MySQL5.5.7到MySQL5.6.6之间的各个版本中，我们表中的数据都会被默认存储到这个系统表空间。

**独立表空间(file-per-table tablespace)**

在MySQL5.6.6以及之后的版本中，InnoB并不会默认的把各个表的数据存储到系统表空间中，而是为每一个表建立一个独立表空间，也就是说我们创建了多少个表，就有多少个独立表空间。使用独立表空间来存储表数据的话，会在该表所属数据库对应的子目录下创建一个表示该独立表空间的文件，文件名和表名相同，只不过添加了一个.ibd的扩展名而已，所以完整的文件名称长这样:表名.ibd。

比方说假如我们使用了独立表空间去存储lijin数据库下的test表的话，那么在该表所在数据库对应的lijin目录下会为test表创建这两个文件:

test.frm和test.ibd

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/dcd558e8144240b380b4bb48237d8163.png)

其中test.ibd文件就用来存储test表中的数据和索引。当然我们也可以自己指定使用系统表空间还是独立表空间来存储数据，这个功能由启动参数

innodb_file_per_table控制，比如说我们想刻意将表数据都存储到系统表空间时，可以在启动MySQL服务器的时候这样配置:

```
[server]

innodb_file_per_table=0
```

当imodb_file_per table的值为0时，代表使用系统表空间;当innodb_file_per table的值为1时，代表使用独立表空间。不过inmodb_file_per_table参数只对新建的表起作用，对于已经分配了表空间的表并不起作用。

**其他类型的表空间**

随着MySQL的发展，除了上述两种老牌表空间之外，现在还新提出了一些不同类型的表空间，比如通用表空间(general tablespace) ,undo表空间(undotablespace)、临时表空间〈temporary tablespace)等。

##### 2.2.3.2.4.MyISAM是如何存储表数据的

在MyISAM中的数据和索引是分开存放的。所以在文件系统中也是使用不同的文件来存储数据文件和索引文件。而且和InnoDB不同的是，MyISA并没有什么所谓的表空间一说，表数据都存放到对应的数据库子目录下。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/5641ac68aec245528eeb761edb99f274.png)

test_myisam表使用MyISAM存储引擎的话，那么在它所在数据库对应的lijin目录下会为myisam表创建三个文件:

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/35de2695a83e4fefbbcfba0e673a3f53.png)

其中test_myisam.MYD代表表的数据文件，也就是我们插入的用户记录; test_myisam.MYI代表表的索引文件，我们为该表创建的索引都会放到这个文件中。

#### 2.2.3.3.日志文件

在服务器运行过程中，会产生各种各样的日志，比如常规的查询日志、错误日志、二进制日志、redo日志、Undo日志等等，日志文件记录了影响MySQL数据库的各种类型活动。

常见的日志文件有：错误日志（error log）、慢查询日志（slow query log）、查询日志（query log）、二进制文件（bin log）。

**错误日志**

错误日志文件对MySQL的启动、运行、关闭过程进行了记录。遇到问题时应该首先查看该文件以便定位问题。该文件不仅记录了所有的错误信息，也记录一些警告信息或正确的信息

用户可以通过下面命令来查看错误日志文件的位置：

```
show variables like 'log_error'\G;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/c7d5ac83a6224143acc8f474ce23991e.png)

当MySQL不能正常启动时，第一个必须查找的文件应该就是错误日志文件，该文件记录了错误信息。

**慢查询日志**

慢查询日志可以帮助定位可能存在问题的SQL语句，从而进行SQL语句层面的优化。

我们已经知道慢查询日志可以帮助定位可能存在问题的SQL语句，从而进行SQL语句层面的优化。但是默认值为关闭的，需要我们手动开启。

```
show VARIABLES like 'slow_query_log';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f72a83180181494fa68d4f014375127b.png)

```
set GLOBAL slow_query_log=1;
```

开启1，关闭0

但是多慢算慢？MySQL中可以设定一个阈值，将运行时间超过该值的所有SQL语句都记录到慢查询日志中。long_query_time参数就是这个阈值。默认值为10，代表10秒。

```
show VARIABLES like '%long_query_time%';
```

当然也可以设置

```
set global long_query_time=0;
```

默认10秒，这里为了演示方便设置为0

同时对于运行的SQL语句没有使用索引，则MySQL数据库也可以将这条SQL语句记录到慢查询日志文件，控制参数是：

```
show VARIABLES like '%log_queries_not_using_indexes%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/19a8d15f0d724fae93946b5bd4f63cc3.png)

开启1，关闭0（默认）

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/67a74308e0524b459cb30cfa66bdba40.png)

```
show VARIABLES like '%slow_query_log_file%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/67524e90e45643d492d14b6c4874a30a.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/ec81c6c0c7fd415aab964da80680c8d8.png)

**查询日志**

查看当前的通用日志文件是否开启

```
show variables like '%general%'
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/1a883cd2f8c245188bab87b9876a9351.png)

```
开启通⽤⽇志查询： set global general_log = on;
关闭通⽤⽇志查询：set global general_log = off;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/fdc92875bf2c4685b1b8a9273230ceed.png)sele

查询日志记录了所有对MySQL数据库请求的信息，无论这些请求是否得到了正确的执行。

默认文件名：主机名.log

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/ae0822bb332b45c3b4ff96e3246e2a74.png)

**二进制日志（binlog）**

二进制日志记录了所有的DDL和DML语句（除了数据查询语句select）,以事件形式记录，还包含语句所执⾏的消耗的时间，MySQL的⼆进制⽇志是事务安全型的

**二进制日志的几种作用：**

恢复（recovery）：某些数据的恢复需要二进制日志，例如，在一个数据库全备文件恢复后，用户可以通过二进制文件进行point-in-time的恢复

复制（replication）：其原理与恢复类似，通过复制和执行二进制日志使一台远程的MySQL数据库（一般称为slave或standby）与一台MySQL数据库（一般称为master或primary）进行实时同步

审计（audit）：用户可以通过二进制日志中的信息来进行审计，判断是否有对数据库进行注入的攻击

log-bin参数该参数用来控制是否开启二进制日志，默认为关闭

如果想要开启二进制日志的功能，可以在MySQL的配置文件中指定如下的格式：

“name”为二进制日志文件的名称

如果不提供name，那么数据库会使用默认的日志文件名（文件名为主机名，后缀名为二进制日志的序列号），且文件保存在数据库所在的目录（datadir下）

--启用/设置二进制日志文件(name可省略)

log-bin=name;

配置以后，就会在数据目录下产生类似于：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/850c1ed18f7c496a96d01d707e224f80.png)

bin_log.00001即为二进制日志文件；bin_log.index为二进制的索引文件，用来存储过往产生的二进制日志序号，通常情况下，不建议手动修改这个文件。

二进制日志文件在默认情况下并没有启动，需要手动指定参数来启动。开启这个选项会对MySQL的性能造成影响，但是性能损失十分有限。根据MySQL官方手册中的测试指明，开启二进制日志会使性能下降1%。

查看binlog是否开启

```
show variables like 'log_bin';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/03cbeb4270ef4342946d640a1afc02f0.png)

mysql安装目录下修改my.cnf

```
log_bin=mysql-bin
binlog-format=ROW
server-id=1
expire_logs_days =30
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/7bcab5e8667f48a7b05aa7a9820013a0.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/5b11e5971bcb45db95d0b8b45539d597.png)

#### 2.2.3.3.其他的数据文件

除了我们上边说的这些用户自己存储的数据以外，数据文件下还包括为了更好运行程序的一些额外文件，当然这些文件不一定会放在数据目录下，而且可以在配置文件或者启动时另外指定存放目录。

主要包括这几种类型的文件:

·服务器进程文件。

我们知道每运行一个MySQL服务器程序，都意味着启动一个进程。MySQL服务器会把自己的进程ID写入到一个pid文件中。

socket文件

当用UNIX域套接字方式进行连接时需要的文件。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/90dbdb30c0d4476f958e69c528af61a2.png)

·默认/自动生成的SSL和RSA证书和密钥文件。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654000409075/adcea5c8cccd41fea0df37221fab7a2b.png)

# 1.MySQL中的系统库

## 1.1.系统库简介

MySQL有几个系统数据库，这几个数据库包含了MySQL服务器运行过程中所需的一些信息以及一些运行状态信息，我们现在稍微了解一下。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/5fa5aef724f744339fc623fe2cde71e1.png)

**performance_schema**

这个数据库里主要保存MySQL服务器运行过程中的一些状态信息，算是对MySQL服务器的一个性能监控。包括统计最近执行了哪些语句，在执行过程的每个阶段都花费了多长时间，内存的使用情况等等信息。

**information_schema**

这个数据库保存着MySQL服务器维护的所有其他数据库的信息，比如有哪些表、哪些视图、哪些触发器、哪些列、哪些索引。这些是一些描述性信息，称之为元数据。

**sys**

这个数据库通过视图的形式把information_schema和performance_schema结合起来，让程序员可以更方便的了解MySQL服务器的一些性能信息。

**mysql**

主要存储了MySQL的用户账户和权限信息，还有一些存储过程、事件的定义信息，一些运行过程中产生的日志信息，一些帮助信息以及时区信息等。

## 1.2.performance_schema

### 1.2.1.什么是performance_schema

MySQL的performance_schema 是运行在较低级别的用于监控MySQL Server运行过程中的资源消耗、资源等待等情况的一个功能特性，它具有以下特点。

**运行在较低级别：**采集的东西相对比较底层，比如磁盘文件、表I/O、表锁等等。

•　performance_schema提供了一种在数据库运行时实时检查Server内部执行情况的方法。performance_schema 数据库中的表使用performance_schema存储引擎。该数据库主要关注数据库运行过程中的性能相关数据。

•　performance_schema通过监视Server的事件来实现监视其内部执行情况，“事件”就是在Server内部活动中所做的任何事情以及对应的时间消耗，利用这些信息来判断Server中的相关资源被消耗在哪里。一般来说，事件可以是函数调用、操作系统的等待、SQL语句执行的阶段[如SQL语句执行过程中的parsing（解析）或sorting（排序）阶段]或者整个SQL语句的集合。采集事件可以方便地提供Server中的相关存储引擎对磁盘文件、表I/O、表锁等资源的同步调用信息。

•　当前活跃事件、历史事件和事件摘要相关表中记录的信息，能提供某个事件的执行次数、使用时长，进而可用于分析与某个特定线程、特定对象（如mutex或file）相关联的活动。

•　performance_schema存储引擎使用Server源代码中的“检测点”来实现事件数据的收集。对于performance_schema实现机制本身的代码没有相关的单独线程来检测，这与其他功能（如复制或事件计划程序）不同。

收集到的事件数据被存储在performance_schema数据库的表中。对于这些表可以使用SELECT语句查询，也可以使用SQL语句更新performance_schema数据库中的表记录（比如动态修改performance_schema的以“setup_”开头的配置表，但要注意，配置表的更改会立即生效，这会影响数据收集）。

•　performance_schema的表中数据不会持久化存储在磁盘中，而是保存在内存中，一旦服务器重启，这些数据就会丢失（包括配置表在内的整个performance_schema下的所有数据）。

### 1.2.2.performance_schema使用

通过上面介绍，相信你对于什么是performance_schema这个问题了解得更清晰了。下面开始介绍performance_schema的使用。

### 1.2.3.检查当前数据库版本是否支持

performance_schema被视为存储引擎，如果该引擎可用，则应该在

INFORMATION_SCHEMA.ENGINES表或show engines语句的输出中可以看到它的Support字段值为YES，如下所示。

```
select * from INFORMATION_SCHEMA.ENGINES;
show engines;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/4eaeb361df6a429e913734336424b62d.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/319e49c66d5a4ca19b9ece850b0eb812.png)

当我们看到performance_schema对应的Support字段值为YES时，就表示当前的数据库版本是支持performance_schema的。但确认了数据库实例支持performance_schema存储引擎就可以使用了吗？NO，很遗憾，performance_schema在MySQL 5.6及之前的版本中默认没有启用，在MySQL 5.7及之后的版本中才修改为默认启用。

mysqld启动之后，通过如下语句查看performance_schema启用是否生效（值为ON表示performance_schema已初始化成功且可以使用了；值为OFF表示在启用performance_schema时发生某些错误，可以查看错误日志进行排查）。

```
show variables like 'performance_schema';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/bcbf802aaec94c4cbdc011df07b2ac8a.png)

*（如果要显式启用或关闭* *performance_schema* *，则需要使用参数**performance_schema=ON|OFF**来设置，并在*my.cnf*中进行配置。注意*  *:* *该参数为只读参数，需要在实例启动之前设置才生效）*

现在，可以通过查询INFORMATION_SCHEMA.TABLES表中与performance_schema存储引擎相关的元数据，或者在performance_schema库下使用show tables语句来了解其存在哪些表。

使用show tables语句来查询有哪些performance_schema引擎表。

现在，我们知道了在当前版本中，performance_schema库下一共有87个表，

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/d1574749323b4c338d87c6ee2f134632.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/80ac426fb1b748919008186131cd93e5.png)

那么这些表都用于存放什么数据呢？我们如何使用它们来查询数据呢？先来看看这些表是如何分类的。

### 1.2.4.performance_schema表的分类

performance_schema库下的表可以按照监视的不同维度进行分组，例如：按照不同的数据库对象进行分组、按照不同的事件类型进行分组，或者按照事件类型分组之后，再进一步按照账号、主机、程序、线程、用户等进行细分。

下面介绍按照事件类型分组记录性能事件数据的表。

•　语句事件记录表：记录语句事件信息的表，包括：events_statements_current（当前语句事件表）、events_statements_history（历史语句事件表）、events_statements_history_long（长语句历史事件表）以及一些summary表（聚合后的摘要表）。其中，summary表还可以根据账号（account）、主机（host）、程序（program）、线程（thread）、用户（user）和全局（global）再进行细分。

```
show tables like 'events_statement%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/6dccdeaa1e0248408af7ada1f39a2eba.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/d557da5e337a4a9fa738da2981d4c8ba.png)

•　等待事件记录表：与语句事件记录表类似。

```
show tables like 'events_wait%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/dd1baacfac7f42f7b7c20490ac5c57f5.png)

•　阶段事件记录表：记录语句执行阶段事件的表，与语句事件记录表类似。

```
show tables like 'events_stage%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/d1488c9b7d3e4828a58be8b684dacf84.png)

•　事务事件记录表：记录与事务相关的事件的表，与语句事件记录表类似。

```sql
show tables like 'events_transaction%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/fd377925af6a4ddda0c729cd4e3cedc4.png)

•　监视文件系统层调用的表：

```sql
show tables like '%file%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/1dfbf5a81a954927bb4b034949a41748.png)

•　监视内存使用的表：

```
show tables like '%memory%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/410a3119ca5a44459bc32274aa8c453a.png)

•　动态对performance_schema进行配置的配置表：

```
show tables like '%setup%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/c0e414ab9c4747389766315633240cd0.png)

现在，我们已经大概知道了performance_schema中主要表的分类，但如何使用这些表来提供性能事件数据呢？

### 1.2.5.performance_schema简单配置与使用

当数据库初始化完成并启动时，并非所有的instruments（在采集配置项的配置表中，每一项都有一个开关字段，或为YES，或为NO）和consumers（与采集配置项类似，也有一个对应的事件类型保存表配置项，为YES表示对应的表保存性能数据，为NO表示对应的表不保存性能数据）都启用了，所以默认不会收集所有的事件。

可能你想检测的事件并没有打开，需要进行设置。可以使用如下两条语句打开对应的instruments和consumers，我们以配置监测等待事件数据为例进行说明。

打开等待事件的采集器配置项开关，需要修改setup_instruments 配置表中对应的采集器配置项。

```
update setup_instruments set enabled='yes',timed='yes' where name like 'wait%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/68d0e6b27f8b40fdbadc10a80f6c3028.png)

打开等待事件的保存表配置项开关，修改setup_consumers 配置表中对应的配置项。

```
update setup_consumers set enabled='yes' where name like 'wait%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/cd2e1dc3050042699c3558b7d1af3fa8.png)

配置好之后，我们就可以查看Server当前正在做什么了。可以通过查询events_waits_current表来得知，该表中每个线程只包含一行数据，用于显示每个线程的最新监视事件（正在做的事情）。

*_current表中每个线程只保留一条记录，且一旦线程完成工作，该表中就不会再记录该线程的事件信息了。*_history表中记录每个线程已经执行完成的事件信息，但每个线程的事件信息只记录10条，再多就会被覆盖掉。*_history_long表中记录所有线程的事件信息，但总记录数量是10000行，超过会被覆盖掉。

summary表提供所有事件的汇总信息。该组中的表以不同的方式汇总事件数据（如：按用户、按主机、按线程等汇总）。

### 1.2.6.查看最近执行失败的SQL语句

使用代码对数据库的某些操作（比如：使用Java的ORM框架操作数据库）报出语法错误，但是代码并没有记录SQL语句文本的功能，在MySQL数据库层能否查看到具体的SQL语句文本，看看是否哪里写错了？这个时候，大多数人首先想到的就是去查看错误日志。很遗憾，对于SQL语句的语法错误，错误日志并不会记录。

实际上，在performance_schema的语句事件记录表中针对每一条语句的执行状态都记录了较为详细的信息，例如：events_statements_表和events_statements_summary_by_digest表（events_statements_表记录了语句所有的执行错误信息，而events_statements_summary_by_digest表只记录了语句在执行过程中发生错误的语句记录统计信息，不记录具体的错误类型，例如：不记录语法错误类的信息）。下面看看如何使用这两个表查询语句发生错误的语句信息。

首先，我们模拟一条语法错误的SQL语句，使用events_statements_history_long表或events_statements_history表查询发生语法错误的SQL语句：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/0fcab44ff55b4854895797962e963355.png)

然后，查询events_statements_history表中错误号为1064的记录

```
select * from events_statements_history where mysql_errno=1064\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/dafdb43d13ed4d3e825317a617a2538b.png)

如果不知道错误号是多少，可以查询发生错误次数不为0的语句记录，在里边找到SQL_TEXT和MESSAGE_TEXT字段（提示信息为语法错误的就是它）。

### 1.2.7.查看最近的事务执行信息

我们可以通过慢查询日志查询到一条语句的执行总时长，但是如果数据库中存在着一些大事务在执行过程中回滚了，或者在执行过程中异常中止，这个时候慢查询日志就爱莫能助了，这时我们可以借助performance_schema的events_transactions_*表来查看与事务相关的记录，在这些表中详细记录了是否有事务被回滚、活跃（长时间未提交的事务也属于活跃事务）或已提交等信息。

首先需要进行配置启用，事务事件默认并未启用

```
update setup_instruments set enabled='yes',timed='yes' where name like 'transaction%';
```

```
update setup_consumers set enabled='yes' where name like '%transaction%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/3f31b531834042a1b066644ce601a56a.png)

现在我们开启一个新会话（会话2）用于执行事务，并模拟事务回滚。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/86a419601c0f49ad805e138a9ad3e717.png)

查询活跃事务，活跃事务表示当前正在执行的事务事件，需要从events_transactions_current表中查询。

下图中可以看到有一条记录，代表当前活跃的事务事件。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/ab315016c38642638c86e198c98fa8ed.png)

会话2中回滚事务：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/62cbcdea081e46a9b717ca366791756a.png)

查询事务事件当前表（events_transactions_current）和事务事件历史记录表（events_transactions_history）

可以看到在两表中都记录了一行事务事件信息，线程ID为30的线程执行了一个事务，事务状态为ROLLED BACK。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/483ff1b4df5d4f73a534940233c35764.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/b30e44b961c144f8b4014d9912634e6d.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/97d994505cf846c6bfd6277f2ac634f2.png)

但是当我们关闭会话2以后，事务事件当前表中（events_transactions_current）的记录就消失了。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/c1bbe1d2ccb041969cd413ee1fc1900f.png)

要查询的话需要去（events_transactions_history_long）表中查

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/06daa01a146a4982a1981154512798e6.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/8d5bcb8ecd9248fab1d003492b034523.png)

### 1.2.8.小结

当然performance_schema的用途不止我们上面说到过的这些，它还能提供比如查看SQL语句执行阶段和进度信息、MySQL集群下复制功能查看复制报错详情等等。

具体可以参考官网：[MySQL :: MySQL 5.7 Reference Manual :: 25 MySQL Performance Schema](https://dev.mysql.com/doc/refman/5.7/en/performance-schema.html)

## 1.3.sys系统库

### 1.3.1.sys使用须知

sys系统库支持MySQL 5.6或更高版本，不支持MySQL 5.5.x及以下版本。

sys系统库通常都是提供给专业的DBA人员排查一些特定问题使用的，其下所涉及的各项查询或多或少都会对性能有一定的影响。

因为sys系统库提供了一些代替直接访问performance_schema的视图，所以必须启用performance_schema（将performance_schema系统参数设置为ON），sys系统库的大部分功能才能正常使用。

同时要完全访问sys系统库，用户必须具有以下数据库的管理员权限。

如果要充分使用sys系统库的功能，则必须启用某些performance_schema的功能。比如：

启用所有的wait instruments：

```
CALL sys.ps_setup_enable_instrument('wait');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/79fb63778c8a4f7594b45794b9c561ba.png)

启用所有事件类型的current表：

```
CALL sys.ps_setup_enable_consumer('current');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/dbc412a1f0c7461aba4b51d1cf2a4646.png)

***注意：*** *performance_schema**的默认配置就可以满足**sys系统库的大部分数据收集功能。启用所有需要功能会对性能产生一定的影响，因此最好仅启用所需的配置。*

### 1.3.2.sys系统库使用

如果使用了USE语句切换默认数据库，那么就可以直接使用sys系统库下的视图进行查询，就像查询某个库下的表一样操作。也可以使用db_name.view_name、db_name.procedure_name、db_name.func_name等方式，在不指定默认数据库的情况下访问sys 系统库中的对象（这叫作名称限定对象引用）。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/ccf9203ed4f54d39877afaa606fab243.png)

在sys系统库下包含很多视图，它们以各种方式对performance_schema表进行聚合计算展示。这些视图大部分是成对出现的，两个视图名称相同，但有一个视图是带 x $前缀的.$

```
host_summary_by_file_io和 x$host_summary_by_file_io
```

代表按照主机进行汇总统计的文件I/O性能数据，两个视图访问的数据源是相同的，但是在创建视图的语句中，不带x$前缀的视图显示的是相关数值经过单位换算后的数据（单位是毫秒、秒、分钟、小时、天等），带 x$ 前缀的视图显示的是原始的数据（单位是皮秒）。![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/d2d5f73695264cb79cf2a736c0dada6f.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/d237312f75f94aa3ba0b9db5ed8c27bc.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/ef56a6efe7354676ab1f874243a05a7e.png)

### 1.3.3.查看慢SQL语句慢在哪里

如果我们频繁地在慢查询日志中发现某个语句执行缓慢，且在表结构、索引结构、统计信息中都无法找出原因时，则可以利用sys系统库中的撒手锏：sys.session视图结合performance_schema的等待事件来找出症结所在。那么session视图有什么用呢？使用它可以查看当前用户会话的进程列表信息，看看当前进程到底再干什么，注意，这个视图在MySQL 5.7.9中才出现。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/5689dd61485a4e4eb4bbacc5093a808c.png)

首先需要启用与等待事件相关功能：

```
call sys.ps_setup_enable_instrument('wait');
call sys.ps_setup_enable_consumer('wait');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/e3552b311f6f4f6b9eb2738f099c4c6c.png)

然后模拟一下：

一个session中执行

```
select sleep(30);
```

另外一个session中在sys库中查询：

```
select * from session where command='query' and conn_id !=connection_id()\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/f53ead8ab12c4f9ca9b8e71b6d8d3ba3.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/6985e3502daa497ca67046d4636800ff.png)

**查询表的增、删、改、查数据量和I/O耗时统计**

```
select * from schema_table_statistics_with_buffer\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/10330f9686954d368867a358eaa1eed4.png)

### 1.3.4.小结

除此之外，通过sys还可以查询查看InnoDB缓冲池中的热点数据、查看是否有事务锁等待、查看未使用的，冗余索引、查看哪些语句使用了全表扫描等等。

具体可以参考官网：[MySQL :: MySQL 5.7 Reference Manual :: 26 MySQL sys Schema](https://dev.mysql.com/doc/refman/5.7/en/sys-schema.html)

## 1.4.information_schema

### 1.4.1.什么是information_schema

information_schema提供了对数据库元数据、统计信息以及有关MySQL Server信息的访问（例如：数据库名或表名、字段的数据类型和访问权限等）。该库中保存的信息也可以称为MySQL的数据字典或系统目录。

在每个MySQL 实例中都有一个独立的information_schema，用来存储MySQL实例中所有其他数据库的基本信息。information_schema库下包含多个只读表（非持久表），所以在磁盘中的数据目录下没有对应的关联文件，且不能对这些表设置触发器。虽然在查询时可以使用USE语句将默认数据库设置为information_schema，但该库下的所有表是只读的，不能执行INSERT、UPDATE、DELETE等数据变更操作。

针对information_schema下的表的查询操作可以替代一些SHOW查询语句（例如：SHOW DATABASES、SHOW TABLES等）。

*注意：根据**MySQL**版本的不同，表的个数和存放是有所不同的。在**MySQL 5.6**版本中总共有**59**个表，在**MySQL 5.7**版本中，该**schema**下总共有**61**个表，*

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/3d96ac8b552f41998507457051e4a15f.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/fc6d1503e9f34f74ad5bf4e0165e3ae1.png)

*在**MySQL 8.0**版本中，该**schema**下的数据字典表（包含部分原**Memory**引擎临时表）都迁移到了**mysql schema**下，且在**mysql schema**下这些数据字典表被隐藏，无法直接访问，需要通过**information_schema**下的同名表进行访问。*

information_schema下的所有表使用的都是Memory和InnoDB存储引擎，且都是临时表，不是持久表，在数据库重启之后这些数据会丢失。在MySQL 的4个系统库中，information_schema也是唯一一个在文件系统上没有对应库表的目录和文件的系统库。

### 1.4.2.information_schema表分类

#### Server层的统计信息字典表

（1）COLUMNS

•　提供查询表中的列（字段）信息。

（2）KEY_COLUMN_USAGE

•　提供查询哪些索引列存在约束条件。

•　该表中的信息包含主键、唯一索引、外键等约束信息，例如：所在的库表列名、引用的库表列名等。该表中的信息与TABLE_CONSTRAINTS表中记录的信息有些类似，但TABLE_CONSTRAINTS表中没有记录约束引用的库表列信息，而KEY_COLUMN_USAGE表中却记录了TABLE_CONSTRAINTS表中所没有的约束类型。

（3）REFERENTIAL_CONSTRAINTS

•　提供查询关于外键约束的一些信息。

（4）STATISTICS

•　提供查询关于索引的一些统计信息，一个索引对应一行记录。

（5）TABLE_CONSTRAINTS

•　提供查询与表相关的约束信息。

（6）FILES

•　提供查询与MySQL的数据表空间文件相关的信息。

（7）ENGINES

•　提供查询MySQL Server支持的引擎相关信息。

（8）TABLESPACES

•　提供查询关于活跃表空间的相关信息（主要记录的是NDB存储引擎的表空间信息）。

•　注意：该表不提供有关InnoDB存储引擎的表空间信息。对于InnoDB表空间的元数据信息，请查询INNODB_SYS_TABLESPACES表和INNODB_SYS_DATAFILES表。另外，从MySQL 5.7.8开始，INFORMATION_SCHEMA.FILES表也提供查询InnoDB表空间的元数据信息。

（9）SCHEMATA

•　提供查询MySQL Server中的数据库列表信息，一个schema就代表一个数据库。

#### Server层的表级别对象字典表

（1）VIEWS

•　提供查询数据库中的视图相关信息。查询该表的账户需要拥有show view权限。

（2）TRIGGERS

•　提供查询关于某个数据库下的触发器相关信息。

（3）TABLES

•　提供查询与数据库内的表相关的基本信息。

（4）ROUTINES

•　提供查询关于存储过程和存储函数的信息（不包括用户自定义函数）。该表中的信息与mysql.proc中记录的信息相对应（如果该表中有值的话）。

（5）PARTITIONS

•　提供查询关于分区表的信息。

（6）EVENTS

•　提供查询与计划任务事件相关的信息。

（7）PARAMETERS

•　提供有关存储过程和函数的参数信息，以及有关存储函数的返回值信息。这些参数信息与mysql.proc表中的param_list列记录的内容类似。

#### Server层的混杂信息字典表

（1）GLOBAL_STATUS、GLOBAL_VARIABLES、SESSION_STATUS、

SESSION_VARIABLES

•　提供查询全局、会话级别的状态变量与系统变量信息。

（2）OPTIMIZER_TRACE

•　提供优化程序跟踪功能产生的信息。

•　跟踪功能默认是关闭的，使用optimizer_trace系统变量启用跟踪功能。如果开启该功能，则每个会话只能跟踪它自己执行的语句，不能看到其他会话执行的语句，且每个会话只能记录最后一条跟踪的SQL语句。

（3）PLUGINS

•　提供查询关于MySQL Server支持哪些插件的信息。

（4）PROCESSLIST

•　提供查询一些关于线程运行过程中的状态信息。

（5）PROFILING

•　提供查询关于语句性能分析的信息。其记录内容对应于SHOW PROFILES和SHOW PROFILE语句产生的信息。该表只有在会话变量 profiling=1时才会记录语句性能分析信息，否则该表不记录。

•　注意：从MySQL 5.7.2开始，此表不再推荐使用，在未来的MySQL版本中删除，改用Performance Schema代替。

（6）CHARACTER_SETS

•　提供查询MySQL Server支持的可用字符集。

（7）COLLATIONS

•　提供查询MySQL Server支持的可用校对规则。

（8）COLLATION_CHARACTER_SET_APPLICABILITY

•　提供查询MySQL Server中哪种字符集适用于什么校对规则。查询结果集相当于从SHOW COLLATION获得的结果集的前两个字段值。目前并没有发现该表有太大的作用。

（9）COLUMN_PRIVILEGES

•　提供查询关于列（字段）的权限信息，表中的内容来自mysql.column_priv列权限表（需要针对一个表的列单独授权之后才会有内容）。

（10）SCHEMA_PRIVILEGES

•　提供查询关于库级别的权限信息，每种类型的库级别权限记录一行信息，该表中的信息来自mysql.db表。

（11）TABLE_PRIVILEGES

•　提供查询关于表级别的权限信息，该表中的内容来自mysql.tables_priv表。

（12）USER_PRIVILEGES

•　提供查询全局权限的信息，该表中的信息来自mysql.user表。

10.2.4　InnoDB层的系统字典表

（1）INNODB_SYS_DATAFILES

•　提供查询InnoDB所有表空间类型文件的元数据（内部使用的表空间ID和表空间文件的路径信息），包括独立表空间、常规表空间、系统表空间、临时表空间和undo空间（如果开启了独立undo空间的话）。

•　该表中的信息等同于InnoDB数据字典内部SYS_DATAFILES表的信息。

（2）INNODB_SYS_VIRTUAL

•　提供查询有关InnoDB虚拟生成列和与之关联的列的元数据信息，等同于InnoDB数据字典内部SYS_VIRTUAL表的信息。该表中展示的行信息是与虚拟生成列相关联列的每个列的信息。

（3）INNODB_SYS_INDEXES

•　提供查询有关InnoDB索引的元数据信息，等同于InnoDB数据字典内部SYS_INDEXES表中的信息。

（4）INNODB_SYS_TABLES

•　提供查询有关InnoDB表的元数据信息，等同于InnoDB数据字典内部SYS_TABLES表的信息。

（5）INNODB_SYS_FIELDS

•　提供查询有关InnoDB索引键列（字段）的元数据信息，等同于InnoDB数据字典内部SYS_FIELDS表的信息。

（6）INNODB_SYS_TABLESPACES

•　提供查询有关InnoDB独立表空间和普通表空间的元数据信息（也包含了全文索引表空间），等同于InnoDB数据字典内部SYS_TABLESPACES表的信息。

（7）INNODB_SYS_FOREIGN_COLS

•　提供查询有关InnoDB外键列的状态信息，等同于InnoDB数据字典内部

SYS_FOREIGN_COLS表的信息。

（8）INNODB_SYS_COLUMNS

•　提供查询有关InnoDB表列的元数据信息，等同于InnoDB数据字典内部

SYS_COLUMNS表的信息。

（9）INNODB_SYS_FOREIGN

•　提供查询有关InnoDB外键的元数据信息，等同于InnoDB数据字典内部SYS_FOREIGN表的信息。

（10）INNODB_SYS_TABLESTATS

•　提供查询有关InnoDB表的较低级别的状态信息视图。 MySQL优化器会使用这些统计信息数据来计算并确定在查询InnoDB表时要使用哪个索引。这些信息保存在内存中的数据结构中，与存储在磁盘上的数据无对应关系。在InnoDB内部也无对应的系统表。

#### InnoDB层的锁、事务、统计信息字典表

（1）INNODB_LOCKS

•　提供查询InnoDB引擎中事务正在请求的且同时被其他事务阻塞的锁信息（即没有发生不同事务之间锁等待的锁信息，在这里是查看不到的。例如，当只有一个事务时，无法查看到该事务所加的锁信息）。该表中的内容可用于诊断高并发下的锁争用信息。

（2）INNODB_TRX

•　提供查询当前在InnoDB引擎中执行的每个事务（不包括只读事务）的信息，包括事务是否正在等待锁、事务什么时间点开始，以及事务正在执行的SQL语句文本信息等（如果有SQL语句的话）。

（3）INNODB_BUFFER_PAGE_LRU

•　提供查询缓冲池中的页面信息。与INNODB_BUFFER_PAGE表不同，INNODB_BUFFER_PAGE_LRU表保存有关InnoDB缓冲池中的页如何进入LRU链表，以及在缓冲池不够用时确定需要从中逐出哪些页的信息。

（4）INNODB_LOCK_WAITS

•　提供查询InnoDB事务的锁等待信息。如果查询该表为空，则表示无锁等待信息；如果查询该表中有记录，则说明存在锁等待，表中的每一行记录表示一个锁等待关系。在一个锁等待关系中包含：一个等待锁（即，正在请求获得锁）的事务及其正在等待的锁等信息、一个持有锁（这里指的是发生锁等待事务正在请求的锁）的事务及其所持有的锁等信息。

（5）INNODB_TEMP_TABLE_INFO

•　提供查询有关在InnoDB实例中当前处于活动状态的用户（只对已建立连接的用户有效，断开的用户连接对应的临时表会被自动删除）创建的InnoDB临时表的信息。它不提供查询优化器使用的内部InnoDB临时表的信息。该表在首次查询时创建。

（6）INNODB_BUFFER_PAGE

•　提供查询关于缓冲池中的页相关信息。

（7）INNODB_METRICS

•　提供查询InnoDB更为详细的性能信息，是对InnoDB的performance_schema的补充。通过对该表的查询，可用于检查InnoDB的整体健康状况，也可用于诊断性能瓶颈、资源短缺和应用程序的问题等。

（8）INNODB_BUFFER_POOL_STATS

•　提供查询一些InnoDB缓冲池中的状态信息，该表中记录的信息与SHOW ENGINEINNODB STATUS语句输出的缓冲池统计部分信息类似。另外，InnoDB缓冲池的一些状态变量也提供了部分相同的值。

#### InnoDB层的全文索引字典表

（1）INNODB_FT_CONFIG

（2）INNODB_FT_BEING_DELETED

（3）INNODB_FT_DELETED

（4）INNODB_FT_DEFAULT_STOPWORD

（5）INNODB_FT_INDEX_TABLE

#### InnoDB层的压缩相关字典表

（1）INNODB_CMP和INNODB_CMP_RESET

•　这两个表中的数据包含了与压缩的InnoDB表页有关的操作状态信息。表中记录的数据为测量数据库中的InnoDB表压缩的有效性提供参考。

（2）INNODB_CMP_PER_INDEX和INNODB_CMP_PER_INDEX_RESET

•　这两个表中记录了与InnoDB压缩表数据和索引相关的操作状态信息，对数据库、表、索引的每个组合使用不同的统计信息，以便为评估特定表的压缩性能和实用性提供参考数据。

（3）INNODB_CMPMEM和INNODB_CMPMEM_RESET

•　这两个表中记录了InnoDB缓冲池中压缩页的状态信息，为测量数据库中InnoDB表压缩的有效性提供参考。

### 1.4.3.information_schema应用

**查看索引列的信息**

INNODB_SYS_FIELDS表提供查询有关InnoDB索引列（字段）的元数据信息，等同于InnoDB数据字典中SYS_FIELDS表的信息。

INNODB_SYS_INDEXES表提供查询有关InnoDB索引的元数据信息，等同于InnoDB数据字典内部SYS_INDEXES表中的信息。

INNODB_SYS_TABLES表提供查询有关InnoDB表的元数据信息，等同于InnoDB数据字典中SYS_TABLES表的信息。

假设需要查询lijin库下的InnoDB表order_exp的索引列名称、组成和索引列顺序等相关信息，

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/65e7a8e3d45a42908ac2d406a47b231d.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/ce9e5c8012de43fdade63467de2c041f.png)

则可以使用如下SQL语句进行查询

```
SELECT
	t. NAME AS d_t_name,
	i. NAME AS i_name,
	i.type AS i_type,
	i.N_FIELDS AS i_column_numbers,
	f. NAME AS i_column_name,
	f.pos AS i_position
FROM
	INNODB_SYS_TABLES AS t
JOIN INNODB_SYS_INDEXES AS i ON t.TABLE_ID = i.TABLE_ID
LEFT JOIN INNODB_SYS_FIELDS AS f ON i.INDEX_ID = f.INDEX_ID
WHERE
	t. NAME = 'lijin/order_exp';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/c6946f02fdef4aed8e61cc6298a91f6e.png)

结果中的列都很好理解，唯一需要额外解释的是i_type(INNODB_SYS_INDEXES.type)，它是表示索引类型的数字ID：

0 =二级索引

1=集群索引

2 =唯一索引

3 =主键索引

32 =全文索引

64 =空间索引

128 =包含虚拟生成列的二级索引。

## 1.5.Mysql中mysql系统库

### 1.5.1.权限系统表

因为权限管理是DBA的职责，所以对于这个部分的表，我们大概了解下即可。在mysql系统库中，MySQL访问权限系统表，放在mysql库中，主要包含如下几个表。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/db19892e12104e04bb0f46161e54f2cd.png)

•　user：包含用户账户、全局权限和其他非权限列表（安全配置字段和资源控制字段）。

•　db：数据库级别的权限表。该表中记录的权限信息代表用户是否可以使用这些权限来访问被授予访问的数据库下的所有对象（表或存储程序）。

•　tables_priv：表级别的权限表。

•　columns_priv：字段级别的权限表。

•　procs_priv：存储过程和函数权限表。

•　proxies_priv：代理用户权限表。

**提示：**

**要更改权限表的内容，应该使用账号管理语句（如：**  **CREATE USER**  **、**  **GRANT**  **、** **REVOKE****等）来间接修改，不建议直接使用****DML语句修改权限表。**

(grant，revoke语句执行后会变更权限表中相关记录，同时会更新内存中记录用户权限的相关对象。dml语句直接修改权限表只是修改了表中权限信息，需要执行flush privileges;来更新内存中保存用户权限的相关对象)

### 1.5.2.统计信息表

持久化统计功能是通过将内存中的统计数据存储到磁盘中，使其在数据库重启时可以快速重新读入这些统计信息而不用重新执行统计，从而使得查询优化器可以利用这些持久化的统计信息准确地选择执行计划（如果没有这些持久化的统计信息，那么数据库重启之后内存中的统计信息将会丢失，下一次访问到某库某表时，需要重新计算统计信息，并且重新计算可能会因为估算值的差异导致查询计划发生变更，从而导致查询性能发生变化）。

如何启用统计信息的持久化功能呢？当innodb_stats_persistent = ON时全局的开启统计信息的持久化功能，默认是开启的，

```
show variables like 'innodb_stats_persistent';
```

如果要单独关闭某个表的持久化统计功能，则可以通过ALTER TABLE tbl_name STATS_PERSISTENT = 0语句来修改。

#### 1.5.2.1.innodb_table_stats

innodb_table_stats表提供查询与表数据相关的统计信息。

```
select * from innodb_table_stats where table_name = 'order_exp'\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/41df5d177b2a4d038f0a85e8178b9c6d.png)

database_name：数据库名称。

•　table_name：表名、分区名或子分区名。

•　last_update：表示InnoDB上次更新统计信息行的时间。

•　n_rows：表中的估算数据记录行数。

•　clustered_index_size：主键索引的大小，以页为单位的估算数值。

•　sum_of_other_index_sizes：其他（非主键）索引的总大小，以页为单位的估算数值。

#### 1.5.2.2.innodb_index_stats

innodb_index_stats表提供查询与索引相关的统计信息。

```
select * from innodb_index_stats where table_name = 'order_exp';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/b7dd7aa5f1ad4ef0a9735e9b6acf3bb6.png)

表字段含义如下。

•　database_name：数据库名称。

•　table_name：表名、分区表名、子分区表名。

•　index_name：索引名称。

•　last_update：表示InnoDB上次更新统计信息行的时间。

•　stat_name：统计信息名称，其对应的统计信息值保存在stat_value字段中。

•　stat_value：保存统计信息名称stat_name字段对应的统计信息值。

•　sample_size：stat_value字段中提供的统计信息估计值的采样页数。

•　stat_description：统计信息名称stat_name字段中指定的统计信息的说明。

从表的查询数据中可以看到：

•　stat_name字段一共有如下几个统计值。

■　size：当stat_name字段为size值时，stat_value字段值表示索引中的总页数量。

■　n_leaf_pages：当stat_name字段为n_leaf_pages值时，stat_value字段值表示索引叶子页的数量。

■　n_diff_pfxNN：NN代表数字（例如01、02等）。当stat_name字段为n_diff_pfxNN值时，stat_value字段值表示索引的first column（即索引的最前索引列，从索引定义顺序的第一个列开始）列的唯一值数量。例如：当NN为01时，stat_value字段值就表示索引的第一个列的唯一值数量；当NN为02时，stat_value字段值就表示索引的第一个和第二个列组合的唯一值数量，依此类推。此外，在stat_name = n_diff_pfxNN的情况下，stat_description字段显示一个以逗号分隔的计算索引统计信息字段的列表。

•　从index_name字段值为PRIMARY数据行的stat_description字段的描述信息“id”中可以看出，主键索引的统计信息只包括创建主键索引时显式指定的列。

•　从index_name字段值为u_idx_day_status数据行的stat_description字段的描述信息“insert_time,order_status,expire_time”中可以看出，唯一索引的统计信息只包括创建唯一索引时显式指定的列。

•　从index_name字段值为idx_order_no数据行的stat_description字段的描述信息“order_no,id”中可以看出，普通索引（非唯一的辅助索引）的统计信息包括了显式定义的列和主键列。

**注意，上述的描述中出现的诸如叶子页，索引的最前索引列等等，这些东西在索引章节有讲解，这里不再阐述。**

### 1.5.3.日志记录表

MySQL的日志系统包含：普通查询日志、慢查询日志、错误日志（记录服务器启动时、运行中、停止时的错误信息）、二进制日志（记录服务器运行过程中数据变更的逻辑日志）、中继日志（记录从库I/O线程从主库获取的主库数据变更日志）、DDL日志（记录DDL语句执行时的元数据变更信息。在MySQL 5.7中只支持写入文件中，在MySQL 8.0中支持写入innodb_ddl_log表中。在MySQL5.7中，只有普通查询日志、慢查询日志支持写入表中（也支持写入文件中）,可以通过log_output=TABLE设置保存到mysql.general_log表和mysql.slow_log表中，其他日志类型在MySQL 5.7中只支持写入文件中。

#### 1.5.3.1. general_log

general_log表提供查询普通SQL语句的执行记录信息，用于查看客户端到底在服务器上执行了什么SQL语句。

缺省不开启

```
show variables like 'general_log';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/ec13306f833e4042b181e836c24583a1.png)

开启

```
set global log_output='TABLE'; -- 'TABLE,FILE'表示同时输出到表和文件
set global general_log=on;
show variables like 'general_log';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/cc4939b34fa14982b4e17e6792a3dcf9.png)

任意执行一个查询后

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/cb17df7fd051446789d55f09c7745e67.png)

```
select * from mysql.general_log\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/70c0912dbc7d41afb8d860432a9e745a.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/dd5f480d5e3c426c9ea960a8c9d608c9.png)

#### 1.5.3.2. slow_log

slow_log表提供查询执行时间超过long_query_time设置值的SQL语句、未使用索引的语句（需要开启参数log_queries_not_using_indexes=ON）或者管理语句（需要开启参数log_slow_admin_statements=ON）。

```
show variables like 'log_queries_not_using_indexes';
show variables like 'log_slow_admin_statements';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/3564d84a6ff544aa8c4afadd7dbc60cb.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/4a71765fcef640c2a48d552dc70774c0.png)

开启

```
set global log_queries_not_using_indexes=on;
set global log_slow_admin_statements=on;
show variables like 'log_queries_not_using_indexes';
show variables like 'log_slow_admin_statements';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/6f2c5bb7c0b94324b88231c480c08605.png)

我们已经知道慢查询日志可以帮助定位可能存在问题的SQL语句，从而进行SQL语句层面的优化。但是默认值为关闭的，需要我们手动开启。

```
show VARIABLES like 'slow_query_log';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1651212459071/f72a83180181494fa68d4f014375127b.png)

```
set GLOBAL slow_query_log=1;
```

开启1，关闭0

但是多慢算慢？MySQL中可以设定一个阈值，将运行时间超过该值的所有SQL语句都记录到慢查询日志中。long_query_time参数就是这个阈值。默认值为10，代表10秒。

```
show VARIABLES like '%long_query_time%';
```

当然也可以设置

```
set global long_query_time=0;
```

默认10秒，这里为了演示方便设置为0

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/d43357ae215c4ee8b1e3fee0d069f6bf.png)

然后我们测试一把，随便写一个SQL

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/2b03256bb14c4345bfede999e8be3639.png)

```
select * from mysql.slow_log\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/b20b773478584320a6e6649cc7a8f0bd.png)

### 1.5.4.InnoDB中的统计数据

我们前边唠叨查询成本的时候经常用到一些统计数据，比如通过SHOW TABLE STATUS可以看到关于表的统计数据，通过SHOW INDEX可以看到关于索引的统计数据，那么这些统计数据是怎么来的呢？它们是以什么方式收集的呢？

#### 1.5.4.1 统计数据存储方式

InnoDB提供了两种存储统计数据的方式：

永久性的统计数据，这种统计数据存储在磁盘上，也就是服务器重启之后这些统计数据还在。

非永久性的统计数据，这种统计数据存储在内存中，当服务器关闭时这些这些统计数据就都被清除掉了，等到服务器重启之后，在某些适当的场景下才会重新收集这些统计数据。

MySQL给我们提供了系统变量innodb_stats_persistent来控制到底采用哪种方式去存储统计数据。在MySQL 5.6.6之前，innodb_stats_persistent的值默认是OFF，也就是说InnoDB的统计数据默认是存储到内存的，之后的版本中innodb_stats_persistent的值默认是ON，也就是统计数据默认被存储到磁盘中。

```
SHOW VARIABLES LIKE 'innodb_stats_persistent';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/cb07fc2592a04f0db993cb4122628605.png)

不过最近的MySQL版本都基本不用基于内存的非永久性统计数据了，所以我们也就不深入研究。

不过InnoDB默认是以表为单位来收集和存储统计数据的，也就是说我们可以把某些表的统计数据（以及该表的索引统计数据）存储在磁盘上，把另一些表的统计数据存储在内存中。怎么做到的呢？我们可以在创建和修改表的时候通过指定STATS_PERSISTENT属性来指明该表的统计数据存储方式：

CREATE TABLE 表名 (...)
Engine=InnoDB, STATS_PERSISTENT = (1|0);

ALTER TABLE 表名
Engine=InnoDB, STATS_PERSISTENT = (1|0);

当STATS_PERSISTENT=1时，表明我们想把该表的统计数据永久的存储到磁盘上，当STATS_PERSISTENT=0时，表明我们想把该表的统计数据临时的存储到内存中。如果我们在创建表时未指定STATS_PERSISTENT属性，那默认采用系统变量innodb_stats_persistent的值作为该属性的值。

#### 1.5.4.2 基于磁盘的永久性统计数据

当我们选择把某个表以及该表索引的统计数据存放到磁盘上时，实际上是把这些统计数据存储到了两个表里：

```
SHOW TABLES FROM mysql LIKE 'innodb%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/1496f23b39ed49ab8aa3cada28590022.png)

可以看到，这两个表都位于mysql系统数据库下边，其中：

innodb_table_stats存储了关于表的统计数据，每一条记录对应着一个表的统计数据。

innodb_index_stats存储了关于索引的统计数据，每一条记录对应着一个索引的一个统计项的统计数据。

**innodb_table_stats**

直接看一下这个innodb_table_stats表中的各个列都是干嘛的：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/a32ca7133e7d43e191e9ec85230def82.png)

database_name       数据库名

table_name       表名

last_update       本条记录最后更新时间

n_rows表中记录的条数

clustered_index_size       表的聚簇索引占用的页面数量

sum_of_other_index_sizes   表的其他索引占用的页面数量

我们直接看一下这个表里的内容：

```
SELECT * FROM mysql.innodb_table_stats;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/e9f1f31332c5441987df16202f3e38cf.png)

几个重要统计信息项的值如下：

n_rows的值是10350，表明order_exp表中大约有10350条记录，注意这个数据是估计值。

clustered_index_size的值是97，表明order_exp表的聚簇索引占用97个页面，这个值是也是一个估计值。

sum_of_other_index_sizes的值是81，表明order_exp表的其他索引一共占用81个页面，这个值是也是一个估计值。

##### n_rows统计项的收集

InnoDB统计一个表中有多少行记录是这样的：

按照一定算法（并不是纯粹随机的）选取几个叶子节点页面，计算每个页面中主键值记录数量，然后计算平均一个页面中主键值的记录数量乘以全部叶子节点的数量就算是该表的n_rows值。

可以看出来这个n_rows值精确与否取决于统计时采样的页面数量，MySQL用名为innodb_stats_persistent_sample_pages的系统变量来控制使用永久性的统计数据时，计算统计数据时采样的页面数量。该值设置的越大，统计出的n_rows值越精确，但是统计耗时也就最久；该值设置的越小，统计出的n_rows值越不精确，但是统计耗时特别少。所以在实际使用是需要我们去权衡利弊，该系统变量的默认值是20。

InnoDB默认是以表为单位来收集和存储统计数据的，我们也可以单独设置某个表的采样页面的数量，设置方式就是在创建或修改表的时候通过指定STATS_SAMPLE_PAGES属性来指明该表的统计数据存储方式：

CREATE TABLE 表名 (...)
Engine=InnoDB, STATS_SAMPLE_PAGES = 具体的采样页面数量;

ALTER TABLE 表名
Engine=InnoDB, STATS_SAMPLE_PAGES = 具体的采样页面数量;

如果我们在创建表的语句中并没有指定STATS_SAMPLE_PAGES属性的话，将默认使用系统变量innodb_stats_persistent_sample_pages的值作为该属性的值。

clustered_index_size和sum_of_other_index_sizes统计项的收集牵涉到很具体的InnoDB表空间的知识和存储页面数据的细节，我们就不深入讲解了。

##### innodb_index_stats

直接看一下这个innodb_index_stats表中的各个列都是干嘛的：

```
desc mysql.innodb_index_stats;
```

字段名描述

database_name       数据库名

table_name       表名

index_name      索引名

last_update       本条记录最后更新时间

stat_name  统计项的名称

stat_value   对应的统计项的值

sample_size       为生成统计数据而采样的页面数量

stat_description       对应的统计项的描述

innodb_index_stats表的每条记录代表着一个索引的一个统计项。可能这会大家有些懵逼这个统计项到底指什么，别着急，我们直接看一下关于order_exp表的索引统计数据都有些什么：

```
SELECT * FROM mysql.innodb_index_stats WHERE table_name = 'order_exp';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/7b1f47ba02cd45ee9dc10c27e067f3d5.png)

先查看index_name列，这个列说明该记录是哪个索引的统计信息，从结果中我们可以看出来，PRIMARY索引（也就是主键）占了3条记录，idx_expire_time索引占了6条记录。

针对index_name列相同的记录，stat_name表示针对该索引的统计项名称，stat_value展示的是该索引在该统计项上的值，stat_description指的是来描述该统计项的含义的。我们来具体看一下一个索引都有哪些统计项：

n_leaf_pages：表示该索引的叶子节点占用多少页面。

size：表示该索引共占用多少页面。

n_diff_pfxNN：表示对应的索引列不重复的值有多少。其中的NN长得有点儿怪呀，啥意思呢？

其实NN可以被替换为01、02、03... 这样的数字。比如对于u_idx_day_status来说：

n_diff_pfx01表示的是统计insert_time这单单一个列不重复的值有多少。

n_diff_pfx02表示的是统计insert_time,order_status这两个列组合起来不重复的值有多少。

n_diff_pfx03表示的是统计insert_time,order_status,expire_time这三个列组合起来不重复的值有多少。

n_diff_pfx04表示的是统计key_pare1、key_pare2、expire_time、id这四个列组合起来不重复的值有多少。

对于普通的二级索引，并不能保证它的索引列值是唯一的，比如对于idx_order_no来说，key1列就可能有很多值重复的记录。此时只有在索引列上加上主键值才可以区分两条索引列值都一样的二级索引记录。

对于主键和唯一二级索引则没有这个问题，它们本身就可以保证索引列值的不重复，所以也不需要再统计一遍在索引列后加上主键值的不重复值有多少。比如u_idx_day_statu和idx_order_no。

在计算某些索引列中包含多少不重复值时，需要对一些叶子节点页面进行采样，sample_size列就表明了采样的页面数量是多少。

对于有多个列的联合索引来说，采样的页面数量是：innodb_stats_persistent_sample_pages × 索引列的个数。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/bacfa088408a46a5928ff6aff7363477.png)

当需要采样的页面数量大于该索引的叶子节点数量的话，就直接采用全表扫描来统计索引列的不重复值数量了。所以大家可以在查询结果中看到不同索引对应的size列的值可能是不同的。

##### 定期更新统计数据

随着我们不断的对表进行增删改操作，表中的数据也一直在变化，innodb_table_stats和innodb_index_stats表里的统计数据也在变化。MySQL提供了如下两种更新统计数据的方式：

###### 开启innodb_stats_auto_recalc。

系统变量innodb_stats_auto_recalc决定着服务器是否自动重新计算统计数据，它的默认值是ON，也就是该功能默认是开启的。每个表都维护了一个变量，该变量记录着对该表进行增删改的记录条数，如果发生变动的记录数量超过了表大小的10%，并且自动重新计算统计数据的功能是打开的，那么服务器会重新进行一次统计数据的计算，并且更新innodb_table_stats和innodb_index_stats表。不过自动重新计算统计数据的过程是异步发生的，也就是即使表中变动的记录数超过了10%，自动重新计算统计数据也不会立即发生，可能会延迟几秒才会进行计算。

再一次强调，InnoDB默认是以表为单位来收集和存储统计数据的，我们也可以单独为某个表设置是否自动重新计算统计数的属性，设置方式就是在创建或修改表的时候通过指定STATS_AUTO_RECALC属性来指明该表的统计数据存储方式：

CREATE TABLE 表名 (...)
Engine=InnoDB, STATS_AUTO_RECALC = (1|0);

ALTER TABLE 表名
Engine=InnoDB, STATS_AUTO_RECALC = (1|0);

当STATS_AUTO_RECALC=1时，表明我们想让该表自动重新计算统计数据，当STATS_AUTO_RECALC=0时，表明不想让该表自动重新计算统计数据。如果我们在创建表时未指定STATS_AUTO_RECALC属性，那默认采用系统变量innodb_stats_auto_recalc的值作为该属性的值。

###### 手动调用ANALYZE TABLE语句来更新统计信息

如果innodb_stats_auto_recalc系统变量的值为OFF的话，我们也可以手动调用ANALYZE
TABLE语句来重新计算统计数据，比如我们可以这样更新关于order_exp表的统计数据：

```
ANALYZE TABLE order_exp;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1654392842080/dd63ab7e994e430c9c22e30a9e26d29d.png)

ANALYZE TABLE语句会立即重新计算统计数据，也就是这个过程是同步的，在表中索引多或者采样页面特别多时这个过程可能会特别慢最好在业务不是很繁忙的时候再运行。

###### 手动更新innodb_table_stats和innodb_index_stats表

其实innodb_table_stats和innodb_index_stats表就相当于一个普通的表一样，我们能对它们做增删改查操作。这也就意味着我们可以手动更新某个表或者索引的统计数据。比如说我们想把order_exp表关于行数的统计数据更改一下可以这么做：

步骤一：更新innodb_table_stats表。

步骤二：让MySQL查询优化器重新加载我们更改过的数据。

更新完innodb_table_stats只是单纯的修改了一个表的数据，需要让MySQL查询优化器重新加载我们更改过的数据，运行下边的命令就可以了：

```

```

FLUSH TABLE order_exp;

# 1. MySQL的执行原理

## 1.1.单表访问之索引合并

我们前边说过MySQL在一般情况下执行一个查询时最多只会用到单个二级索引，但存在有特殊情况，在这些特殊情况下也可能在一个查询中使用到多个二级索引，MySQL中这种使用到多个索引来完成一次查询的执行方法称之为：**索引合并/index merge**，具体的索引合并算法有下边三种。

### 1.1.1.Intersection合并

Intersection翻译过来的意思是交集。这里是说某个查询可以使用多个二级索引，将从多个二级索引中查询到的结果取交集，比方说下边这个查询：

```
SELECT * FROM order_exp WHERE order_no = 'a' AND expire_time = 'b';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/cc53b73663344fb8a82497e2b4d9de15.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/ee4f4d1814e7456aadd55a9844b5e30a.png)

假设这个查询使用Intersection合并的方式执行的话，那这个过程就是这样的：

* 从idx_order_no二级索引对应的B+树中取出order_no='a'的相关记录。
* 从idx_expire_time二级索引对应的B+树中取出expire_time='b'的相关记录。

二级索引的记录都是由索引列 + 主键构成的，所以我们可以计算出这两个结果集中id值的交集。

按照上一步生成的id值列表进行回表操作，也就是从聚簇索引中把指定id值的完整用户记录取出来，返回给用户。

为啥不直接使用idx_order_no或者idx_expire_time只根据某个搜索条件去读取一个二级索引，然后回表后再过滤另外一个搜索条件呢？这里要分析一下两种查询执行方式之间需要的成本代价。

**只读取一个二级索引的成本：**

1.按照某个搜索条件读取一个二级索引

2.根据从该二级索引得到的主键值进行回表操作

3.然后再过滤其他的搜索条件

**读取多个二级索引之后取交集成本：**

1.按照不同的搜索条件分别读取不同的二级索引

2.将从多个二级索引得到的主键值取交集

3.最后根据主键值进行回表操作。

虽然读取多个二级索引比读取一个二级索引消耗性能，但是大部分情况下读取二级索引的操作是顺序I/O，而回表操作是随机I/O，所以如果只读取一个二级索引时需要回表的记录数特别多，而读取多个二级索引之后取交集的记录数非常少，当节省的因为回表而造成的性能损耗比访问多个二级索引带来的性能损耗更高时，读取多个二级索引后取交集比只读取一个二级索引的成本更低。

**所以MySQL在某些特定的情况下才可能会使用到Intersection索引合并，哪些情况呢？**

#### 1.1.1.1.等值匹配

**二级索引列必须是等值匹配的情况**

**对于联合索引来说，在联合索引中的每个列都必须等值匹配，不能出现只匹配部分列的情况。**

而下边这两个查询就不能进行Intersection索引合并：

```
SELECT * FROM order_exp WHERE order_no> 'a' AND expire_time = 'a' 
```

```
SELECT * FROM order_exp WHERE order_no = 'a' AND insert_time = 'a';
```

第一个查询是因为对order_no进行了范围匹配

第二个查询是因为insert_time使用到的联合索引u_idx_day_status中的order_status和expire_time列并没有出现在搜索条件中，所以这两个查询不能进行Intersection索引合并。

#### 1.1.1.2.主键列可以是范围匹配

比方说下边这个查询可能用到主键和u_idx_day_status进行Intersection索引合并的操作：

```
SELECT * FROM order_exp WHERE id > 100 AND expire_time = 'a';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/6df36e7ef5b74c1088368a811f4ca915.png)

因为主键的索引是有序的，按照有序的主键值去回表取记录有个专有名词，叫：Rowid Ordered Retrieval，简称 **ROR** 。

而二级索引的用户记录是由索引列 + 主键构成的，所以根据范围匹配出来的主键就是乱序的，导致回表开销很大。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/0f487092ac4c49fbaf3167b51b2ce71f.png)

那为什么在二级索引列都是等值匹配的情况下也可能使用Intersection索引合并，是因为只有在这种情况下根据二级索引查询出的结果集是按照主键值排序的。

Intersection索引合并会把从多个二级索引中查询出的主键值求交集，如果从各个二级索引中查询的到的结果集本身就是已经按照主键排好序的，那么求交集的过程就很容易。

当然，上边说的两种情况只是发生Intersection索引合并的必要条件，不是充分条件。也就是说即使符合Intersection的条件，也不一定发生Intersection索引合并，这得看优化器的心情（判断）。

优化器只有在单独根据搜索条件从某个二级索引中获取的记录数太多，导致回表开销太大，而通过Intersection索引合并后需要回表的记录数大大减少时才会使用Intersection索引合并。

### 1.1.2.Union合并

我们在写查询语句时经常想把既符合某个搜索条件的记录取出来，也把符合另外的某个搜索条件的记录取出来，我们说这些不同的搜索条件之间是OR关系。有时候OR关系的不同搜索条件会使用到不同的索引，比方说这样：

```
SELECT * FROM order_exp WHERE order_no = 'a' OR expire_time = 'b'
```

Intersection是交集的意思，这适用于使用不同索引的搜索条件之间使用AND连接起来的情况；Union是并集的意思，适用于使用不同索引的搜索条件之间使用OR连接起来的情况。与Intersection索引合并类似，MySQL在某些特定的情况下才可能会使用到Union索引合并：

#### 1.1.2.1.等值匹配

分析同Intersection合并

#### 1.1.2.2.主键列可以是范围匹配

分析同Intersection合并

#### 1.1.1.3.使用Intersection索引合并的搜索条件

就是搜索条件的某些部分使用Intersection索引合并的方式得到的主键集合和其他方式得到的主键集合取交集，比方说这个查询：

```
SELECT * FROM order_exp WHERE insert_time = 'a' AND order_status = 'b' AND expire_time = 'c'
OR (order_no = 'a' AND expire_time = 'b');
```

优化器可能采用这样的方式来执行这个查询：

1、先按照搜索条件order_no = 'a' AND expire_time = 'b'从索引idx_order_no和idx_expire_time中使用Intersection索引合并的方式得到一个主键集合。

2、再按照搜索条件 insert_time ='a' AND order_status = 'b' AND expire_time = 'c'从联合索引u_idx_day_status中得到另一个主键集合。

3、采用Union索引合并的方式把上述两个主键集合取并集，然后进行回表操作，将结果返回给用户。

当然，查询条件符合了这些情况也不一定就会采用Union索引合并，也得看优化器的心情。优化器只有在单独根据搜索条件从某个二级索引中获取的记录数比较少，通过Union索引合并后进行访问的代价比全表扫描更小时才会使用Union索引合并。

### 1.1.3.Sort-Union合并

Union索引合并的使用条件太苛刻，必须保证各个二级索引列在进行等值匹配的条件下才可能被用到，比方说下边这个查询就无法使用到Union索引合并：

```
SELECT * FROM order_exp WHERE order_no< 'a' OR expire_time> 'z'
```

这是因为根据order_no&#x3c;'a'从idx_order_no索引中获取的二级索引记录的主键值不是排好序的，

同时根据expire_time> 'z'从idx_expire_time索引中获取的二级索引记录的主键值也不是排好序的，但是order_no&#x3c; 'a'和expire_time> 'z''这两个条件又特别让我们动心，所以我们可以这样：

1、先根据order_no&#x3c; 'a'条件从idx_order_no二级索引中获取记录，并按照记录的主键值进行排序

2、再根据expire_time>'z'条件从idx_expire_time二级索引中获取记录，并按照记录的主键值进行排序

3、因为上述的两个二级索引主键值都是排好序的，剩下的操作和Union索引合并方式就一样了。

上述这种先按照二级索引记录的主键值进行排序，之后按照Union索引合并方式执行的方式称之为Sort-Union索引合并，很显然，这种Sort-Union索引合并比单纯的Union索引合并多了一步对二级索引记录的主键值排序的过程。

当然，查询条件符合了这些情况也不一定就会采用Sort-Union索引合并，也得看优化器的心情。优化器只有在单独根据搜索条件从某个二级索引中获取的记录数比较少，通过Sort-Union索引合并后进行访问的代价比全表扫描更小时才会使用Sort-Union索引合并。

### 1.1.4.联合索引替代Intersection索引合并

```
SELECT * FROM order_exp WHERE order_no= 'a' And expire_time= 'z';
```

这个查询之所以可能使用Intersection索引合并的方式执行，还不是因为idx_order_no和idx_expire_time是两个单独的B+树索引，要是把这两个列搞一个联合索引，那直接使用这个联合索引就把事情搞定了，何必用啥索引合并呢，就像这样：

```
ALTER TABLE order_exp drop index idx_order_no;
ALTER TABLE order_exp drop idx_expire_time;
ALTER TABLE add index idx_order_no_expire_time(order_no,expire_time);
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/1b443b74c0a14d96b1882bc427f20470.png)

这样我们把idx_order_no, idx_expire_time都干掉，再添加一个联合索引idx_order_no_expire_time，使用这个联合索引进行查询简直是又快又好，既不用多读一棵B+树，也不用合并结果。

## 1.2.连接查询

搞数据库一个避不开的概念就是Join，翻译成中文就是连接。使用的时候常常陷入下边两种误区：

**误区一：**业务至上，管他三七二十一，再复杂的查询也用在一个连接语句中搞定。

**误区二：**敬而远之，上次慢查询就是因为使用了连接导致的，以后再也不敢用了。

所以我们来学习一下连接的原理，才能在工作中用好SQL连接。

### 1.2.1.连接简介

#### 1.2.1.1.连接的本质

为了方便讲述，我们建立两个简单的演示表并给它们写入数据：

```
CREATE TABLE e1 (m1 int, n1 char(1));
CREATE TABLE e2 (m2 int, n2 char(1));
INSERT INTO e1 VALUES(1, 'a'), (2, 'b'), (3, 'c');
INSERT INTO e2 VALUES(2, 'b'), (3, 'c'), (4, 'd');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/b6fc97d7960a4907b7a74140760d457d.png)![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/7723ace339084720b155005174a3dcbf.png)

**连接的本质就是把各个连接表中的记录都取出来依次匹配的组合加入结果集并返回给用户。**

所以我们把e1和e2两个表连接起来的过程如下图所示：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/ce63857198984eee994ffcf826ab953e.png)

这个过程看起来就是把e1表的记录和e2的记录连起来组成新的更大的记录，所以这个查询过程称之为连接查询。连接查询的结果集中包含一个表中的每一条记录与另一个表中的每一条记录相互匹配的组合，像这样的结果集就可以称之为 **笛卡尔积** 。

因为表e1中有3条记录，表e2中也有3条记录，所以这两个表连接之后的笛卡尔积就有3×3=9行记录。

在MySQL中，连接查询的语法很随意，只要在FROM语句后边跟多个表名就好了，比如我们把e1表和e2表连接起来的查询语句可以写成这样：

```
 SELECT * FROM e1, e2;
```

#### 1.2.1.2.连接过程简介

我们可以连接任意数量张表，但是如果没有任何限制条件的话，这些表连接起来产生的笛卡尔积可能是非常巨大的。比方说3个100行记录的表连接起来产生的笛卡尔积就有100×100×100=1000000行数据！所以在连接的时候过滤掉特定记录组合是有必要的，在连接查询中的过滤条件可以分成两种，比方说下边这个查询语句：

```
SELECT * FROM e1, e2 WHERE e1.m1 > 1 AND e1.m1 = e2.m2 AND e2.n2 < 'd';
```

**涉及单表的条件**

e1.m1 > 1是只针对e1表的过滤条件

e2.n2&#x3c; 'd'是只针对e2表的过滤条件。

**涉及两表的条件**

比如类似e1.m1 = e2.m2，这些条件中涉及到了两个表。

看一下携带过滤条件的连接查询的大致执行过程在这个查询中我们指明了这三个过滤条件：

* e1.m1 > 1
* e1.m1 = e2.m2
* e2.n2 &#x3c; 'd'

那么这个连接查询的大致执行过程如下：

**确定驱动表(t1)**

首先确定第一个需要查询的表，这个表称之为 **驱动表** 。单表中执行查询语句只需要选取代价最小的那种访问方法去执行单表查询语句就好了（就是说之前从执行计划中找const、ref、ref_or_null、range、index、all等等这些执行方法中选取代价最小的去执行查询）。

此处假设使用e1作为驱动表，那么就需要到e1表中找满足e1.m1 > 1的记录，因为表中的数据太少，我们也没在表上建立二级索引，所以此处查询e1表的访问方法就设定为all，也就是采用全表扫描的方式执行单表查询。

**遍历驱动表结果，到被驱动表(t2)中查找匹配记录**

针对上一步骤中从驱动表产生的结果集中的每一条记录，分别需要到e2表中查找匹配的记录，所谓匹配的记录，指的是符合过滤条件的记录。

因为是根据e1表中的记录去找e2表中的记录，所以e2表也可以被称之为 **被驱动表** 。上一步骤从驱动表中得到了2条记录，所以需要查询2次e2表。

此时涉及两个表的列的过滤条件e1.m1 = e2.m2就派上用场了

当e1.m1 = 2时，过滤条件e1.m1 =e2.m2就相当于e2.m2 = 2，所以此时e2表相当于有了e2.m2 = 2、e2.n2 &#x3c; 'd'这两个过滤条件，然后到e2表中执行单表查询。

当e1.m1 = 3时，过滤条件e1.m1 =e2.m2就相当于e2.m2 = 3，所以此时e2表相当于有了e2.m2 = 3、e2.n2 &#x3c; 'd'这两个过滤条件，然后到e2表中执行单表查询。

所以整个连接查询的执行过程就如下图所示：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/b4edbeb22ba44282a683e282d6d6d386.png)

也就是说整个连接查询最后的结果只有两条符合过滤条件的记录：

从上边两个步骤可以看出来，这个两表连接查询共需要查询1次e1表，2次e2表。

当然这是在特定的过滤条件下的结果，如果我们把e1.m1 > 1这个条件去掉，那么从e1表中查出的记录就有3条，就需要查询3次e2表了。也就是说在两表连接查询中， **驱动表只需要访问一次，被驱动表可能被访问多次** 。

#### 1.2.1.3.内连接和外连接

为了大家更好理解后边内容，我们创建两个有现实意义的表，并插入一些数据：

```
CREATE TABLE student (
    number INT NOT NULL AUTO_INCREMENT COMMENT '学号',
    name VARCHAR(5) COMMENT '姓名',
    major VARCHAR(30) COMMENT '专业',
    PRIMARY KEY (number)
) Engine=InnoDB CHARSET=utf8 COMMENT '客户信息表';
```

```
CREATE TABLE score (
    number INT COMMENT '学号',
    subject VARCHAR(30) COMMENT '科目',
    score TINYINT COMMENT '成绩',
    PRIMARY KEY (number, subject)
) Engine=InnoDB CHARSET=utf8 COMMENT '客户成绩表';
```

两张表插入以下数据

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/23e133e52d14454589866f7d211ee196.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/587b439e6e9847c08f68158e1350f6ed.png)

现在我们想把每个学生的考试成绩都查询出来就需要进行两表连接了（因为score中没有姓名信息，所以不能单纯只查询score表）。连接过程就是从student表中取出记录，在score表中查找number相同的成绩记录，所以过滤条件就是student.number = socre.number，整个查询语句就是这样：

```
SELECT s1.number, s1.name, s2.subject, s2.score FROM student AS s1,score AS s2 WHERE s1.number = s2.number;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/1cf5538c2f964aa69480cbadffd2b0ec.png)

从上述查询结果中我们可以看到，各个同学对应的各科成绩就都被查出来了，可是有个问题，yan同学，也就是学号为20200904的同学因为某些原因没有参加考试，所以在score表中没有对应的成绩记录。

如果老师想查看所有同学的考试成绩，即使是缺考的同学也应该展示出来，但是到目前为止我们介绍的连接查询是无法完成这样的需求的。我们稍微思考一下这个需求，其本质是想： **驱动表中的记录即使在被驱动表中没有匹配的记录，也仍然需要加入到结果集** 。为了解决这个问题，就有了**内连接**和**外连接**的概念：

对于内连接的两个表，驱动表中的记录在被驱动表中找不到匹配的记录，该记录不会加入到最后的结果集，我们上边提到的连接都是所谓的内连接。

对于外连接的两个表，驱动表中的记录即使在被驱动表中没有匹配的记录，也仍然需要加入到结果集。

**在MySQL中，根据选取驱动表的不同，外连接仍然可以细分为2种：**

**左外连接** ，选取左侧的表为驱动表。

**右外连接** ，选取右侧的表为驱动表。

可是这样仍然存在问题，即使对于外连接来说，有时候我们也并不想把驱动表的全部记录都加入到最后的结果集。

这就犯难了，怎么办？把过滤条件分为两种就可以就解决这个问题了，所以放在不同地方的过滤条件是有不同语义的：

**WHERE子句中的过滤条件**

WHERE子句中的过滤条件就是我们平时见的那种，不论是内连接还是外连接，凡是不符合WHERE子句中的过滤条件的记录都不会被加入最后的结果集。

**ON子句中的过滤条件**

对于外连接的驱动表的记录来说，如果无法在被驱动表中找到匹配ON子句中的过滤条件的记录，那么该记录仍然会被加入到结果集中，对应的被驱动表记录的各个字段使用NULL值填充。

需要注意的是，这个ON子句是专门为外连接驱动表中的记录在被驱动表找不到匹配记录时应不应该把该记录加入结果集这个场景下提出的，所以如果把ON子句放到内连接中，MySQL会把它和WHERE子句一样对待，也就是说：内连接中的WHERE子句和ON子句是等价的。

一般情况下，我们都把只涉及单表的过滤条件放到WHERE子句中，把涉及两表的过滤条件都放到ON子句中，我们也一般把放到ON子句中的过滤条件也称之为连接条件。

##### 左（外）连接的语法

左（外）连接的语法还是挺简单的，比如我们要把e1表和e2表进行左外连接查询可以这么写：

```
SELECT * FROM e1 LEFT [OUTER] JOIN e2 ON 连接条件 [WHERE 普通过滤条件];
```

其中中括号里的OUTER单词是可以省略的。

对于LEFTJOIN类型的连接来说：

我们把放在左边的表称之为**外表或者驱动表**

右边的表称之为**内表或者被驱动表**。

所以上述例子中e1就是外表或者驱动表，e2就是内表或者被驱动表。需要注意的是，对于左（外）连接和右（外）连接来说，必须使用ON子句来指出连接条件。了解了左（外）连接的基本语法之后，再次回到我们上边那个现实问题中来，看看怎样写查询语句才能把所有的客户的成绩信息都查询出来，即使是缺考的考生也应该被放到结果集中：

```
SELECT s1.number, s1.name, s2.subject, s2.score FROM student AS s1 LEFT JOIN score AS s2 ON s1.number = s2.number;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/c761b34fe96b40849564af52e00413a6.png)

从结果集中可以看出来，虽然yan并没有对应的成绩记录，但是由于采用的是连接类型为左（外）连接，所以仍然把她放到了结果集中，只不过在对应的成绩记录的各列使用NULL值填充而已。

##### 右（外）连接的语法

右（外）连接和左（外）连接的原理是一样的，语法也只是把LEFT换成RIGHT而已：

```
SELECT * FROM e1
RIGHT [OUTER] JOIN e2 ON 连接条件 [WHERE 普通过滤条件];
```

只不过驱动表是右边的表e2，被驱动表是左边的表e1。

##### 内连接的语法

内连接和外连接的根本区别就是在驱动表中的记录不符合ON子句中的连接条件时不会把该记录加入到最后的结果集，一种最简单的内连接语法，就是直接把需要连接的多个表都放到FROM子句后边。其实针对内连接，MySQL提供了好多不同的语法：

```
SELECT * FROM e1 [INNER | CROSS] JOIN e2 [ON 连接条件] [WHERE 普通过滤条件];
```

也就是说在MySQL中，下边这几种内连接的写法都是等价的：

```
SELECT * FROM e1 JOIN e2;

SELECT * FROM e1 INNER JOIN e2;

SELECT * FROM e1 CROSS JOIN e2;
```

上边的这些写法和直接把需要连接的表名放到FROM语句之后，用逗号,分隔开的写法是等价的：

```
SELECT * FROM e1, e2;
```

再说一次，由于在内连接中ON子句和WHERE子句是等价的，所以内连接中不要求强制写明ON子句。

我们前边说过，连接的本质就是把各个连接表中的记录都取出来依次匹配的组合加入结果集并返回给用户。不论哪个表作为驱动表，两表连接产生的笛卡尔积肯定是一样的。而对于内连接来说，由于凡是不符合ON子句或WHERE子句中的条件的记录都会被过滤掉，其实也就相当于从两表连接的笛卡尔积中把不符合过滤条件的记录给踢出去，所以对于内连接来说，驱动表和被驱动表是可以互换的，并不会影响最后的查询结果。

但是对于外连接来说，由于驱动表中的记录即使在被驱动表中找不到符合ON子句条件的记录时也要将其加入到结果集，所以此时驱动表和被驱动表的关系就很重要了，也就是说左外连接和右外连接的驱动表和被驱动表不能轻易互换。

### 1.2.2.MySQL对连接的执行

复习了连接、内连接、外连接这些基本概念后，我们需要理解MySQL怎么样来进行表与表之间的连接，才能明白有的连接查询运行的快，有的却慢。

#### 1.2.2.1.嵌套循环连接（Nested-LoopJoin）

我们前边说过，对于两表连接来说，驱动表只会被访问一遍，但被驱动表却要被访问到好多遍，具体访问几遍取决于对驱动表执行单表查询后的结果集中的记录条数。

对于内连接来说，选取哪个表为驱动表都没关系，而外连接的驱动表是固定的，也就是说左（外）连接的驱动表就是左边的那个表，右（外）连接的驱动表就是右边的那个表。

如果有3个表进行连接的话，那么首先两表连接得到的结果集就像是新的驱动表，然后第三个表就成为了被驱动表，可以用伪代码表示一下这个过程就是这样：

```
for each row in e1 {   #此处表示遍历满足对e1单表查询结果集中的每一条记录，N条
    for each row in e2 {   #此处表示对于某条e1表的记录来说，遍历满足对e2单表查询结果集中的每一条记录，M条
            for each row in t3 {   #此处表示对于某条e1和e2表的记录组合来说，对t3表进行单表查询，L条
            if row satisfies join conditions, send to client
        }
    }
}

```

这个过程就像是一个嵌套的循环，所以这种驱动表只访问一次，但被驱动表却可能被多次访问，访问次数取决于对驱动表执行单表查询后的结果集中的记录条数的连接执行方式称之为**嵌套循环连接（** **Nested-Loop Join**  **）** ，这是最简单，也是最笨拙的一种连接查询算法，时间复杂度是O（N *  M * L）。

#### 1.2.2.2.使用索引加快连接速度

我们知道在嵌套循环连接的步骤2中可能需要访问多次被驱动表，如果访问被驱动表的方式都是全表扫描的话，那速度肯定会很慢很慢。

但是查询e2表其实就相当于一次单表查询，我们可以利用索引来加快查询速度。回顾一下最开始介绍的e1表和e2表进行内连接的例子：

```
SELECT * FROM e1, e2 WHERE e1.m1 > 1 AND e1.m1 = e2.m2 AND e2.n2 < 'd';
```

我们使用的其实是嵌套循环连接算法执行的连接查询，再把上边那个查询执行过程表回顾一下：

查询驱动表e1后的结果集中有两条记录，嵌套循环连接算法需要对被驱动表查询2次：

当e1.m1 = 2时，去查询一遍e2表，对e2表的查询语句相当于：

```
SELECT * FROM e2 WHERE e2.m2 = 2 AND e2.n2 < 'd';
```

当e1.m1 = 3时，再去查询一遍e2表，此时对e2表的查询语句相当于：

```
SELECT * FROM e2 WHERE e2.m2 = 3 AND e2.n2 < 'd';
```

可以看到，原来的e1.m1 = e2.m2这个涉及两个表的过滤条件在针对e2表做查询时关于e1表的条件就已经确定了，所以我们只需要单单优化对e2表的查询了，上述两个对e2表的查询语句中利用到的列是m2和n2列，我们可以在e2表的m2列上建立索引。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/de2d4d0ffab0420f9c395fd0e4f345a1.png)

因为对m2列的条件是等值查找，比如e2.m2= 2、e2.m2 = 3等，所以可能使用到**ref**的访问方法，假设使用ref的访问方法去执行对e2表的查询的话，需要回表之后再判断e2.n2 &#x3c; d这个条件是否成立。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/30b0db42d4a64754b749b5211b2dfc73.png)

在n2列上建立索引，涉及到的条件是e2.n2 &#x3c; 'd'，可能用到range的访问方法，假设使用range的访问方法对e2表的查询的话，需要回表之后再判断在m2列上的条件是否成立。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/666114546b4d44c89037d6756c0e4ceb.png)

假设m2和n2列上都存在索引的话，那么就需要从这两个里边儿挑一个代价更低的去执行对e2表的查询。当然，建立了索引不一定使用索引，只有在二级索引 + 回表的代价比全表扫描的代价更低时才会使用索引。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/ae35eadd398f411c99da4c4b4a7991bc.png)

另外，有时候连接查询的查询列表和过滤条件中可能只涉及被驱动表的部分列，而这些列都是某个索引的一部分，这种情况下即使不能使用eq_ref、ref、ref_or_null或者range这些访问方法执行对被驱动表的查询的话，也可以使用索引扫描，也就是index(索引覆盖)的访问方法来查询被驱动表。

#### 1.2.2.3.基于块的嵌套循环连接（Block Nested-Loop Join）

**扫描一个表的过程其实是先把这个表从磁盘上加载到内存中，然后从内存中比较匹配条件是否满足。**

现实生活中的表成千上万条记录都是少的，几百万、几千万甚至几亿条记录的表到处都是。内存里可能并不能完全存放的下表中所有的记录，所以在扫描表前边记录的时候后边的记录可能还在磁盘上，等扫描到后边记录的时候可能内存不足，所以需要把前边的记录从内存中释放掉。

而采用嵌套循环连接算法的两表连接过程中，被驱动表可是要被访问好多次的，如果这个被驱动表中的数据特别多而且不能使用索引进行访问，那就相当于要从磁盘上读好几次这个表，这个I/O代价就非常大了，所以我们得想办法：尽量减少访问被驱动表的次数。

当被驱动表中的数据非常多时，每次访问被驱动表，被驱动表的记录会被加载到内存中，在内存中的每一条记录只会和驱动表结果集的一条记录做匹配，之后就会被从内存中清除掉。然后再从驱动表结果集中拿出另一条记录，再一次把被驱动表的记录加载到内存中一遍，周而复始，驱动表结果集中有多少条记录，就得把被驱动表从磁盘上加载到内存中多少次。

所以我们可不可以在把被驱动表的记录加载到内存的时候，一次性和多条驱动表中的记录做匹配，这样就可以大大减少重复从磁盘上加载被驱动表的代价了。

所以MySQL提出了一个**join buffer**的概念，join buffer就是执行连接查询前申请的一块固定大小的内存，先把若干条驱动表结果集中的记录装在这个join buffer中，然后开始扫描被驱动表，每一条被驱动表的记录一次性和join buffer中的多条驱动表记录做匹配，因为匹配的过程都是在内存中完成的，所以这样可以显著减少被驱动表的I/O代价。使用join buffer的过程如下图所示：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/739edb3cbe0c4e078f1a3ef47019c1fa.png)

最最好的情况是join buffer足够大，能容纳驱动表结果集中的所有记录。

这种加入了join buffer的嵌套循环连接算法称之为**基于块的嵌套连接（** **Block Nested-Loop Join**  **）** 算法。

这个join buffer的大小是可以通过启动参数或者系统变量join_buffer_size进行配置，默认大小为262144字节（也就是256KB），最小可以设置为128字节。

```
show variables like 'join_buffer_size' ;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655442554057/e957d0f02aad4bb88347f5280193dab1.png)

当然，对于优化被驱动表的查询来说，最好是为被驱动表加上效率高的索引，如果实在不能使用索引，并且自己的机器的内存也比较大可以尝试调大join_buffer_size的值来对连接查询进行优化。

另外需要注意的是，驱动表的记录并不是所有列都会被放到join buffer中，只有查询列表中的列和过滤条件中的列才会被放到join buffer中，所以再次提醒我们，最好不要把*作为查询列表，只需要把我们关心的列放到查询列表就好了，这样还可以在join buffer中放置更多的记录。

# 1.MySQL的执行原理-2

## 1.1.MySQL的查询成本

### 1.1.1.什么是成本

MySQL执行一个查询可以有不同的执行方案，它会选择其中成本最低，或者说代价最低的那种方案去真正的执行查询。不过我们之前对成本的描述是非常模糊的，其实在MySQL中一条查询语句的执行成本是由下边这两个方面组成的：

**I/O成本**

我们的表经常使用的MyISAM、InnoDB存储引擎都是将数据和索引都存储到磁盘上的，当我们想查询表中的记录时，需要先把数据或者索引加载到内存中然后再操作。这个从磁盘到内存这个加载的过程损耗的时间称之为I/O成本。

**CPU成本**

读取以及检测记录是否满足对应的搜索条件、对结果集进行排序等这些操作损耗的时间称之为CPU成本。

对于InnoDB存储引擎来说，页是磁盘和内存之间交互的基本单位。

**MySQL规定读取一个页面花费的成本默认是1.0（I/O成本）**

**读取以及检测一条记录是否符合搜索条件的成本默认是0.2（CPU成本）**

1.0、0.2这些数字称之为成本常数，这两个成本常数我们最常用到，当然还有其他的成本常数。

**注意，不管读取记录时需不需要检测是否满足搜索条件，哪怕是空数据，其成本都算是0.2。**

### 1.1.2.单表查询的成本

#### 1.1.2.1.基于成本的优化步骤实战

在一条单表查询语句真正执行之前，MySQL的查询优化器会找出执行该语句所有可能使用的方案，对比之后找出成本最低的方案，这个**成本最低的方案就是所谓的执行计划**，之后才会调用存储引擎提供的接口真正的执行查询，这个过程总结一下就是这样：

1、根据搜索条件，找出所有可能使用的索引

2、计算全表扫描的代价

3、计算使用不同索引执行查询的代价

4、对比各种执行方案的代价，找出成本最低的那一个

下边我们就以一个实例来分析一下这些步骤，单表查询语句如下：

```
SELECT * FROM order_exp WHERE order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S') 
AND  expire_time> '2021-03-22 18:28:28' AND expire_time<= '2021-03-22 18:35:09' 
AND insert_time> expire_time AND order_note LIKE '%7****排1%' AND  order_status = 0;
```

看上去有点儿复杂，我们一步一步分析一下。

##### 1. 根据搜索条件，找出所有可能使用的索引

我们前边说过，对于B+树索引来说，只要索引列和常数使用=、&#x3c;=>、IN、NOT IN、IS NULL、IS NOT NULL、>、&#x3c;、>=、&#x3c;=、BETWEEN、!=（不等于也可以写成&#x3c;>）或者LIKE操作符连接起来，就可以产生一个所谓的范围区间（LIKE匹配字符串前缀也行），MySQL把一个查询中可能使用到的索引称之为possible keys。

我们分析一下上边查询中涉及到的几个搜索条件：

order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S') ，这个搜索条件可以使用二级索引idx_order_no。

expire_time> '2021-03-22 18:28:28' AND expire_time&#x3c;= '2021-03-22 18:35:09'，这个搜索条件可以使用二级索引idx_expire_time。

insert_time> expire_time，这个搜索条件的索引列由于没有和常数比较，所以并不能使用到索引。

order_note LIKE '%hello%'，order_note即使有索引，但是通过LIKE操作符和以通配符开头的字符串做比较，不可以适用索引。

order_status = 0，由于该列上只有联合索引，而且不符合最左前缀原则，所以不会用到索引。

综上所述，上边的查询语句可能用到的索引，也就是possible keys只有idx_order_no,idx_expire_time。

```
EXPLAIN SELECT * FROM order_exp WHERE order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S') 
AND  expire_time> '2021-03-22 18:28:28' AND expire_time<= '2021-03-22 18:35:09' 
AND insert_time> expire_time AND order_note LIKE '%7****排1%' AND  order_status = 0;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/eac38849149042b1bbd39ea51280ea8d.png)

##### 2. 计算全表扫描的代价

对于InnoDB存储引擎来说，全表扫描的意思就是把聚簇索引（主键索引）中的记录都依次和给定的搜索条件做一下比较，把符合搜索条件的记录加入到结果集，所以需要将聚簇索引对应的页面加载到内存中，然后再检测记录是否符合搜索条件。由于查询成本=I/O成本+CPU成本，所以计算全表扫描的代价需要两个信息：

**1、聚簇索引占用的页面数**

**2、该表中的记录数**

这两个信息从哪来呢？MySQL为每个表维护了一系列的统计信息，关于这些统计信息是如何收集起来的我们放在后边再说，现在看看怎么查看这些统计信息。

MySQL给我们提供了SHOW TABLE STATUS语句来查看表的统计信息，如果要看指定的某个表的统计信息，在该语句后加对应的LIKE语句就好了，比方说我们要查看order_exp这个表的统计信息可以这么写：

```
SHOW TABLE STATUS LIKE 'order_exp'\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/88f44ae6336b445ea8936e5baf9aadce.png)

出现了很多统计选项，但我们目前只需要两个：

**Rows**

本选项表示表中的记录条数。对于使用MyISAM存储引擎的表来说，该值是准确的，对于使用InnoDB存储引擎的表来说，该值是一个估计值。从查询结果我们也可以看出来，由于我们的order_exp表是使用InnoDB存储引擎的，所以虽然实际上表中有10567条记录，但是SHOW TABLE STATUS显示的Rows值只有10350条记录。但成本计算按照SHOW TABLE STATUS来计算。

**Data_length**

本选项表示表占用的存储空间字节数。使用MyISAM存储引擎的表来说，该值就是数据文件的大小，对于使用InnoDB存储引擎的表来说，该值就相当于聚簇索引占用的存储空间大小，也就是说可以这样计算该值的大小：

Data_length = 聚簇索引的页面数量 x 每个页面的大小

我们的order_exp使用默认16KB的页面大小，而上边查询结果显示Data_length的值是1589248，所以我们可以反向来推导出聚簇索引的页面数量：

**聚簇索引的页面数量 = 1589248 ÷ 16 ÷ 1024 = 97**

我们现在已经得到了聚簇索引占用的页面数量以及该表记录数的估计值，所以就可以计算全表扫描成本了。

现在可以看一下全表扫描成本的计算过程：

**I/O成本**

97 x 1.0 + 1.1 = 98.1

97指的是聚簇索引占用的页面数，1.0指的是加载一个页面的成本常数，后边的1.1是一个微调值。

关于这个微调值解释如下：

*MySQL*在真实计算成本时会进行一些微调，这些微调的值是直接硬编码到代码里的，没有注释而且这些微调的值十分的小，并不影响我们分析。

**CPU成本**

10350x 0.2 + 1.0 = 2071

10350指的是统计数据中表的记录数，对于InnoDB存储引擎来说是一个估计值，0.2指的是访问一条记录所需的成本常数，后边的1.0是一个微调值。

**总成本：**

98.1 + 2071 = 2169.1

**综上所述，对于order_exp的全表扫描所需的总成本就是2169.1。**

##### 3. 计算使用不同索引执行查询的代价

从第1步分析我们得到，上述查询可能使用到idx_order_no，idx_expire_time这两个索引，我们需要分别分析单独使用这些索引执行查询的成本，最后还要分析是否可能使用到索引合并。

这里需要提一点的是，MySQL查询优化器先分析使用唯一二级索引的成本，再分析使用普通索引的成本，我们这里两个索引都是普通索引，先算哪个都可以。我们也先分析idx_expire_time的成本，然后再看使用idx_order_no的成本。

###### 3.1使用idx_expire_time执行查询的成本分析

idx_expire_time对应的搜索条件是：

```
expire_time>'2021-03-22 18:28:28' AND expire_time<= '2021-03-22 18:35:09'
```

也就是说对应的范围区间就是：('2021-03-22 18:28:28' , '2021-03-22 18:35:09' )。

使用idx_expire_time搜索会使用用二级索引 + 回表方式的查询，MySQL计算这种查询的成本依赖两个方面的数据：

**1** **、范围区间数量**

不论某个范围区间的二级索引到底占用了多少页面，查询优化器认为读取索引的一个范围区间的I/O成本和读取一个页面是相同的。本例中使用idx_expire_time的范围区间只有一个，所以相当于访问这个范围区间的二级索引付出的I/O成本就是：**1 x 1.0 = 1.0**

**2** **、需要回表的记录数**

优化器需要计算二级索引的某个范围区间到底包含多少条记录，对于本例来说就是要计算idx_expire_time在('2021-03-22 18:28:28' ，'2021-03-22 18:35:09')这个范围区间中包含多少二级索引记录，计算过程是这样的：

**步骤1：**先根据expire_time>‘2021-03-22 18:28:28’这个条件访问一下idx_expire_time对应的B+树索引，找到满足expire_time> ‘2021-03-22 18:28:28’这个条件的第一条记录，我们把这条记录称之为区间最左记录。我们前头说过在B+数树中定位一条记录的过程是很快的，是常数级别的，所以这个过程的性能消耗是可以忽略不计的。

**步骤2：**然后再根据expire_time&#x3c;=‘2021-03-22 18:35:09’这个条件继续从idx_expire_time对应的B+树索引中找出最后一条满足这个条件的记录，我们把这条记录称之为区间最右记录，这个过程的性能消耗也可以忽略不计的。

**步骤3：**如果区间最左记录和区间最右记录相隔不太远（在MySQL 5.7这个版本里，只要相隔不大于10个页面即可），那就可以精确统计出满足expire_time> ‘2021-03-22 18:28:28’ AND expire_time&#x3c;= ‘2021-03-22 18:35:09’条件的二级索引记录条数。否则只沿着区间最左记录向右读10个页面，计算平均每个页面中包含多少记录，然后用这个平均值乘以区间最左记录和区间最右记录之间的页面数量就可以了。

那么问题又来了，怎么估计区间最左记录和区间最右记录之间有多少个页面呢？解决这个问题还得回到B+树索引的结构中来。

我们假设区间**最左记录在页b中**，**区间最右记录在页c中**，那么我们计算区间最左记录和区间最右记录之间的页面数量就相当于计算页b和页c之间有多少页面，而它们父节点中记录的每一条目录项记录都对应一个数据页，所以计算页b和页c之间有多少页面就相当于计算它们父节点（也就是页a）中对应的目录项记录之间隔着几条记录。在一个页面中统计两条记录之间有几条记录的成本就很小了。

不过还有问题，如果页b和页c之间的页面实在太多，以至于页b和页c对应的目录项记录都不在一个父页面中怎么办？既然是树，那就继续递归，之前我们说过一个B+树有4层高已经很了不得了，所以这个统计过程也不是很耗费性能。

知道了如何统计二级索引某个范围区间的记录数之后，就需要回到现实问题中来，MySQL根据上述算法测得idx_expire_time在区间('2021-03-22 18:28:28' ，'2021-03-22 18:35:09')之间大约有39条记录。

```
explain SELECT * FROM order_exp WHERE expire_time> '2021-03-22 18:28:28' AND expire_time<= '2021-03-22 18:35:09';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/437bdbd1a1fc42ea80b1b00910a699f3.png)

读取这39条二级索引记录需要付出的CPU成本就是：

**39 x 0.2 + 0.01 = 7.81**

其中39是需要读取的二级索引记录条数，0.2是读取一条记录成本常数，0.01是微调。

在通过二级索引获取到记录之后，还需要干两件事儿：

**1** **、根据这些记录里的主键值到聚簇索引中做回表操作**

MySQL评估回表操作的I/O成本依旧很简单粗暴，他们认为每次回表操作都相当于访问一个页面，也就是说二级索引范围区间有多少记录，就需要进行多少次回表操作，也就是需要进行多少次页面I/O。我们上边统计了使用idx_expire_time二级索引执行查询时，预计有39 条二级索引记录需要进行回表操作，所以回表操作带来的I/O成本就是：

**39 x 1.0 = 39**

其中39 是预计的二级索引记录数，1.0是一个页面的I/O成本常数。

**2** **、回表操作后得到的完整用户记录，然后再检测其他搜索条件是否成立**

回表操作的本质就是通过二级索引记录的主键值到聚簇索引中找到完整的用户记录，然后再检测除expire_time> '2021-03-22 18:28:28' AND expire_time&#x3c;'2021-03-22 18:35:09'这个搜索条件以外的搜索条件是否成立。

因为我们通过范围区间获取到二级索引记录共39条，也就对应着聚簇索引中39 条完整的用户记录，读取并检测这些完整的用户记录是否符合其余的搜索条件的CPU成本如下：

**39 x 0.2 =7.8**

其中39 是待检测记录的条数，0.2是检测一条记录是否符合给定的搜索条件的成本常数。

**所以本例中使用idx_expire_time执行查询的成本就如下所示：**

**I/O成本：**

1.0 + 39 x 1.0 = 40 .0 (范围区间的数量 + 预估的二级索引记录条数)

**CPU成本：**

39 x 0.2 + 0.01+39 x 0.2 = 15.61 （读取二级索引记录的成本 + 读取并检测回表后聚簇索引记录的成本）

综上所述，使用idx_expire_time执行查询的总成本就是：

**40 .0 + 15.61 = 55.61**

###### 3.2使用idx_order_no执行查询的成本分析

idx_order_no对应的搜索条件是：

```
order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S')
```

也就是说相当于3个单点区间。与使用idx_expire_time的情况类似，我们也需要计算使用idx_order_no时需要访问的范围区间数量以及需要回表的记录数，计算过程与上面类似，我们不详列所有计算步骤和说明了。

**范围区间数量**

使用idx_order_no执行查询时很显然有3个单点区间，所以访问这3个范围区间的二级索引付出的I/O成本就是：

3 x 1.0 = 3.0

**需要回表的记录数**

由于使用idx_expire_time时有3个单点区间，所以每个单点区间都需要查找一遍对应的二级索引记录数，三个单点区间总共需要回表的记录数是58。

```
explain SELECT * FROM order_exp WHERE order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S');
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/ca0a978531af460ab59808adb6cc2a28.png)

读取这些二级索引记录的CPU成本就是：58 x 0.2+0.01 = 11.61

得到总共需要回表的记录数之后，就要考虑：

根据这些记录里的主键值到聚簇索引中做回表操作，所需的I/O成本就是：58 x 1.0 = 58.0

回表操作后得到的完整用户记录，然后再比较其他搜索条件是否成立

此步骤对应的CPU成本就是：

58 x 0.2 = 11.6

**所以本例中使用idx_order_no执行查询的成本就如下所示：**

**I/O成本：**

3.0 + 58 x 1.0 = 61.0 (范围区间的数量 + 预估的二级索引记录条数)

**CPU成本：**

58 x 0.2 + 58 x 0.2 + 0.01 = 23.21 （读取二级索引记录的成本 + 读取并检测回表后聚簇索引记录的成本）

**综上所述，使用idx_order_no执行查询的总成本就是：61.0 + 23.21 = 84.21**

###### 3.3是否有可能使用索引合并（Index Merge）

本例中有关order_no和expire_time的搜索条件是使用AND连接起来的，而对于idx_order_no和idx_expire_time都是范围查询，也就是说查找到的二级索引记录并不是按照主键值进行排序的，并不满足使用Intersection索引合并的条件，所以并不会使用索引合并。而且MySQL查询优化器计算索引合并成本的算法也比较麻烦.

##### 4. 对比各种方案，找出成本最低的那一个

下边把执行本例中的查询的各种可执行方案以及它们对应的成本列出来：

* **全表扫描的成本：2148.7**
* **使用idx_expire_time的成本：55.61**
* **使用idx_order_no的成本：84.21**

很显然，使用idx_expire_time的成本最低，所以当然选择idx_expire_time来执行查询。

***最后请注意：MySQL的源码中对成本的计算实际要更复杂，但是以上基本思想和算法是没问题的。***

### 1.1.3.Explain与查询成本

#### 1.1.3.1.EXPLAIN输出成本

前面我们已经对MySQL查询优化器如何计算成本有了比较深刻的了解。但是EXPLAIN语句输出中缺少了一个衡量执行计划好坏的重要属性—— **成本。**

不过MySQL已经为我们提供了一种查看某个执行计划花费的成本的方式：

在EXPLAIN单词和真正的查询语句中间加上FORMAT=JSON。

这样我们就可以得到一个json格式的执行计划，里边包含该计划花费的成本，比如这样：

```
explain format= json SELECT * FROM order_exp WHERE order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S') AND  expire_time> '2021-03-22 18:28:28' AND expire_time<= '2021-03-22 18:35:09' AND insert_time> expire_time AND order_note LIKE '%7排1%' AND  order_status = 0\G
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/6731f38ecf4a4a7e8067e6ed2f6de380.png)

这么多字段怎么解释，这里我用截图的方式解释一下

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/e95000b8e8d246cda35312323f8176f8.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/f3de9ce2944242d982eb2fcc98e6a0d4.png)

#### 1.1.3.2.Optimizer Trace

自认为比较牛逼的同学可能有这样的疑问：“我就觉得使用其他的执行方案比EXPLAIN输出的这种方案强，凭什么优化器做的决定和我想的不一样呢？为什么MySQL一定要全文扫描，不用索引呢？”，所以：在MySQL 5.6以及之后的版本中，MySQL提出了一个optimizertrace的功能，这个功能可以让我们方便的查看优化器生成执行计划的整个过程，这个功能的开启与关闭由系统变量optimizer_trace决定：

```
SHOW VARIABLES LIKE 'optimizer_trace';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/569ef34d93b64e3f9f0626a17ef94c45.png)

可以看到enabled值为off，表明这个功能默认是关闭的。

如果想打开这个功能，必须首先把enabled的值改为on，就像这样：（注意这个开关是seesion级别）

```
SET optimizer_trace= 'enabled=on';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/b49e94eacb674d52859b8c5c3aea4d61.png)

one_line的值是控制输出格式的，如果为on那么所有输出都将在一行中展示，我们就保持其默认值为off。

当停止查看语句的优化过程时，把optimizertrace功能关闭

```
SET optimizer_trace="enabled=off";
```

**注意：开启trace****会影响mysql****性能，所以只能临时分析sql** **使用，用完之后立即关闭** **。**

现在我们有一个搜索条件比较多的查询语句，它的执行计划如下：

```
explain
SELECT * FROM order_exp WHERE order_no IN ('DD00_6S', 'DD00_9S', 'DD00_10S')
AND expire_time> '2021-03-22 18:28:28' AND insert_time> '2021-03-22
18:35:09' AND order_note LIKE '%7****排1%';
```

可以看到该查询可能使用到的索引有3个u_idx_day_status,idx_order_no,idx_expire_time，那么为什么优化器最终选择了idx_order_no而不选择其他的索引或者直接全表扫描呢？这时候就可以通过otpimzer trace功能来查看优化器的具体工作过程：（记得开启optimizer trace功能）

```
SELECT * FROM information_schema.OPTIMIZER_TRACE\G
```

然后我们就可以输入我们想要查看优化过程的查询语句，当该查询语句执行完成后，就可以到information_schema数据库下的OPTIMIZER_TRACE表中查看完整的优化过程。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/071e2b6370d64fc6a05afe4ac2fa0f24.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/e13ccfaeaa79441089ad76dba81914af.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/d1b5b8c07a5b4bbfb4e13161fe9b47ca.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/ea094b91cfd24eda82ea99bd93dd9940.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/60d0b4b81b3649f8a5c01af5e8ea60d3.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/9aaf797bc5434cf58417deb6ca325912.png)

**优化过程大致分为了三个阶段：**

**prepare阶段**

**optimize阶段**

**execute阶段**

我们所说的基于成本的优化主要集中在optimize阶段，对于单表查询来说，我们主要关注optimize阶段的"rows_estimation"这个过程，这个过程深入分析了对单表查询的各种执行方案的成本；

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/68b11334b36a447180d89a6ad72a25dc.png)

对于多表连接查询来说，我们更多需要关注"considered_execution_plans"这个过程，这个过程里会写明各种不同的连接方式所对应的成本。反正优化器最终会选择成本最低的那种方案来作为最终的执行计划，也就是我们使用EXPLAIN语句所展现出的那种方案。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/bdef9326eefc4ac5af42bba9bc054137.png)

如果对使用EXPLAIN语句展示出的对某个查询的执行计划很不理解，就可以尝试使用optimizer trace功能来详细了解每一种执行方案对应的成本。

### 1.1.4.连接查询的成本

#### 1.1.4.1.Condition filtering介绍

我们前边说过，MySQL中连接查询采用的是嵌套循环连接算法，驱动表会被访问一次，被驱动表可能会被访问多次，所以对于两表连接查询来说，它的查询成本由下边两个部分构成：

**1、单次查询驱动表的成本**

**2、多次查询被驱动表的成本（具体查询多少次取决于对驱动表查询的结果集中有多少条记录）**

**对驱动表进行查询后得到的记录条数称之为驱动表的 扇出 （英文名：fanout）。**

很显然驱动表的扇出值越小，对被驱动表的查询次数也就越少，连接查询的总成本也就越低。当查询优化器想计算整个连接查询所使用的成本时，就需要计算出驱动表的扇出值，有的时候扇出值的计算是很容易的，比如下边这两个查询：

**查询一：**

```
SELECT * FROM order_exp AS s1 INNER JOIN order_exp2 AS s2;
```

假设使用s1表作为驱动表，很显然对驱动表的单表查询只能使用全表扫描的方式执行，驱动表的扇出值也很明确，那就是驱动表中有多少记录，扇出值就是多少。统计数据中s1表的记录行数是10573，也就是说优化器就直接会把10573当作在s1表的扇出值。

**查询二：**

```
SELECT * FROM order_exp AS s1 INNER JOIN order_exp2 AS s2 WHERE s1.expire_time> '2021-03-22 18:28:28' AND s1.expire_time<= '2021-03-22 18:35:09';
```

仍然假设s1表是驱动表的话，很显然对驱动表的单表查询可以使用idx_expire_time索引执行查询。此时范围区间( '2021-03-22 18:28:28', '2021-03-22 18:35:09')中有多少条记录，那么扇出值就是多少。

**但是有的时候扇出值的计算就变得很棘手，比方说下边几个查询：**

**查询三：**

```
SELECT * FROM order_exp AS s1 INNER JOIN order_exp2 AS s2 WHERE s1.order_note > 'xyz';
```

本查询和查询一类似，只不过对于驱动表s1多了一个order_note > 'xyz'的搜索条件。查询优化器又不会真正的去执行查询，所以它只能猜这10573记录里有多少条记录满足order_note > 'xyz'条件。

**查询四：**

```
SELECT * FROM order_exp AS s1 INNER JOIN order_exp2 AS s2 WHERE s1.expire_time>'2021-03-22 18:28:28' AND s1.expire_time<= '2021-03-22 18:35:09' AND s1.order_note > 'xyz';
```

本查询和查询二类似，只不过对于驱动表s1也多了一个order_note > 'xyz'的搜索条件。不过因为本查询可以使用idx_expire_time索引，所以只需要从符合二级索引范围区间的记录中猜有多少条记录符合order_note > 'xyz'条件，也就是只需要猜在39条记录中有多少符合order_note > 'xyz'条件。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/c7fc7eee09fb4d15ace392cc285430bb.png)

通过上面4个案例大家可以看到，MySQL很多时候在计算数据的时候很多时候只能靠猜。

MySQL把这个猜的过程称之为 **condition filtering** 。当然，这个过程可能会使用到索引，也可能使用到统计数据，也可能就是MySQL单纯的瞎猜，整个评估过程非常复杂，所以我们不去细讲。

在MySQL 5.7之前的版本中，查询优化器在计算驱动表扇出时，如果是使用全表扫描的话，就直接使用表中记录的数量作为扇出值，如果使用索引的话，就直接使用满足范围条件的索引记录条数作为扇出值。

在MySQL 5.7中，MySQL引入了这个condition filtering的功能，就是还要猜一猜剩余的那些搜索条件能把驱动表中的记录再过滤多少条，其实本质上就是为了让成本估算更精确。我们所说的纯粹瞎猜其实是很不严谨的，MySQL称之为启发式规则。

#### 1.1.4.2.两表连接的成本分析

连接查询的成本计算公式是这样的：

连接查询总成本 = 单次访问驱动表的成本 + 驱动表扇出数 x 单次访问被驱动表的成本

对于左（外）连接和右（外）连接查询来说，它们的驱动表是固定的，所以想要得到最优的查询方案只需要分别为驱动表和被驱动表选择成本最低的访问方法。

可是对于内连接来说，驱动表和被驱动表的位置是可以互换的，所以需要考虑两个方面的问题：

不同的表作为驱动表最终的查询成本可能是不同的，也就是需要考虑最优的表连接顺序。然后分别为驱动表和被驱动表选择成本最低的访问方法。

很显然，计算内连接查询成本的方式更麻烦一些，下边我们就以内连接为例来看看如何计算出最优的连接查询方案。当然在某些情况下，左（外）连接和右（外）连接查询在某些特殊情况下可以被优化为内连接查询。

我们来看看内连接，比如对于下边这个查询来说：

```
SELECT
	*
FROM
	order_exp AS s1
INNER JOIN order_exp2 AS s2 ON s1.order_no = s2.order_note
WHERE s1.expire_time > '2021-03-22 18:28:28'
AND s1.expire_time <= '2021-03-22 18:35:09'
AND s2.expire_time > '2021-03-22 18:35:09'
AND s2.expire_time <= '2021-03-22 18:35:59';
```

可以选择的连接顺序有两种：

s1连接s2，也就是s1作为驱动表，s2作为被驱动表。

s2连接s1，也就是s2作为驱动表，s1作为被驱动表。

查询优化器需要分别考虑这两种情况下的最优查询成本，然后选取那个成本更低的连接顺序以及该连接顺序下各个表的最优访问方法作为最终的查询计划。我们定性的分析一下，不像分析单表查询那样定量的分析了：

具体都可以使用分析语句来执行

```
explain format=json   SQL语句
```

#### 1.1.4.4.多表连接的成本分析

首先要考虑一下多表连接时可能产生出多少种连接顺序：

对于两表连接，比如表A和表B连接只有 AB、BA这两种连接顺序。其实相当于2× 1 = 2种连接顺序。

对于三表连接，比如表A、表B、表C进行连接有ABC、ACB、BAC、BCA、CAB、CBA这么6种连接顺序。其实相当于3 × 2 × 1 = 6种连接顺序。

对于四表连接的话，则会有4 × 3 × 2 × 1 = 24种连接顺序。对于n表连接的话，则有 n × (n-1) × (n-2) × ··· × 1种连接顺序，就是n的阶乘种连接顺序，也就是n!。

有n个表进行连接，MySQL查询优化器要每一种连接顺序的成本都计算一遍么？那可是n!种连接顺序呀。其实真的是要都算一遍，不过MySQL用了很多办法减少计算非常多种连接顺序的成本的方法：

**提前结束某种顺序的成本评估**

MySQL在计算各种链接顺序的成本之前，会维护一个全局的变量，这个变量表示当前最小的连接查询成本。如果在分析某个连接顺序的成本时，该成本已经超过当前最小的连接查询成本，那就压根儿不对该连接顺序继续往下分析了。比方说A、B、C三个表进行连接，已经得到连接顺序ABC是当前的最小连接成本，比方说10.0，在计算连接顺序BCA时，发现B和C的连接成本就已经大于10.0时，就不再继续往后分析BCA这个连接顺序的成本了。

**系统变量optimizer_search_depth**

为了防止无穷无尽的分析各种连接顺序的成本，MySQL提出了optimizer_search_depth系统变量，如果连接表的个数小于该值，那么就继续穷举分析每一种连接顺序的成本，否则只对与optimizer_search_depth值相同数量的表进行穷举分析。很显然，该值越大，成本分析的越精确，越容易得到好的执行计划，但是消耗的时间也就越长，否则得到不是很好的执行计划，但可以省掉很多分析连接成本的时间。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/b5219847280b4452adcd0efd0c2d1b17.png)

**根据某些规则压根儿就不考虑某些连接顺序**

即使是有上边两条规则的限制，但是分析多个表不同连接顺序成本花费的时间还是会很长，所以MySQL干脆提出了一些所谓的启发式规则（就是根据以往经验指定的一些规则），凡是不满足这些规则的连接顺序压根儿就不分析，这样可以极大的减少需要分析的连接顺序的数量，但是也可能造成错失最优的执行计划。他们提供了一个系统变量optimizer_prune_level来控制到底是不是用这些启发式规则。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/93c11888f3384b2f9b38aeccefae17c7.png)

### 1.1.5.调节成本常数

我们前边已经介绍了两个成本常数：

读取一个页面花费的成本默认是1.0

检测一条记录是否符合搜索条件的成本默认是0.2

其实除了这两个成本常数，MySQL还支持很多，它们被存储到了MySQL数据库的两个表中：

```
SHOW TABLES FROM mysql LIKE '%cost%';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/1b5828a088844fcea880181114b0d91e.png)

因为一条语句的执行其实是分为两层的：server层、存储引擎层。

在server层进行连接管理、查询缓存、语法解析、查询优化等操作，在存储引擎层执行具体的数据存取操作。也就是说一条语句在server层中执行的成本是和它操作的表使用的存储引擎是没关系的，所以关于这些操作对应的成本常数就存储在了server_cost表中，而依赖于存储引擎的一些操作对应的成本常数就存储在了engine_cost表中。

#### 1.1.5.1.mysql.server_cost表

server_cost表中在server层进行的一些操作对应的成本常数，具体内容如下：

```
SELECT * FROM mysql.server_cost;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/33e0741af5d442628638dd8d282d0162.png)

我们先看一下server_cost各个列都分别是什么意思：

cost_name

表示成本常数的名称。

cost_value

表示成本常数对应的值。如果该列的值为NULL的话，意味着对应的成本常数会采用默认值。

last_update

表示最后更新记录的时间。

comment

注释。

从server_cost中的内容可以看出来，目前在server层的一些操作对应的成本常数有以下几种：

**disk_temptable_create_cost 默认值40.0**

创建基于磁盘的临时表的成本，如果增大这个值的话会让优化器尽量少的创建基于磁盘的临时表。

**disk_temptable_row_cost     默认值1.0**

向基于磁盘的临时表写入或读取一条记录的成本，如果增大这个值的话会让优化器尽量少的创建基于磁盘的临时表。

**key_compare_cost   0.1**

两条记录做比较操作的成本，多用在排序操作上，如果增大这个值的话会提升filesort的成本，让优化器可能更倾向于使用索引完成排序而不是filesort。

**memory_temptable_create_cost  默认值2.0**

创建基于内存的临时表的成本，如果增大这个值的话会让优化器尽量少的创建基于内存的临时表。

**memory_temptable_row_cost     默认值0.2**

向基于内存的临时表写入或读取一条记录的成本，如果增大这个值的话会让优化器尽量少的创建基于内存的临时表。

**row_evaluate_cost  默认值0.2**

这个就是我们之前一直使用的检测一条记录是否符合搜索条件的成本，增大这个值可能让优化器更倾向于使用索引而不是直接全表扫描。

MySQL在执行诸如DISTINCT查询、分组查询、Union查询以及某些特殊条件下的排序查询都可能在内部先创建一个临时表，使用这个临时表来辅助完成查询（比如对于DISTINCT查询可以建一个带有UNIQUE索引的临时表，直接把需要去重的记录插入到这个临时表中，插入完成之后的记录就是结果集了）。在数据量大的情况下可能创建基于磁盘的临时表，也就是为该临时表使用MyISAM、InnoDB等存储引擎，在数据量不大时可能创建基于内存的临时表，也就是使用Memory存储引擎。大家可以看到，创建临时表和对这个临时表进行写入和读取的操作代价还是很高的就行了。

这些成本常数在server_cost中的初始值都是NULL，意味着优化器会使用它们的默认值来计算某个操作的成本，如果我们想修改某个成本常数的值的话，需要做两个步骤：

对我们感兴趣的成本常数做update更新操作，然后使用下边语句即可：

```
FLUSH OPTIMIZER_COSTS;
```

当然，在你修改完某个成本常数后想把它们再改回默认值的话，可以直接把cost_value的值设置为NULL，再使用FLUSH OPTIMIZER_COSTS语句让系统重新加载。

#### 1.1.5.2.mysql.engine_cost表

engine_cost表表中在存储引擎层进行的一些操作对应的成本常数，具体内容如下：

```
SELECT * FROM mysql.engine_cost;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/1c736464e55c45789b62b058b54f276a.png)

与server_cost相比，engine_cost多了两个列：

**engine_name列**

指成本常数适用的存储引擎名称。如果该值为default，意味着对应的成本常数适用于所有的存储引擎。

**device_type列**

指存储引擎使用的设备类型，这主要是为了区分常规的机械硬盘和固态硬盘，不过在MySQL 5.7.X这个版本中并没有对机械硬盘的成本和固态硬盘的成本作区分，所以该值默认是0。

我们从engine_cost表中的内容可以看出来，目前支持的存储引擎成本常数只有两个：

**io_block_read_cost  默认值1.0**

从磁盘上读取一个块对应的成本。请注意我使用的是块，而不是页这个词。对于InnoDB存储引擎来说，一个页就是一个块，不过对于MyISAM存储引擎来说，默认是以4096字节作为一个块的。增大这个值会加重I/O成本，可能让优化器更倾向于选择使用索引执行查询而不是执行全表扫描。

**memory_block_read_cost     默认值1.0**

与上一个参数类似，只不过衡量的是从内存中读取一个块对应的成本。

怎么从内存中和从磁盘上读取一个块的默认成本是一样的？这主要是因为在MySQL目前的实现中，并不能准确预测某个查询需要访问的块中有哪些块已经加载到内存中，有哪些块还停留在磁盘上，所以MySQL简单的认为不管这个块有没有加载到内存中，使用的成本都是1.0。

与更新server_cost表中的记录一样，我们也可以通过更新engine_cost表中的记录来更改关于存储引擎的成本常数，做法一样。

## 1.2.MySQL的查询重写规则

对于一些执行起来十分耗费性能的语句，MySQL还是依据一些规则，竭尽全力的把这个很糟糕的语句转换成某种可以比较高效执行的形式，这个过程也可以被称作查询重写。

### 1.2.1.条件化简

我们编写的查询语句的搜索条件本质上是一个表达式，这些表达式可能比较繁杂，或者不能高效的执行，MySQL的查询优化器会为我们简化这些表达式。

#### 1.2.1.1.移除不必要的括号

有时候表达式里有许多无用的括号，比如这样：

```
((a = 5 AND b =c) OR ((a > c) AND (c < 5)))
```

看着就很烦，优化器会把那些用不到的括号给干掉，就是这样：

```
(a = 5 and b =c) OR (a > c AND c < 5)
```

#### 1.2.1.2.常量传递（constant_propagation）

有时候某个表达式是某个列和某个常量做等值匹配，比如这样：

```
a = 5
```

当这个表达式和其他涉及列a的表达式使用AND连接起来时，可以将其他表达式中的a的值替换为5，比如这样：

```
a = 5 AND b >a
```

就可以被转换为：

```
a = 5 AND b >5
```

等值传递（equality_propagation）

有时候多个列之间存在等值匹配的关系，比如这样：

```
a = b and b = c and c = 5
```

这个表达式可以被简化为：

```
a = 5 and b = 5 and c = 5
```

#### 1.2.1.3.移除没用的条件（trivial_condition_removal）

对于一些明显永远为TRUE或者FALSE的表达式，优化器会移除掉它们，比如这个表达式：

```
(a < 1 and b= b) OR (a = 6 OR 5 != 5)
```

很明显，b = b这个表达式永远为TRUE，5 != 5这个表达式永远为FALSE，所以简化后的表达式就是这样的：

```
(a < 1 and TRUE) OR (a = 6 OR FALSE)
```

可以继续被简化为

```
a < 1 OR a =6
```

#### 1.2.1.4.表达式计算

在查询开始执行之前，如果表达式中只包含常量的话，它的值会被先计算出来，比如这个：

```
a = 5 + 1
```

因为5 + 1这个表达式只包含常量，所以就会被化简成：

```
a = 6
```

但是这里需要注意的是，如果某个列并不是以单独的形式作为表达式的操作数时，比如出现在函数中，出现在某个更复杂表达式中，就像这样：

```
ABS(a) > 5
```

或者：

```
-a < -8
```

优化器是不会尝试对这些表达式进行化简的。我们前边说过只有搜索条件中索引列和常数使用某些运算符连接起来才可能使用到索引，所以如果可以的话，最好让索引列以单独的形式出现在表达式中。

#### 1.2.1.5.常量表检测

MySQL觉得下边这种查询运行的特别快：

使用主键等值匹配或者唯一二级索引列等值匹配作为搜索条件来查询某个表。

MySQL觉得这两种查询花费的时间特别少，少到可以忽略，所以也把通过这两种方式查询的表称之为常量表（英文名：constant tables）。优化器在分析一个查询语句时，先首先执行常量表查询，然后把查询中涉及到该表的条件全部替换成常数，最后再分析其余表的查询成本，比方说这个查询语句：

```
SELECT
	*
FROM
	table1
INNER JOIN table2 ON table1.column1 = table2.column2
WHERE
	table1.primary_key = 1;
```

很明显，这个查询可以使用主键和常量值的等值匹配来查询table1表，也就是在这个查询中table1表相当于常量表，在分析对table2表的查询成本之前，就会执行对table1表的查询，并把查询中涉及table1表的条件都替换掉，也就是上边的语句会被转换成这样：

```
SELECT
	table1表记录的各个字段的常量值,
	table2.*
FROM
	table1
INNER JOIN table2 ON table1表column1列的常量值 = table2.column2;
```

### 1.2.2.外连接消除

我们前边说过，内连接的驱动表和被驱动表的位置可以相互转换，而左（外）连接和右（外）连接的驱动表和被驱动表是固定的。这就导致内连接可能通过优化表的连接顺序来降低整体的查询成本，而外连接却无法优化表的连接顺序。

我们之前说过，外连接和内连接的本质区别就是：对于外连接的驱动表的记录来说，如果无法在被驱动表中找到匹配ON子句中的过滤条件的记录，那么该记录仍然会被加入到结果集中，对应的被驱动表记录的各个字段使用NULL值填充；而内连接的驱动表的记录如果无法在被驱动表中找到匹配ON子句中的过滤条件的记录，那么该记录会被舍弃。查询效果就是这样：

```
SELECT * FROM e1 INNER JOIN e2 ON e1.m1 = e2.m2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/4a3733668cf246d4aa0d15a1be8bd3b7.png)

```
SELECT * FROM e1 LEFT JOIN e2 ON e1.m1 = e2.m2;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/370684f5300e48b88bc8ba28f057e8e9.png)

对于上边例子中的（左）外连接来说，由于驱动表e1中m1=1, n1='a'的记录无法在被驱动表e2中找到符合ON子句条件e1.m1 = e2.m2的记录，所以就直接把这条记录加入到结果集，对应的e2表的m2和n2列的值都设置为NULL。

因为凡是不符合WHERE子句中条件的记录都不会参与连接。只要我们在搜索条件中指定关于被驱动表相关列的值不为NULL，那么外连接中在被驱动表中找不到符合ON子句条件的驱动表记录也就被排除出最后的结果集了，也就是说：在这种情况下：外连接和内连接也就没有什么区别了！

另外再说下这个查询：

```
SELECT* FROM e1 LEFT JOIN e2 ON e1.m1 = e2.m2 WHERE e2.n2 IS NOT NULL
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/a5649b1e6f734a50b88f02c7804a3101.png)

由于指定了被驱动表e2的n2列不允许为NULL，所以上边的e1和e2表的左（外）连接查询和内连接查询是一样的。当然，我们也可以不用显式的指定被驱动表的某个列IS NOT NULL，只要隐含的有这个意思就行了，比方说这样：

```
SELECT * FROM e1 LEFT JOIN e2 ON e1.m1 = e2.m2 WHERE e2.m2 = 2
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1655603177032/a045575075da46d7aaae5a5b6072d84d.png)

在这个例子中，我们在WHERE子句中指定了被驱动表e2的m2列等于2，也就相当于间接的指定了m2列不为NULL值，所以上边的这个左（外）连接查询其实和下边这个内连接查询是等价的：

```
SELECT* FROM e1 INNER JOIN e2 ON e1.m1 = e2.m2 WHERE e2.m2 = 2
```

我们把这种在外连接查询中，指定的WHERE子句中包含被驱动表中的列不为NULL值的条件称之为空值拒绝（英文名：reject-NULL）。在被驱动表的WHERE子句符合空值拒绝的条件后，外连接和内连接可以相互转换。这种转换带来的好处就是查询优化器可以通过评估表的不同连接顺序的成本，选出成本最低的那种连接顺序来执行查询。

### 1.2.3.子查询优化

#### 1.2.3.1.子查询语法

在一个查询语句A里的某个位置也可以有另一个查询语句B，这个出现在A语句的某个位置中的查询B就被称为子查询，A也被称之为外层查询。子查询可以在一个外层查询的各种位置出现，比如：

**1）SELECT子句中**

也就是我们平时说的查询列表中，比如这样：

```
SELECT(SELECT m1 FROM e1 LIMIT 1);
```

其中的(SELECT m1 FROM e1LIMIT 1)就是子查询。

**2）FROM子句中**

```
SELECT m, n FROM (SELECT m2 + 1 AS m, n2 AS n FROM e2 WHERE m2 > 2) AS t;
```

这个例子中的子查询是：(SELECT m2+1 AS m, n2 AS n FROM e2 WHERE m2 > 2)

这里可以把子查询的查询结果当作是一个表，子查询后边的AS t表明这个子查询的结果就相当于一个名称为t的表，这个名叫t的表的列就是子查询结果中的列，比如例子中表t就有两个列：m列和n列。

这个放在FROM子句中的子查询本质上相当于一个表，但又和我们平常使用的表有点儿不一样，MySQL把这种由子查询结果集组成的表称之为 **派生表** 。

**3）WHERE****或ON****子句中**

把子查询放在外层查询的WHERE子句或者ON子句中可能是我们最常用的一种使用子查询的方式了，比如这样：

```
SELECT * FROM e1 WHERE m1 IN (SELECT m2 FROM e2)
```

这个查询表明我们想要将(SELECT m2FROM e2)这个子查询的结果作为外层查询的IN语句参数，整个查询语句的意思就是我们想找e1表中的某些记录，这些记录的m1列的值能在e2表的m2列找到匹配的值。

**4）ORDER BY****子句、GROUP BY****子句中**

虽然语法支持，但没啥意义。

还有一些其他的子查询，这里不一一列举

#### 1.2.3.2.子查询在MySQL中是怎么执行的

想象中子查询的执行方式是这样的：

如果该子查询是不相关子查询，比如下边这个查询：

```
SELECT * FROM s1 WHERE order_note IN (SELECT order_note FROM s2);
```

先单独执行(SELECTorder_note FROM s2)这个子查询。

然后在将上一步子查询得到的结果当作外层查询的参数再执行外层查询

最后根据子查询的查询结果来检测外层查询WHERE子句的条件是否成立，如果成立，就把外层查询的那条记录加入到结果集，否则就丢弃。

**但真的是这样吗？其实MySQL用了一系列的办法来优化子查询的执行，大部分情况下这些优化措施其实挺有效的，下边我们来看看各种不同类型的子查询具体是怎么执行的。**

不同的子查询

##### 1）按返回的结果集区分子查询

因为子查询本身也算是一个查询，所以可以按照它们返回的不同结果集类型而把这些子查询分为不同的类型：

###### 1.1)标量子查询

那些只返回一个单一值的子查询称之为标量子查询，比如这样：

```
SELECT (SELECT m1 FROM e1 LIMIT 1);
```

或者这样：

```
SELECT * FROM e1 WHERE m1 = (SELECT MIN(m2) FROM e2);

SELECT * FROM e1 WHERE m1 < (SELECT MIN(m2) FROM e2);
```

这两个查询语句中的子查询都返回一个单一的值，也就是一个标量。这些标量子查询可以作为一个单一值或者表达式的一部分出现在查询语句的各个地方。

###### 1.2)行子查询

顾名思义，就是返回一条记录的子查询，不过这条记录需要包含多个列（只包含一个列就成了标量子查询了）。比如这样：

```
SELECT * FROM e1 WHERE (m1, n1) = (SELECT m2, n2 FROM e2 LIMIT 1);
```

其中的(SELECT m2, n2 FROM e2 LIMIT 1)就是一个行子查询，整条语句的含义就是要从e1表中找一些记录，这些记录的m1和n1列分别等于子查询结果中的m2和n2列。

###### 1.3)列子查询

列子查询自然就是查询出一个列的数据，不过这个列的数据需要包含多条记录（只包含一条记录就成了标量子查询了）。比如这样：

```
SELECT * FROM e1 WHERE m1 IN (SELECT m2 FROM e2);
```

其中的(SELECT m2 FROM e2)就是一个列子查询，表明查询出e2表的m2列的值作为外层查询IN语句的参数。

###### 1.4)表子查询

顾名思义，就是子查询的结果既包含很多条记录，又包含很多个列，比如这样：

```
SELECT * FROM e1 WHERE (m1, n1) IN (SELECT m2, n2 FROM e2);
```

其中的(SELECT m2, n2 FROM e2)就是一个表子查询，

这里需要和行子查询对比一下，行子查询中我们用了LIMIT 1来保证子查询的结果只有一条记录，表子查询中不需要这个限制。

##### 2)按与外层查询关系来区分子查询

###### 2.1)不相关子查询

如果子查询可以单独运行出结果，而不依赖于外层查询的值，我们就可以把这个子查询称之为不相关子查询。我们前边介绍的那些子查询全部都可以看作不相关子查询。

###### 2.2)相关子查询

如果子查询的执行需要依赖于外层查询的值，我们就可以把这个子查询称之为相关子查询。比如：

```
SELECT * FROM e1 WHERE m1 IN (SELECT m2 FROM e2 WHERE n1 = n2);
```

例子中的子查询是(SELECT m2 FROM e2 WHERE n1 = n2)，

可是这个查询中有一个搜索条件是n1 = n2，别忘了n1是表e1的列，也就是外层查询的列，也就是说子查询的执行需要依赖于外层查询的值，所以这个子查询就是一个相关子查询。

##### 3) [NOT] IN/ANY/SOME/ALL子查询

对于列子查询和表子查询来说，它们的结果集中包含很多条记录，这些记录相当于是一个集合，所以就不能单纯的和另外一个操作数使用操作符来组成布尔表达式了，MySQL通过下面的语法来支持某个操作数和一个集合组成一个布尔表达式：

###### 3.1)IN或者NOT IN

具体的语法形式如下：

操作数 [NOT] IN (子查询)

这个布尔表达式的意思是用来判断某个操作数在不在由子查询结果集组成的集合中，比如下边的查询的意思是找出e1表中的某些记录，这些记录存在于子查询的结果集中：

```
SELECT * FROM e1 WHERE (m1, n1) IN (SELECT m2, n2 FROM e2);
```

###### 3.2) ANY/SOME（ANY和SOME是同义词）

具体的语法形式如下：

操作数 比较符 ANY/SOME(子查询)

这个布尔表达式的意思是只要子查询结果集中存在某个值和给定的操作数做比较操作，比较结果为TRUE，那么整个表达式的结果就为TRUE，否则整个表达式的结果就为FALSE。比方说下边这个查询：

```
SELECT * FROM e1 WHERE m1 > ANY(SELECT m2 FROM e2);
```

这个查询的意思就是对于e1表的某条记录的m1列的值来说

如果子查询(SELECTm2 FROM e2)的结果集中存在一个小于m1列的值，那么整个布尔表达式的值就是TRUE，

否则为FALSE，也就是说只要m1列的值大于子查询结果集中最小的值，整个表达式的结果就是TRUE，所以上边的查询本质上等价于这个查询：

```
SELECT * FROM e1 WHERE m1 > (SELECT MIN(m2) FROM e2);
```

另外，=ANY相当于判断子查询结果集中是否存在某个值和给定的操作数相等，它的含义和IN是相同的。

###### 3.3)ALL具体的语法形式如下：

操作数 比较操作 ALL(子查询)

这个布尔表达式的意思是子查询结果集中所有的值和给定的操作数做比较操作比较结果为TRUE，那么整个表达式的结果就为TRUE，否则整个表达式的结果就为FALSE。比方说下边这个查询：

```
SELECT * FROM e1 WHERE m1 > ALL(SELECT m2 FROM e2);
```

这个查询的意思就是对于e1表的某条记录的m1列的值来说

如果子查询(SELECT m2 FROM e2)的结果集中的所有值都小于m1列的值，那么整个布尔表达式的值就是TRUE，否则为FALSE，也就是说只要m1列的值大于子查询结果集中最大的值，整个表达式的结果就是TRUE，所以上边的查询本质上等价于这个查询：

```
SELECT * FROM e1 WHERE m1 > (SELECT MAX(m2) FROM e2);
```

###### 3.4)EXISTS子查询

有的时候我们仅仅需要判断子查询的结果集中是否有记录，而不在乎它的记录具体是个啥，可以使用把EXISTS或者NOT EXISTS放在子查询语句前边，就像这样：

```
SELECT * FROM e1 WHERE EXISTS (SELECT 1 FROM e2);
```

对于子查询(SELECT 1 FROM e2)来说，我们并不关心这个子查询最后到底查询出的结果是什么，所以查询列表里填*、某个列名，或者其他啥东西都无所谓，我们真正关心的是子查询的结果集中是否存在记录。也就是说只要(SELECT 1 FROM e2)这个查询中有记录，那么整个EXISTS表达式的结果就为TRUE。

#### 1.2.3.3.MySQL对IN子查询的优化

##### 1）标量子查询、行子查询的执行方式

对于**不相关标量子查询或者行子查询**来说，它们的执行方式很简单，比方说下边这个查询语句：

```
SELECT * FROM s1 WHERE order_note = (SELECT order_note FROM s2 WHERE key3 = 'a' LIMIT 1);
```

它的执行方式和我们前面想象的一样：

先单独执行(SELECT order_note FROM s2 WHERE key3 = 'a' LIMIT 1)这个子查询。

然后在将上一步子查询得到的结果当作外层查询的参数，

再执行外层查询SELECT * FROM s1 WHERE order_note= ...。

也就是说，对于包含不相关的标量子查询或者行子查询的查询语句来说，MySQL会分别独立的执行外层查询和子查询，就当作两个单表查询就好了。

对于**相关的标量子查询或者行子查询**来说，比如下边这个查询：

```
SELECT * FROM s1 WHERE
order_note = (SELECT order_note FROM s2 WHERE s1.order_no= s2.order_no LIMIT 1);
```

事情也和我们前面想象的一样，它的执行方式就是这样的：

先从外层查询中获取一条记录，本例中也就是先从s1表中获取一条记录。

然后从上一步骤中获取的那条记录中找出子查询中涉及到的值，本例中就是从s1表中获取的那条记录中找出s1.order_no列的值，然后执行子查询。

最后根据子查询的查询结果来检测外层查询WHERE子句的条件是否成立，如果成立，就把外层查询的那条记录加入到结果集，否则就丢弃。

再次执行第一步，获取第二条外层查询中的记录，依次类推。

也就是说对于两种使用标量子查询以及行子查询的场景中，MySQL优化器的执行方式并没有什么新鲜的。

###### 2)物化表

对于不相关的IN子查询，比如这样：

```
SELECT * FROM s1 WHERE order_note IN (SELECT order_note FROM s2 WHERE order_no = 'a');
```

我们最开始的感觉就是这种不相关的IN子查询和不相关的标量子查询或者行子查询是一样一样的，都是把外层查询和子查询当作两个独立的单表查询来对待。但是MySQL为了优化IN子查询下了很大力气，所以整个执行过程并不像我们想象的那么简单。

对于不相关的IN子查询来说，如果子查询的结果集中的记录条数很少，那么把子查询和外层查询分别看成两个单独的单表查询效率很高，但是如果单独执行子查询后的结果集太多的话，就会导致这些问题：

1、结果集太多，可能内存中都放不下。

2、对于外层查询来说，如果子查询的结果集太多，那就意味着IN子句中的参数特别多，这就导致：无法有效的使用索引，只能对外层查询进行全表扫描。

在对外层查询执行全表扫描时，由于IN子句中的参数太多，这会导致检测一条记录是否符合和IN子句中的参数匹配花费的时间太长。

比如说IN子句中的参数只有两个：

```
SELECT * FROM tbl_name WHERE column IN (a, b);
```

这样相当于需要对tbl_name表中的每条记录判断一下它的column列是否符合column = a OR column = b。

在IN子句中的参数比较少时这并不是什么问题，如果IN子句中的参数比较多时，比如这样：

```
SELECT * FROM tbl_name WHERE column IN (a, b, c ..., ...);
```

那么这样每条记录需要判断一下它的column列是否符合column =a OR column = b OR column = c OR ...，这样性能耗费可就多了。

MySQL的改进是不直接将不相关子查询的结果集当作外层查询的参数，而是将该结果集写入一个临时表里。写入临时表的过程是这样的：

1、该临时表的列就是子查询结果集中的列。

2、写入临时表的记录会被去重，临时表也是个表，只要为表中记录的所有列建立主键或者唯一索引。

一般情况下子查询结果集不会大的离谱，所以会为它建立基于内存的使用Memory存储引擎的临时表，而且会为该表建立哈希索引。

如果子查询的结果集非常大，超过了系统变量tmp_table_size或者max_heap_table_size，临时表会转而使用基于磁盘的存储引擎来保存结果集中的记录，索引类型也对应转变为B+树索引。

MySQL把这个将子查询结果集中的记录保存到临时表的过程称之为 **物化** （英文名：Materialize）。为了方便起见，我们就把那个存储子查询结果集的临时表称之为物化表。正因为物化表中的记录都建立了索引（基于内存的物化表有哈希索引，基于磁盘的有B+树索引），通过索引执行IN语句判断某个操作数在不在子查询结果集中变得非常快，从而提升了子查询语句的性能。

###### 3)物化表转连接

事情到这就完了？我们还得重新审视一下最开始的那个查询语句：

```
SELECT * FROM s1 WHERE order_note IN (SELECT order_note FROM s2 WHERE order_no = 'a');
```

当我们把子查询进行物化之后，假设子查询物化表的名称为materialized_table，该物化表存储的子查询结果集的列为m_val，那么这个查询

就相当于表s1和子查询物化表materialized_table进行内连接：

```
SELECT s1.* FROM s1 INNER JOIN materialized_table ON order_note = m_val;
```

转化成内连接之后就有意思了，查询优化器可以评估不同连接顺序需要的成本是多少，选取成本最低的那种查询方式执行查询。

我们分析一下上述查询中使用外层查询的表s1和物化表materialized_table进行内连接的成本都是由哪几部分组成的：

**1、如果使用s1表作为驱动表的话，总查询成本由下边几个部分组成：**

* 物化子查询时需要的成本
* 扫描s1表时的成本

s1表中的记录数量 × 通过m_val = xxx对materialized_table表进行单表访问的成本（我们前边说过物化表中的记录是不重复的，并且为物化表中的列建立了索引，所以这个步骤显然是非常快的）。

**2、如果使用materialized_table表作为驱动表的话，总查询成本由下边几个部分组成：**

* 物化子查询时需要的成本
* 扫描物化表时的成本

物化表中的记录数量 × 通过order_note= xxx对s1表进行单表访问的成本（如果order_note列上建立了索引，这个步骤还是非常快的）。

MySQL查询优化器会通过运算来选择上述成本更低的方案来执行查询。



# 1.InnoDB引擎底层解析

**InnoDB的三大特性：**

* 双写机制（double write）
* Buffer Pool
* 自适应Hash索引

自适应Hash索引在之前的索引课中已经讲到了，这节课不再做陈述。同时我们对InnoDB不能只是光看亮点，还是要体系化的去学习。

InnoDB的内存结构和磁盘存储结构图总结如下：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/a264b5382fc744b189952d7b0770a6aa.png)

看这种结构图大家肯定是比较晕的，所以我们用需求来驱动进行讲解。

1、InnoDB对于我们来说还是一个黑盒，我们只负责使用客户端发送请求并等待服务器返回结果，表中的数据到底存到了哪里？

2、表中的数据以什么格式存放的？

3、InnoDB是以什么方式来访问的这些数据？

4、InnoDB中的事务、锁等的原理是怎样？

## 1.1.InnoDB记录存储结构和索引页结构

InnoDB是一个将表中的数据存储到磁盘上的存储引擎，所以即使关机后重启我们的数据还是存在的。而真正处理数据的过程是发生在内存中的，所以需要把磁盘中的数据加载到内存中，如果是处理写入或修改请求的话，还需要把内存中的内容刷新到磁盘上。而我们知道读写磁盘的速度非常慢，和内存读写差了几个数量级，所以当我们想从表中获取某些记录时，InnoDB存储引擎需要一条一条的把记录从磁盘上读出来么？

InnoDB采取的方式是：将数据划分为若干个页，以页作为磁盘和内存之间交互的基本单位，InnoDB中页的大小一般为 16 KB。也就是在一般情况下，一次最少从磁盘中读取16KB的内容到内存中，一次最少把内存中的16KB内容刷新到磁盘中。

我们平时是以记录为单位来向表中插入数据的，这些记录在磁盘上的存放方式也被称为**行格式。**

### 1.1.1.行格式

InnoDB存储引擎设计了4种不同类型的行格式，分别是Compact、Redundant、Dynamic和Compressed行格式。我们可以查看默认值：

```
show variables like 'innodb_default_row_format'
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/9ed37ba7e1154c808ad4330cd4f6e2b0.png)

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/b29180bf7aa74682b371fe59dcb617a5.png)

我们可以在创建或修改表的语句中指定行格式：

```
CREATE TABLE 表名 (列的信息) ROW_FORMAT=行格式名称
```

#### 1.1.1.1.COMPACT

```
create table text(c1 VARCHAR(10)) ROW_FORMAT=COMPACT;
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/c416f3ea5c4a432db11f1a0f1b7f8abe.png)

COMPACT行格式示意图如下：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/0d816200b1df4a5fac70d5b76464347f.png)

**变长字段长度列表**

我们知道MySQL支持一些变长的数据类型，比如VARCHAR(M)、VARBINARY(M)、各种TEXT类型，各种BLOB类型，我们也可以把拥有这些数据类型的列称为变长字段，变长字段中存储多少字节的数据是不固定的，所以我们在存储真实数据的时候需要顺便把这些数据占用的字节数也存起来。如果该可变字段允许存储的最大字节数（M×W）超过255字节并且真实存储的字节数（L）超过127字节，则使用2个字节，否则使用1个字节。

**NULL值列表**

表中的某些列可能存储NULL值，如果把这些NULL值都放到记录的真实数据中存储会很占地方，所以Compact行格式把这些值为NULL的列统一管理起来，存储到NULL值列表。每个允许存储NULL的列对应一个二进制位，二进制位的值为1时，代表该列的值为NULL。二进制位的值为0时，代表该列的值不为NULL。

**记录头信息**

它是由固定的5个字节组成。5个字节也就是40个二进制位，不同的位代表不同的意思。

|              | 二进制位数 | 解释                                                         |
| ------------ | ---------- | ------------------------------------------------------------ |
| 预留位1      | 1          | 没有使用                                                     |
| 预留位2      | 1          | 没有使用                                                     |
| delete_mask  | 1          | 标记该记录是否被删除                                         |
| min_rec_mask | 1          | B+树的每层非叶子节点中的最小记录都会添加该标记               |
| n_owned      | 4          | 表示当前记录拥有的记录数                                     |
| heap_no      | 13         | 表示当前记录在页的位置信息                                   |
| record_type  | 3          | 表示当前记录的类型，<br />0表示普通记录，<br />1表示B+树非叶子节点记录，<br />2表示最小记录，<br />3表示最大记录 |
| next_record  | 16         | 表示下一条记录的相对位置                                     |

**隐藏列信息**

MySQL会为每个记录默认的添加一些列（也称为隐藏列），包括：

DB_ROW_ID(row_id)：非必须，6字节，表示行ID，唯一标识一条记录

InnoDB表对主键的生成策略是：优先使用用户自定义主键作为主键，如果用户没有定义主键，则选取一个Unique键作为主键，如果表中连Unique键都没有定义的话，则InnoDB会为表默认添加一个名为row_id的隐藏列作为主键。

DB_TRX_ID：必须，6字节，表示事务ID

DB_ROLL_PTR：必须，7字节，表示回滚指

其他的行格式和Compact行格式差别不大。

#### 1.1.1.2.Redundant行格式

Redundant行格式是MySQL5.0之前用的一种行格式，不予深究。

#### 1.1.1.3.Dynamic和Compressed行格式

MySQL5.7的默认行格式就是Dynamic，Dynamic和Compressed行格式和Compact行格式挺像，只不过在处理行溢出数据时有所不同。Compressed行格式和Dynamic不同的一点是，Compressed行格式会采用压缩算法对页面进行压缩，以节省空间。

#### 1.1.1.4. 数据溢出

如果我们定义一个表，表中只有一个VARCHAR字段，如下：

```
CREATE TABLE test_varchar( c VARCHAR(60000) )
```

然后往这个字段插入60000个字符，会发生什么？

前边说过，MySQL中磁盘和内存交互的基本单位是页，也就是说MySQL是以页为基本单位来管理存储空间的，我们的记录都会被分配到某个页中存储。而一个页的大小一般是16KB，也就是16384字节，而一个VARCHAR(M)类型的列就最多可以存储65532个字节，这样就可能造成一个页存放不了一条记录的情况。

在Compact和Redundant行格式中，对于占用存储空间非常大的列，在记录的真实数据处只会存储该列的该列的前768个字节的数据，然后把剩余的数据分散存储在几个其他的页中，记录的真实数据处用20个字节存储指向这些页的地址。这个过程也叫做行溢出，存储超出768字节的那些页面也被称为溢出页。

Dynamic和Compressed行格式，不会在记录的真实数据处存储字段真实数据的前768个字节，而是把所有的字节都存储到其他页面中，只在记录的真实数据处存储其他页面的地址。

### 1.1.2.索引页格式

前边我们简单提了一下Page页的概念，它是InnoDB管理存储空间的基本单位，一个页的大小一般是16KB。

InnoDB为了不同的目的而设计了许多种不同类型的页，存放我们表中记录的那种类型的页自然也是其中的一员，官方称这种存放记录的页为索引（INDEX）页，不过要理解成数据页也没问题，毕竟存在着聚簇索引这种索引和数据混合的东西。

#### 1.1.2.1.数据页结构

一个InnoDB数据页的存储空间大致被划分成了7个部分：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/7a6e884c29d34321a751a285dbfce597.png)

| name               | 名称               | 长度       | 备注                     |
| ------------------ | ------------------ | ---------- | ------------------------ |
| File Header        | 文件头部           | 38字节     | 页的一些通用信息         |
| Page Header        | 页面头部           | 56字节     | 数据页专有的一些信息     |
| Infimum + Supremum | 最小记录和最大记录 | 26字节     | 两个虚拟的行记录         |
| User Records       | 用户记录           | 大小不确定 | 实际存储的行记录内容     |
| Free Space         | 空闲空间           | 大小不确定 | 页中尚未使用的空间       |
| Page Directory     | 页面目录           | 大小不确定 | 页中的某些记录的相对位置 |
| File Trailer       | 文件尾部           | 8字节      | 校验页是否完整           |

##### Page页的类型：

![image-20240129125538343](E:\图灵课堂\MySQL专题\MySQL专题.assets\image-20240129125538343.png)

Page页底层采用链表管理（详见三大特性之Buffer Pool），根据（header中）状态可分为三种类型。空闲，已使用未被修改，脏页等待刷盘

##### [User Records]()

我们自己存储的记录会按照我们**指定的行格式存储到User Records部分**。

但是在一开始生成页的时候，其实并没有User Records这个部分，每当我们插入一条记录，都会从Free Space部分，也就是尚未使用的存储空间中申请一个记录大小的空间划分到User Records部分，当Free Space部分的空间全部被User Records部分替代掉之后，也就意味着这个页使用完了，如果还有新的记录插入的话，就需要去申请新的页了。

当前记录被删除时，则会修改记录头信息中的delete_mask为1，也就是说被删除的记录还在页中，还在真实的磁盘上。这些被删除的记录之所以不立即从磁盘上移除，是因为移除它们之后把其他的记录在磁盘上重新排列需要性能消耗。

所以只是打一个删除标记而已，所有被删除掉的记录都会组成一个所谓的垃圾链表，在这个链表中的记录占用的空间称之为所谓的可重用空间，之后如果有新记录插入到表中的话，可能把这些被删除的记录占用的存储空间覆盖掉。

同时我们插入的记录在会记录自己在本页中的位置，写入了记录头信息中heap_no部分。heap_no值为0和1的记录是InnoDB自动给每个页增加的两个记录，称为伪记录或者虚拟记录。这两个伪记录一个代表最小记录，一个代表最大记录，这两条存放在页的User Records部分，他们被单独放在一个称为Infimum + Supremum的部分。

记录头信息中next_record记录了从当前记录的真实数据到下一条记录的真实数据的地址偏移量。这其实是个链表，可以通过一条记录找到它的下一条记录。但是需要注意注意再注意的一点是，下一条记录指得并不是按照我们插入顺序的下一条记录，而是按照主键值由小到大的顺序的下一条记录。而且规定 Infimum记录（也就是最小记录） 的下一条记录就是本页中主键值最小的用户记录，而本页中主键值最大的用户记录的下一条记录就是 Supremum记录（也就是最大记录）

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/ae01bc1913984281bf5ba09cf5385aa2.png)

我们的记录按照主键从小到大的顺序形成了一个单链表，记录被删除，则从这个链表上摘除。

##### Page Directory

Page Directory主要**是解决记录链表的查找问题**。

如果我们想根据主键值查找页中的某条记录该咋办？按链表查找的办法：从Infimum记录（最小记录）开始，沿着链表一直往后找，总会找到或者找不到。

InnoDB的改进是，为页中的记录再制作了一个目录，他们的制作过程是这样的：

1、将所有正常的记录（包括最大和最小记录，不包括标记为已删除的记录）划分为几个组。

2、每个组的最后一条记录（也就是组内最大的那条记录）的头信息中的n_owned属性表示该记录拥有多少条记录，也就是该组内共有几条记录。

3、将每个组的最后一条记录的地址偏移量单独提取出来按顺序存储到靠近页的尾部的地方，这个地方就是所谓的Page Directory，也就是页目录页面目录中的这些地址偏移量被称为槽（英文名：Slot），所以这个页面目录就是由槽组成的。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/472172ba6b78440fba068453fbe35af8.png)

4、每个分组中的记录条数是有规定的：对于最小记录所在的分组只能有 1 条记录，最大记录所在的分组拥有的记录条数只能在1到8 条之间，剩下的分组中记录的条数范围只能在是 4到8 条之间，如下图：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/52fd8de4b5f14e34ba686cabae8a75f5.png)

这样，一个数据页中查找指定主键值的记录的过程分为两步：

通过二分法确定该记录所在的槽，并找到该槽所在分组中主键值最小的那条记录。

通过记录的next_record属性遍历该槽所在的组中的各个记录。

##### Page Header

InnoDB为了能得到一个数据页中**存储的记录的状态信息**。

比如本页中已经存储了多少条记录，第一条记录的地址是什么，页目录中存储了多少个槽等等，特意在页中定义了一个叫Page Header的部分，它是页结构的第二部分，这个部分占用固定的56个字节，专门存储各种状态信息。

##### File Header

File Header针对各种类型的页都通用，也就是说不同类型的页都会以File Header作为第一个组成部分。

它描述了一些针对**各种页都通用的一些信息**，比方说页的类型，这个页的编号是多少，它的上一个页、下一个页是谁，页的校验和等等，这个部分占用固定的38个字节。

页的类型，包括Undo日志页、段信息节点、InsertBuffer空闲列表、Insert Buffer位图、系统页、事务系统数据、表空间头部信息、扩展描述页、溢出页、索引页，有些页会在后面的课程看到。

同时通过上一个页、下一个页建立一个双向链表把许许多多的页就串联起来，而无需这些页在物理上真正连着。但是并不是所有类型的页都有上一个和下一个页的属性，数据页是有这两个属性的，所以所有的数据页其实是一个双向链表。

##### File Trailer

我们知道InnoDB存储引擎会把数据存储到磁盘上，但是磁盘速度太慢，需要以页为单位把数据加载到内存中处理，如果该页中的数据在内存中被修改了，那么在修改后的某个时间需要把数据同步到磁盘中。但是在同步了一半的时候中断电了咋办？

**为了检测一个页是否完整**（也就是在同步的时候有没有发生只同步一半的尴尬情况），InnoDB每个页的尾部都加了一个File Trailer部分，这个部分由8个字节组成，可以分成2个小部分：

前4个字节代表页的校验和

这个部分是和File Header中的校验和相对应的。每当一个页面在内存中修改了，在同步之前就要把它的校验和算出来，因为File Header在页面的前边，所以校验和会被首先同步到磁盘，当完全写完时，校验和也会被写到页的尾部，如果完全同步成功，则页的首部和尾部的校验和应该是一致的。如果写了一半儿断电了，那么在File Header中的校验和就代表着已经修改过的页，而在File Trailer中的校验和代表着原先的页，二者不同则意味着同步中间出了错。

后4个字节代表页面被最后修改时对应的日志序列位置（LSN），这个也和校验页的完整性有关。

这个File Trailer与File Header类似，都是所有类型的页通用的。

## 1.2.InnoDB的表空间

表空间是一个抽象的概念，对于系统表空间来说，对应着文件系统中一个或多个实际文件；对于每个独立表空间来说，对应着文件系统中一个名为表名.ibd的实际文件。大家可以把表空间想象成被切分为许许多多个页的池子，当我们想为某个表插入一条记录的时候，就从池子中捞出一个对应的页来把数据写进去。

再回忆一次，InnoDB是以页为单位管理存储空间的，我们的聚簇索引（也就是完整的表数据）和其他的二级索引都是以B+树的形式保存到表空间的，而B+树的节点就是数据页。

任何类型的页都有File Header这个部分，File Header中专门的地方（FIL_PAGE_ARCH_LOG_NO_OR_SPACE_ID）保存页属于哪个表空间，同时表空间中的每一个页都对应着一个页号（FIL_PAGE_OFFSET），这个页号由4个字节组成，也就是32个比特位，所以一个表空间最多可以拥有2³²个页，如果按照页的默认大小16KB来算，一个表空间最多支持64TB的数据。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/83c7dc17f55c4285a3861743be595a97.png)

### 1.2.1.独立表空间结构

#### 1.2.1.1.  区（extent）

表空间中的页可以达到2³²个页，实在是太多了，为了更好的管理这些页面，InnoDB中还有一个区（英文名：extent）的概念。对于16KB的页来说，连续的64个页就是一个区，也就是说一个区默认占用1MB空间大小。

不论是系统表空间还是独立表空间，都可以看成是由若干个区组成的，每256个区又被划分成一个组。

第一个组最开始的3个页面的类型是固定的：用来登记整个表空间的一些整体属性以及本组所有的区被称为FSP_HDR，也就是extent 0 ~ extent 255这256个区，整个表空间只有一个FSP_HDR。

其余各组最开始的2个页面的类型是固定的，一个XDES类型，用来登记本组256个区的属性，FSP_HDR类型的页面其实和XDES类型的页面的作用类似，只不过FSP_HDR类型的页面还会额外存储一些表空间的属性。

**引入区的主要目的是什么？**

我们每向表中插入一条记录，本质上就是向该表的聚簇索引以及所有二级索引代表的B+树的节点中插入数据。而B+树的每一层中的页都会形成一个双向链表，如果是以页为单位来分配存储空间的话，双向链表相邻的两个页之间的物理位置可能离得非常远。

我们介绍B+树索引的适用场景的时候特别提到范围查询只需要定位到最左边的记录和最右边的记录，然后沿着双向链表一直扫描就可以了，而如果链表中相邻的两个页物理位置离得非常远，就是所谓的随机I/O。再一次强调，磁盘的速度和内存的速度差了好几个数量级，随机I/O是非常慢的，所以我们应该尽量让链表中相邻的页的物理位置也相邻，这样进行范围查询的时候才可以使用所谓的顺序I/O。

一个区就是在物理位置上连续的64个页。在表中数据量大的时候，为某个索引分配空间的时候就不再按照页为单位分配了，而是按照区为单位分配，甚至在表中的数据十分非常特别多的时候，可以一次性分配多个连续的区，从性能角度看，可以消除很多的随机I/O。

#### 1.2.1.2.  段（segment）

我们提到的范围查询，其实是对B+树叶子节点中的记录进行顺序扫描，而如果不区分叶子节点和非叶子节点，统统把节点代表的页面放到申请到的区中的话，进行范围扫描的效果就大打折扣了。所以InnoDB对B+树的叶子节点和非叶子节点进行了区别对待，也就是说叶子节点有自己独有的区，非叶子节点也有自己独有的区。

存放叶子节点的区的集合就算是一个段（segment），存放非叶子节点的区的集合也算是一个段。也就是说一个索引会生成2个段，一个叶子节点段，一个非叶子节点段。

段其实不对应表空间中某一个连续的物理区域，而是一个逻辑上的概念。

### 1.2.2.系统表空间

#### 1.2.2.1.  整体结构

系统表空间的结构和独立表空间基本类似，只不过由于整个MySQL进程只有一个系统表空间，在系统表空间中会额外记录一些有关整个系统信息的页面，所以会比独立表空间多出一些记录这些信息的页面，相当于是表空间之首，所以它的表空间 ID（Space ID）是0。

系统表空间的extent 1和extent 2这两个区，也就是页号从64~191这128个页面被称为Doublewrite buffer，也就是双写缓冲区。

#### 1.2.2.2. 双写缓冲区/双写机制

双写缓冲区/双写机制是InnoDB的三大特性之一，还有两个是Buffer Pool、自适应Hash索引。

##### 先了解：部分写失效

当数据库正在从内存向磁盘写一个数据页时，数据库宕机，从而导致这个页只写了部分数据，就是部分写失效。

##### 解决了什么问题

部分写失效会导致数据丢失。是无法通过重做日志恢复的，因为重做日志记录的是对页的物理修改，如果页本身已经损坏，重做日志也无能为力。

它是一种特殊文件flush技术，带给InnoDB存储引擎的是数据页的可靠性。它的作用是，在把页写到数据文件之前，InnoDB先把它们写到一个叫doublewrite buffer（双写缓冲区）的连续区域内，在写doublewrite buffer完成后，InnoDB才会把页写到数据文件的适当的位置。如果在写页的过程中发生意外崩溃，InnoDB在稍后的恢复过程中在doublewrite buffer中找到完好的page副本用于恢复。

doublewrite buffer是InnoDB在系统表空间上的128个页（2个区，extend1和extend2），大小是2MB

所以在正常的情况下, MySQL写数据页时，会写两遍到磁盘上，第一遍是在写redo log （prepare状态的时候）写到doublewrite buffer，第二遍是写到真正的数据文件中。如果发生了极端情况（断电），InnoDB再次启动后，发现了一个页数据已经损坏，那么此时就可以从doublewrite buffer中进行数据恢复了。

所以，虽然叫双写缓冲区，但是这个缓冲区不仅在内存中有，更多的是属于MySQL的系统表空间，属于磁盘文件的一部分。

那为什么要引入一个双写机制呢？

InnoDB的页大小一般是16KB，其数据校验也是针对这16KB来计算的，将数据写入到磁盘是以页为单位进行操作的。而操作系统写文件是以4KB作为单位的，那么每写一个InnoDB的页到磁盘上，操作系统需要写4个块。

而计算机硬件和操作系统，在极端情况下（比如断电）往往并不能保证这一操作的原子性，16K的数据，写入4K时，发生了系统断电或系统崩溃，只有一部分写是成功的，这种情况下会产生partial page write（部分页写入）问题。这时页数据出现不一样的情形，从而形成一个"断裂"的页，使数据产生混乱。在InnoDB存储引擎未使用doublewrite技术前，曾经出现过因为部分写失效而导致数据丢失的情况。

doublewrite是在一个连续的存储空间, 所以硬盘在写数据的时候是顺序写，而不是随机写，这样性能影响不大，相比不双写，降低了大概5-10%左右。

所以，在一些情况下可以关闭doublewrite以获取更高的性能。比如在slave上可以关闭，因为即使出现了partial
page write问题，数据还是可以从中继日志中恢复。比如某些文件系统ZFS本身有些文件系统本身就提供了部分写失效的防范机制，也可以关闭。

在数据库异常关闭的情况下启动时，都会做数据库恢复（redo）操作，恢复的过程中，数据库都会检查页面是不是合法（校验等等），如果发现一个页面校验结果不一致，则此时会用到双写这个功能。

有经验的同学也许会想到，如果发生写失效，可以通过重做日志(Redo Log)进行恢复啊！但是要注意，重做日志中记录的是对页的物理操作，如偏移量800,写' aaaa'记录，而不是页面的全量记录，而如果发生partial page write（部分页写入）问题时，出现问题的是未修改过的数据，此时重做日志(Redo Log)无能为力。写doublewrite buffer成功了，这个问题就不用担心了。

##### 具体操作：

![img](https://images2017.cnblogs.com/blog/1113510/201707/1113510-20170726195345906-321682602.png)

　doublewrite由两部分组成，一部分为内存中的doublewrite buffer，其大小为2MB，另一部分是磁盘上共享表空间(ibdata x)中连续的128个页，即2个区(extent)，大小也是2M。

　　1、当一系列机制触发数据缓冲池中的脏页刷新时，并不直接写入磁盘数据文件中，而是先拷贝至内存中的doublewrite buffer中；

　　2、接着从两次写缓冲区分两次写入磁盘共享表空间中(连续存储，顺序写，性能很高)，每次写1MB；

　　3、待第二步完成后，再将doublewrite buffer中的脏页数据写入实际的各个表空间文件(离散写)；(脏页数据固化后，即进行标记对应doublewrite数据可覆盖)

4、doublewrite的崩溃恢复

　　如果操作系统在将页写入磁盘的过程中发生崩溃，在恢复过程中，innodb存储引擎可以从共享表空间的doublewrite中找到该页的一个最近的副本，将其复制到表空间文件，再应用redo log，就完成了恢复过程。

默认是开启状态：可设置 innodb_doublewrite=0关闭。

相关参数:

 show status like "InnoDB_dblwr%";    -- 写到共享表空间的页数

 show VARIABLES like "%double%write%"; -- 写到数据文件的次数

虽然称之为buffer 实际上在共享表空间 物理文件中也有个2M的file文件，

doublewrite文件的默认大小是InnoDB page size * doublewrite page bytes.。

**doublewrite的副作用**

1、double write带来的写负载

　　1、double write是一个buffer, 但其实它是开在物理文件上的一个buffer, 其实也就是file, 所以它会导致系统有更多的fsync操作, 而硬盘的fsync性能是很慢的, 所以它会降低mysql的整体性能。

　　2、但是，doublewrite buffer写入磁盘共享表空间这个过程是连续存储，是顺序写，性能非常高，(约占写的%10)，牺牲一点写性能来保证数据页的完整还是很有必要的。

2、监控double write工作负载

```
mysql> show global status like '%dblwr%';
+----------------------------+-------+
| Variable_name              | Value |
+----------------------------+-------+
| Innodb_dblwr_pages_written | 7     |
| Innodb_dblwr_writes        | 3     |
+----------------------------+-------+
2 rows in set (0.00 sec)
```

　　关注点：Innodb_dblwr_pages_written / Innodb_dblwr_writes

　　开启doublewrite后，每次脏页刷新必须要先写doublewrite，而doublewrite存在于磁盘上的是两个连续的区，每个区由连续的页组成，一般情况下一个区最多有64个页，所以一次IO写入应该可以最多写64个页。

　　而根据以上系统Innodb_dblwr_pages_written与Innodb_dblwr_writes的比例来看，大概在3左右，远远还没到64(如果约等于64，那么说明系统的写压力非常大，有大量的脏页要往磁盘上写)，所以从这个角度也可以看出，系统写入压力并不高。

3、关闭double write适合的场景

　　1、海量DML

　　2、不惧怕数据损坏和丢失

　　3、系统写负载成为主要负载

```
mysql> show variables like '%double%';
+--------------------+-------+
| Variable_name      | Value |
+--------------------+-------+
| innodb_doublewrite | ON    |
+--------------------+-------+
1 row in set (0.04 sec)
```

　　作为InnoDB的一个关键特性，doublewrite功能默认是开启的，但是在上述特殊的一些场景也可以视情况关闭，来提高数据库写性能。静态参数，配置文件修改，重启数据库。

4、为什么没有把double write里面的数据写到data page里面呢？

　　1、double write里面的数据是连续的，如果直接写到data page里面，而data page的页又是离散的，写入会很慢。

　　2、double write里面的数据没有办法被及时的覆盖掉，导致double write的压力很大；短时间内可能会出现double write溢出的情况。





#### 1.2.2.2.InnoDB数据字典(Data Dictionary Header)

我们平时使用INSERT语句向表中插入的那些记录称之为用户数据，MySQL只是作为一个软件来为我们来保管这些数据，提供方便的增删改查接口而已。但是每当我们向一个表中插入一条记录的时候，MySQL先要校验一下插入语句对应的表存不存在，插入的列和表中的列是否符合，如果语法没有问题的话，还需要知道该表的聚簇索引和所有二级索引对应的根页面是哪个表空间的哪个页面，然后把记录插入对应索引的B+树中。所以说，MySQL除了保存着我们插入的用户数据之外，还需要保存许多额外的信息，比方说：

某个表属于哪个表空间，表里边有多少列，表对应的每一个列的类型是什么，该表有多少索引，每个索引对应哪几个字段，该索引对应的根页面在哪个表空间的哪个页面，该表有哪些外键，外键对应哪个表的哪些列，某个表空间对应文件系统上文件路径是什么。

上述这些数据并不是我们使用INSERT语句插入的用户数据，实际上是为了更好的管理我们这些用户数据而不得已引入的一些额外数据，这些数据也称为元数据。InnoDB存储引擎特意定义了一些列的内部系统表（internal system table）来记录这些这些元数据：

| 表名             | 描述                                                       |
| ---------------- | ---------------------------------------------------------- |
| SYS_TABLES       | 整个InnoDB存储引擎中所有的表的信息                         |
| SYS_COLUMNS      | 整个InnoDB存储引擎中所有的列的信息                         |
| SYS_INDEXES      | 整个InnoDB存储引擎中所有的索引的信息                       |
| SYS_FIELDS       | 整个InnoDB存储引擎中所有的索引对应的列的信息               |
| SYS_FOREIGN      | 整个InnoDB存储引擎中所有的外键的信息                       |
| SYS_FOREIGN_COLS | 整个InnoDB存储引擎中所有的外键对应列的信息                 |
| SYS_TABLESPACES  | 整个InnoDB存储引擎中所有的表空间信息                       |
| SYS_DATAFILES    | 整个InnoDB存储引擎中所有的表空间对应文件系统的文件路径信息 |
| SYS_VIRTUAL      | 整个InnoDB存储引擎中所有的虚拟生成列的信息                 |

这些系统表也被称为数据字典，它们都是以B+树的形式保存在系统表空间的某些页面中，其中SYS_TABLES、SYS_COLUMNS、SYS_INDEXES、SYS_FIELDS这四个表尤其重要，称之为基本系统表。

用户是不能直接访问InnoDB的这些内部系统表的，除非你直接去解析系统表空间对应文件系统上的文件。不过InnoDB考虑到查看这些表的内容可能有助于大家分析问题，所以在系统数据库information_schema中提供了一些以innodb_sys开头的表：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/035081b1c9b440f49a758775ea6697be.png)

在information_schema数据库中的这些以INNODB_SYS开头的表并不是真正的内部系统表（内部系统表就是我们上边唠叨的以SYS开头的那些表），而是在存储引擎启动时读取这些以SYS开头的系统表，然后填充到这些以INNODB_SYS开头的表中。

## 1.3.InnoDB的Buffer Pool

### 1.3.1.缓存的重要性

我们知道，对于使用InnoDB作为存储引擎的表来说，不管是用于存储用户数据的索引（包括聚簇索引和二级索引），还是各种系统数据，都是以页的形式存放在表空间中的，而所谓的表空间只不过是InnoDB对文件系统上一个或几个实际文件的抽象，也就是说我们的数据说到底还是存储在磁盘上的。

但是磁盘的速度慢，所以InnoDB存储引擎在处理客户端的请求时，当需要访问某个页的数据时，就会把完整的页的数据全部加载到内存中，也就是说即使我们只需要访问一个页的一条记录，那也需要先把整个页的数据加载到内存中。将整个页加载到内存中后就可以进行读写访问了，在进行完读写访问之后并不着急把该页对应的内存空间释放掉，而是将其缓存起来，这样将来有请求再次访问该页面时，就可以省去磁盘IO的开销了。

### 1.3.2.Buffer Pool

查询的一条数据就几十几百个byte，是不是调用存储引擎的接口就给我Server返回这么多呢？

如果对操作系统有所了解的话，就知道 不会这么设计

磁盘IO操作，相对内存效率是非常慢。

所以不论是innodb还是操作系统的引擎都会有一个预读取的概念 根据局部性原理来操作，

操作系统的块大小 ？ 4KB   预读取3块 加起来就是16KB

Innodb？ 16KB  （看时间把控 要不要后面的详情）

修改比较麻烦，需要清空数据初始化。而且大部分机器最优

可以到官网查看 innodb_page_size 也可以到客户端查看 SHOW GLOBAL STATUS LIKE '%innodb_page_size%'    默认16384

为了加速数据访问，把常用访问的数据放到此区域，避免每次都访问数据库。

哪些放到缓存池呢？最热的数据放到最近的地方   InnoDB里面最重要的一块

InnoDB为了缓存磁盘中的页，在MySQL服务器启动的时候就向操作系统申请了一片连续的内存，他们给这片内存起了个名，叫做Buffer Pool（中文名是缓冲池）。那它有多大呢？这个其实看我们机器的配置，默认情况下Buffer Pool只有8M大小，这个值其实是偏小的。

```
show variables like 'innodb_buffer_pool_size';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/da272fcb3d6f42a8a6b62e049cd10f80.png)

可以在启动服务器的时候配置innodb_buffer_pool_size参数的值，它表示BufferPool的大小，就像这样：

```
[server]

innodb_buffer_pool_size= 268435456
```

其中，268435456的单位是字节，也就是指定Buffer Pool的大小为256M。需要注意的是，Buffer Pool也不能太小，最小值为5M(当小于该值时会自动设置成5M)。

Buffer Pool内部组成

Buffer Pool中默认的缓存页大小和在磁盘上默认的页大小是一样的，都是16KB。为了更好的管理这些在Buffer Pool中的缓存页，InnoDB为每一个缓存页都创建了一些所谓的控制信息，这些控制信息包括该页所属的表空间编号、页号、缓存页在Buffer Pool中的地址、链表节点信息、一些锁信息以及LSN信息，当然还有一些别的控制信息。

每个缓存页对应的控制信息占用的内存大小是相同的，我们称为控制块。控制块和缓存页是一一对应的，它们都被存放到 Buffer Pool 中，其中控制块被存放到 Buffer Pool 的前边，缓存页被存放到 Buffer Pool 后边，所以整个Buffer Pool对应的内存空间看起来就是这样的：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/faf8b48ad7424410a7569ce920b9bb5c.png)

每个控制块大约占用缓存页大小的5%，而我们设置的innodb_buffer_pool_size并不包含这部分控制块占用的内存空间大小，也就是说InnoDB在为Buffer Pool向操作系统申请连续的内存空间时，这片连续的内存空间一般会比innodb_buffer_pool_size的值大5%左右。





#### 1.3.2.1.  free链表的管理

最初启动MySQL服务器的时候，需要完成对Buffer Pool的初始化过程，就是先向操作系统申请Buffer Pool的内存空间，然后把它划分成若干对控制块和缓存页。但是此时并没有真实的磁盘页被缓存到Buffer Pool中（因为还没有用到），之后随着程序的运行，会不断的有磁盘上的页被缓存到Buffer Pool中。

那么问题来了，从磁盘上读取一个页到Buffer Pool中的时候该放到哪个缓存页的位置呢？或者说怎么区分Buffer Pool中哪些缓存页是空闲的，哪些已经被使用了呢？最好在某个地方记录一下Buffer Pool中哪些缓存页是可用的，这个时候缓存页对应的控制块就派上大用场了，我们可以把所有空闲的缓存页对应的控制块作为一个节点放到一个链表中，这个链表也可以被称作free链表（或者说空闲链表）。刚刚完成初始化的Buffer Pool中所有的缓存页都是空闲的，所以每一个缓存页对应的控制块都会被加入到free链表中，假设该Buffer Pool中可容纳的缓存页数量为n，那增加了free链表的效果图就是这样的：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/b4f550a809a94f349f5d611f5aa00147.png)

有了这个free链表之后，每当需要从磁盘中加载一个页到Buffer Pool中时，就从free链表中取一个空闲的缓存页，并且把该缓存页对应的控制块的信息填上（就是该页所在的表空间、页号之类的信息），然后把该缓存页对应的free链表节点从链表中移除，表示该缓存页已经被使用了。

#### 1.3.2.2.  缓存页的哈希处理

我们前边说过，当我们需要访问某个页中的数据时，就会把该页从磁盘加载到Buffer Pool中，如果该页已经在Buffer Pool中的话直接使用就可以了。那么问题也就来了，我们怎么知道该页在不在Buffer Pool中呢？难不成需要依次遍历Buffer Pool中各个缓存页么？

我们其实是根据表空间号 + 页号来定位一个页的，也就相当于表空间号 + 页号是一个key，缓存页就是对应的value，怎么通过一个key来快速找着一个value呢？

所以我们可以用表空间号 + 页号作为key，缓存页作为value创建一个哈希表，在需要访问某个页的数据时，先从哈希表中根据表空间号 + 页号看看有没有对应的缓存页，如果有，直接使用该缓存页就好，如果没有，那就从free链表中选一个空闲的缓存页，然后把磁盘中对应的页加载到该缓存页的位置。

#### 1.3.2.3.  flush链表的管理

如果我们修改了Buffer Pool中某个缓存页的数据，那它就和磁盘上的页不一致了，这样的缓存页也被称为脏页（英文名：dirty page）。当然，最简单的做法就是每发生一次修改就立即同步到磁盘上对应的页上，但是频繁的往磁盘中写数据会严重的影响程序的性能。所以每次修改缓存页后，我们并不着急立即把修改同步到磁盘上，而是在未来的某个时间点进行同步。

但是如果不立即同步到磁盘的话，那之后再同步的时候我们怎么知道Buffer Pool中哪些页是脏页，哪些页从来没被修改过呢？总不能把所有的缓存页都同步到磁盘上吧，假如Buffer Pool被设置的很大，比方说300G，那一次性同步会非常慢。

所以，需要再创建一个存储脏页的链表，凡是修改过的缓存页对应的控制块都会作为一个节点加入到一个链表中，因为这个链表节点对应的缓存页都是需要被刷新到磁盘上的，所以也叫flush链表。链表的构造和free链表差不多。

#### 1.3.2.4. LRU链表的管理

##### 缓存不够的窘境

Buffer Pool对应的内存大小毕竟是有限的，如果需要缓存的页占用的内存大小超过了Buffer Pool大小，也就是free链表中已经没有多余的空闲缓存页的时候该咋办？当然是把某些旧的缓存页从Buffer Pool中移除，然后再把新的页放进来，那么问题来了，移除哪些缓存页呢？

为了回答这个问题，我们还需要回到我们设立Buffer Pool的初衷，我们就是想减少和磁盘的IO交互，最好每次在访问某个页的时候它都已经被缓存到Buffer Pool中了。假设我们一共访问了n次页，那么被访问的页已经在缓存中的次数除以n就是所谓的缓存命中率，我们的期望就是让缓存命中率越高越好。

从这个角度出发，回想一下我们的微信聊天列表，排在前边的都是最近很频繁使用的，排在后边的自然就是最近很少使用的，假如列表能容纳下的联系人有限，你是会把最近很频繁使用的留下还是最近很少使用的留下呢？当然是留下最近很频繁使用的了。

##### 简单的LRU链表

管理Buffer Pool的缓存页其实也是这个道理，当Buffer Pool中不再有空闲的缓存页时，就需要淘汰掉部分最近很少使用的缓存页。不过，我们怎么知道哪些缓存页最近频繁使用，哪些最近很少使用呢？

再创建一个链表，由于这个链表是为了按照最近最少使用的原则去淘汰缓存页的，所以这个链表可以被称为LRU链表（LRU的英文全称：Least Recently Used）。当我们需要访问某个页时，可以这样处理LRU链表：

如果该页不在Buffer Pool中，在把该页从磁盘加载到Buffer Pool中的缓存页时，就把该缓存页对应的控制块作为节点塞到LRU链表的头部。

如果该页已经缓存在Buffer Pool中，则直接把该页对应的控制块移动到LRU链表的头部。

也就是说：只要我们使用到某个缓存页，就把该缓存页调整到LRU链表的头部，这样LRU链表尾部就是最近最少使用的缓存页。所以当Buffer Pool中的空闲缓存页使用完时，到LRU链表的尾部找些缓存页淘汰就行了。

##### 划分区域的LRU链表

但是这种实现存在两种比较尴尬的情况：

情况一：InnoDB提供了预读（英文名：readahead）。所谓预读，就是InnoDB认为执行当前的请求可能之后会读取某些页面，就预先把它们加载到Buffer Pool中。根据触发方式的不同，预读又可以细分为下边两种：

###### 线性预读

InnoDB提供了一个系统变量innodb_read_ahead_threshold，如果顺序访问了某个区（extent）的页面超过这个系统变量的值，就会触发一次异步读取下一个区中全部的页面到Buffer Pool的请求。

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/3c2c542815eb4c47b00a8db31821cf90.png)

```
show variables like 'innodb_read_ahead_threshold';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/46dc910c532b4349b111aaaaa565133e.png)

这个innodb_read_ahead_threshold系统变量的值默认是56，我们可以在服务器启动时通过启动参数或者服务器运行过程中直接调整该系统变量的值。

###### 随机预读

如果Buffer Pool中已经缓存了某个区的13个连续的页面，不论这些页面是不是顺序读取的，都会触发一次异步读取本区中所有其他的页面到Buffer Pool的请求。![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/bfca76b672f7463d87447d48ad572e9e.png)

如果预读到Buffer Pool中的页成功的被使用到，那就可以极大的提高语句执行的效率。可是如果用不到呢？这些预读的页都会放到LRU链表的头部，但是如果此时Buffer Pool的容量不太大而且很多预读的页面都没有用到的话，这就会导致处在LRU链表尾部的一些缓存页会很快的被淘汰掉，也就是所谓的劣币驱逐良币，会大大降低缓存命中率。

所以InnoDB同时提供了innodb_random_read_ahead系统变量，它的默认值为OFF。

```
show variables like 'innodb_random_read_ahead';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/eb9c14c4b4f44357a4a4656354f950eb.png)

情况二：应用程序可能会写一些需要扫描全表的查询语句（比如没有建立合适的索引或者压根儿没有WHERE子句的查询）。

扫描全表意味着什么？意味着将访问到该表所在的所有页！假设这个表中记录非常多的话，那该表会占用特别多的页，当需要访问这些页时，会把它们统统都加载到Buffer Pool中，这也就意味着Buffer Pool中的所有页都被换了一次血，其他查询语句在执行时又得执行一次从磁盘加载到Buffer Pool的操作。而这种全表扫描的语句执行的频率也不高，每次执行都要把Buffer Pool中的缓存页换一次血，这严重的影响到其他查询对 Buffer Pool的使用，从而大大降低了缓存命中率。

总结一下上边说的可能降低Buffer Pool的两种情况：

加载到Buffer Pool中的页不一定被用到。

如果非常多的使用频率偏低的页被同时加载到Buffer Pool时，可能会把那些使用频率非常高的页从Buffer Pool中淘汰掉。

因为有这两种情况的存在，所以InnoDB把这个LRU链表按照一定比例分成两截，分别是：

一部分存储使用频率非常高的缓存页，所以这一部分链表也叫做热数据，或者称young区域。

另一部分存储使用频率不是很高的缓存页，所以这一部分链表也叫做冷数据，或者称old区域。

我们是按照某个比例将LRU链表分成两半的，不是某些节点固定是young区域的，某些节点固定是old区域的，随着程序的运行，某个节点所属的区域也可能发生变化。那这个划分成两截的比例怎么确定呢？对于InnoDB存储引擎来说，我们可以通过查看系统变量innodb_old_blocks_pct的值来确定old区域在LRU链表中所占的比例，比方说这样：

```
SHOW VARIABLES LIKE 'innodb_old_blocks_pct';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/46acfcb881b34f08b46043a195bdea3c.png)

从结果可以看出来，默认情况下，old区域在LRU链表中所占的比例是37%，也就是说old区域大约占LRU链表的3/8。这个比例我们是可以设置的，我们可以在启动时修改innodb_old_blocks_pct参数来控制old区域在LRU链表中所占的比例。在服务器运行期间，我们也可以修改这个系统变量的值，不过需要注意的是，这个系统变量属于全局变量。

有了这个被划分成young和old区域的LRU链表之后，InnoDB就可以针对我们上边提到的两种可能降低缓存命中率的情况进行优化了：

**针对预读的页面可能不进行后续访问情况的优化：**

InnoDB规定，当磁盘上的某个页面在初次加载到Buffer Pool中的某个缓存页时，该缓存页对应的控制块会被放到old区域的头部。这样针对预读到Buffer Pool却不进行后续访问的页面就会被逐渐从old区域逐出，而不会影响young区域中被使用比较频繁的缓存页。

针对全表扫描时，短时间内访问大量使用频率非常低的页面情况的优化：

在进行全表扫描时，虽然首次被加载到Buffer Pool的页被放到了old区域的头部，但是后续会被马上访问到，每次进行访问的时候又会把该页放到young区域的头部，这样仍然会把那些使用频率比较高的页面给顶下去。

有同学会想：可不可以在第一次访问该页面时不将其从old区域移动到young区域的头部，后续访问时再将其移动到young区域的头部。回答是：行不通！因为InnoDB规定每次去页面中读取一条记录时，都算是访问一次页面，而一个页面中可能会包含很多条记录，也就是说读取完某个页面的记录就相当于访问了这个页面好多次。

全表扫描有一个特点，那就是它的执行频率非常低，出现了全表扫描的语句也是我们应该尽快优化的对象。而且在执行全表扫描的过程中，即使某个页面中有很多条记录，也就是去多次访问这个页面所花费的时间也是非常少的。

所以在对某个处在old区域的缓存页进行第一次访问时就在它对应的控制块中记录下来这个访问时间，如果后续的访问时间与第一次访问的时间在某个时间间隔内，那么该页面就不会被从old区域移动到young区域的头部，否则将它移动到young区域的头部。上述的这个间隔时间是由系统变量innodb_old_blocks_time控制的：

```
SHOW VARIABLES LIKE 'innodb_old_blocks_time';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/647ab86437ca4fe0a291297ba4bf5e2c.png)

这个innodb_old_blocks_time的默认值是1000，它的单位是毫秒，也就意味着对于从磁盘上被加载到LRU链表的old区域的某个页来说，如果第一次和最后一次访问该页面的时间间隔小于1s（很明显在一次全表扫描的过程中，多次访问一个页面中的时间不会超过1s），那么该页是不会被加入到young区域的，
当然，像innodb_old_blocks_pct一样，我们也可以在服务器启动或运行时设置innodb_old_blocks_time的值，这里需要注意的是，如果我们把innodb_old_blocks_time的值设置为0，那么每次我们访问一个页面时就会把该页面放到young区域的头部。

综上所述，正是因为将LRU链表划分为young和old区域这两个部分，又添加了innodb_old_blocks_time这个系统变量，才使得预读机制和全表扫描造成的缓存命中率降低的问题得到了遏制，因为用不到的预读页面以及全表扫描的页面都只会被放到old区域，而不影响young区域中的缓存页。

##### 更进一步优化LRU链表

对于young区域的缓存页来说，我们每次访问一个缓存页就要把它移动到LRU链表的头部，这样开销是不是太大？

毕竟在young区域的缓存页都是热点数据，也就是可能被经常访问的，这样频繁的对LRU链表进行节点移动操作也会拖慢速度？为了解决这个问题，MySQL中还有一些优化策略，比如只有被访问的缓存页位于young区域的1/4的后边，才会被移动到LRU链表头部，这样就可以降低调整LRU链表的频率，从而提升性能。

### 1.3.3.多个Buffer Pool实例

我们上边说过，Buffer Pool本质是InnoDB向操作系统申请的一块连续的内存空间，在多线程环境下，访问Buffer Pool中的各种链表都需要加锁处理，在Buffer Pool特别大而且多线程并发访问特别高的情况下，单一的Buffer Pool可能会影响请求的处理速度。所以在Buffer Pool特别大的时候，我们可以把它们拆分成若干个小的Buffer Pool，每个Buffer Pool都称为一个实例，它们都是独立的，独立的去申请内存空间，独立的管理各种链表，所以在多线程并发访问时并不会相互影响，从而提高并发处理能力。

我们可以在服务器启动的时候通过设置innodb_buffer_pool_instances的值来修改Buffer Pool实例的个数

那每个Buffer Pool实例实际占多少内存空间呢？其实使用这个公式算出来的：

**innodb_buffer_pool_size/innodb_buffer_pool_instances**

也就是总共的大小除以实例的个数，结果就是每个Buffer Pool实例占用的大小。

不过也不是说Buffer Pool实例创建的越多越好，分别管理各个Buffer Pool也是需要性能开销的，InnoDB规定：当innodb_buffer_pool_size（默认128M）的值小于1G的时候设置多个实例是无效的，InnoDB会默认把innodb_buffer_pool_instances 的值修改为1。所以Buffer
Pool大于或等于1G的时候设置应该多个Buffer Pool实例。

### 1.3.4.  innodb_buffer_pool_chunk_size

在MySQL 5.7.5之前，Buffer Pool的大小只能在服务器启动时通过配置innodb_buffer_pool_size启动参数来调整大小，在服务器运行过程中是不允许调整该值的。不过MySQL在5.7.5以及之后的版本中支持了在服务器运行过程中调整Buffer Pool大小的功能，但是有一个问题，就是每次当我们要重新调整Buffer Pool大小时，都需要重新向操作系统申请一块连续的内存空间，然后将旧的Buffer Pool中的内容复制到这一块新空间，这是极其耗时的。所以MySQL决定不再一次性为某Buffer Pool实例向操作系统申请一大片连续的内存空间，而是以一个所谓的chunk为单位向操作系统申请空间。也就是说一个Buffer Pool实例其实是由若干个chunk组成的，一个chunk就代表一片连续的内存空间，里边儿包含了若干缓存页与其对应的控制块：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/dbf081ff23de46cd99cb7ca90e1cf85a.png)

正是因为发明了这个chunk的概念，我们在服务器运行期间调整Buffer Pool的大小时就是以chunk为单位增加或者删除内存空间，而不需要重新向操作系统申请一片大的内存，然后进行缓存页的复制。这个所谓的chunk的大小是我们在启动操作MySQL服务器时通过innodb_buffer_pool_chunk_size启动参数指定的，它的默认值是134217728，也就是128M。不过需要注意的是，innodb_buffer_pool_chunk_size的值只能在服务器启动时指定，在服务器运行过程中是不可以修改的。

```
SHOW VARIABLES LIKE 'innodb_buffer_pool_chunk_size';
```

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/6bc3f7b25ac049308885ea7818ca7e7e.png)

Buffer Pool的缓存页除了用来缓存磁盘上的页面以外，还可以存储锁信息、自适应哈希索引等信息。

### 1.3.5.  查看Buffer Pool的状态信息

MySQL给我们提供了SHOW ENGINE INNODB STATUS语句来查看关于InnoDB存储引擎运行过程中的一些状态信息，其中就包括Buffer Pool的一些信息，我们看一下（为了突出重点，我们只把输出中关于Buffer Pool的部分提取了出来）：

```
SHOW ENGINE INNODB STATUS\G
```

这里边的每个值都代表什么意思如下，知道即可：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/6ff5c96b5b8a4e368b455166f831cf04.png)

**Total large memory allocated**

代表Buffer Pool向操作系统申请的连续内存空间大小，包括全部控制块、缓存页、以及碎片的大小。

**Dictionary memory allocated**

为数据字典信息分配的内存空间大小，注意这个内存空间和Buffer Pool没啥关系，不包括在Total memory allocated中。

**Buffer pool size**

代表该Buffer Pool可以容纳多少缓存页，注意，单位是页！

**Free buffers**

代表当前Buffer Pool还有多少空闲缓存页，也就是free链表中还有多少个节点。

**Database pages**

代表LRU链表中的页的数量，包含young和old两个区域的节点数量。

**Old database pages**

代表LRU链表old区域的节点数量。

**Modified db pages**

代表脏页数量，也就是flush链表中节点的数量。

**Pending reads**

正在等待从磁盘上加载到Buffer Pool中的页面数量。

当准备从磁盘中加载某个页面时，会先为这个页面在Buffer Pool中分配一个缓存页以及它对应的控制块，然后把这个控制块添加到LRU的old区域的头部，但是这个时候真正的磁盘页并没有被加载进来，Pending reads的值会跟着加1。

**Pending writes**
LRU：即将从LRU链表中刷新到磁盘中的页面数量。

**Pending writes**
flush list：即将从flush链表中刷新到磁盘中的页面数量。

**Pending writes**
single page：即将以单个页面的形式刷新到磁盘中的页面数量。

**Pages made young**

代表LRU链表中曾经从old区域移动到young区域头部的节点数量。

**Page made not young** 

在将innodb_old_blocks_time设置的值大于0时，首次访问或者后续访问某个处在old区域的节点时由于不符合时间间隔的限制而不能将其移动到young区域头部时，Page made not young的值会加1。

**youngs/s：**代表每秒从old区域被移动到young区域头部的节点数量。

**non-youngs/s：**代表每秒由于不满足时间限制而不能从old区域移动到young区域头部的节点数量。

Pages read、created、written：代表读取，创建，写入了多少页。后边跟着读取、创建、写入的速率。

**Buffer pool hit rate：**

表示在过去某段时间，平均访问1000次页面，有多少次该页面已经被缓存到Buffer Pool了。

**young-making rate：**

表示在过去某段时间，平均访问1000次页面，有多少次访问使页面移动到young区域的头部了。

**not(young-making rate)：**

表示在过去某段时间，平均访问1000次页面，有多少次访问没有使页面移动到young区域的头部。

LRU len：代表LRU链表中节点的数量。

unzip_LRU：代表unzip_LRU链表中节点的数量。

I/O sum：最近50s读取磁盘页的总数。

I/O cur：现在正在读取的磁盘页数量。

I/O unzip sum：最近50s解压的页面数量。

I/O unzip cur：正在解压的页面数量。

### 1.3.3.InnoDB的内存结构总结

InnoDB的内存结构和磁盘存储结构图总结如下：

![image.png](https://fynotefile.oss-cn-zhangjiakou.aliyuncs.com/fynote/fyfile/5983/1656035756047/2603eace6ad04235a1bb5cd1bce517ca.png)

其中的Insert/Change Buffer主要是用于对二级索引的写入优化，Undo空间则是undo日志一般放在系统表空间，但是通过参数配置后，也可以用独立表空间存放，所以用虚线表示。

# 高频面试题：



## MySQL中有哪些存储引擎？

InnoDB存储引擎

InnoDB是MySQL的默认事务型引擎，也是最重要、使用最广泛的存储引擎。它被设计用来处理大量的短期(short-lived)事务，应该优先考虑InnoDB引擎。

MylSAM存储引擎

在MySQL 5.1及之前的版本，MyISAM是默认的存储引擎。MyISAM提供了大量的特性，包括全文索引、压缩、空间函数（GIS）等，但MyISAM不支持事务和行级锁，而且崩溃后无法安全恢复。MyISAM对整张表加锁，很容易因为表锁的问题导致典型的的性能问题。

Mrg_MylSAM

Merge存储引擎，是一组MyIsam的组合，也就是说，他将MyIsam引擎的多个表聚合起来，但是他的内部没有数据，真正的数据依然是MyIsam引擎的表中，但是可以直接进行查询、删除更新等操作。

Archive引擎

Archive存储引擎只支持INSERT和SELECT操作，会缓存所有的写并利用zlib对插入的行进行压缩，所以比MyISAM表的磁盘I/O更少。但是每次SELECT查询都需要执行全表扫描。所以Archive表适合日志和数据采集类应用，Archive引擎是一个针对高速插入和压缩做了优化的简单引擎。

Blackhole引擎

Blackhole引擎没有实现任何的存储机制，它会丢弃所有插入的数据，不做任何保存。可以在一些特殊的复制架构和日志审核时发挥作用。但这种引擎在应用方式上有很多问题，因此并不推荐。

CSV引擎

CSV引擎可以将普通的CSV文件(逗号分割值的文件）作为MySQL
的表来处理，但这种表不支持索引。因此CSV引擎可以作为一种数据交换的机制，非常有用。

Federated引擎

Federated引擎是访问其他MySQL服务器的一个代理，它会创建一个到远程MySQL服务器的客户端连接，并将查询传输到远程服务器执行，然后提取或者发送需要的数据。默认是禁用的。

Memory 引擎

Memory表至少比MyISAM 表要快一个数量级，数据文件是存储在内存中。Memory表的结构在重启以后还会保留，但数据会丢失。

Memroy表在很多场景可以发挥好的作用:

用于查找(lookup）或者映射(mapping）表，例如将邮编和州名映射的表。

用于缓存周期性聚合数据(periodically
aggregated data)的结果。

用于保存数据分析中产生的中间数据。

Memory表支持 Hash索引，因此查找操作非常快。Memroy表是表级锁，因此并发写入的性能较低，每行的长度是固定的，可能导致部分内存的浪费。

NDB集群引擎

使用MySQL服务器、NDB集群存储引擎，以及分布式的、share-nothing 的、容灾的、高可用的NDB数据库的组合，被称为MySQL集群（(MySQL
Cluster)。

## MyISAM和InnoDB的区别是什么?

MyISAM引擎是5.1版本之前的默认引擎，支持全文检索、压缩、空间函数等，但是不支持事务和行级锁，所以一般用于有大量查询少量插入的场景来使用，而且MyISAM不支持外键，并且索引和数据是分开存储的。

InnoDB是基于聚簇索引建立的，和MyISAM相反它支持事务、外键，并且通过MVCC来支持高并发，索引和数据存储在一起。

## 请概述下数据库的范式设计

目前关系数据库有六种范式，常见范式：第一范式：1NF是对属性的原子性约束，要求属性具有原子性，不可再分解；第二范式：2NF是对记录的惟一性约束，要求记录有惟一标识，即实体的惟一性；第三范式：3NF是对字段冗余性的约束，即任何字段不能由其他字段派生出来，它要求字段没有冗余。。

范式化设计优缺点:

优点:可以尽量得减少数据冗余，使得更新快，体积小；缺点:对于查询需要多个表进行关联，减少写得效率增加读得效率，更难进行索引优化

反范式化:

优点:可以减少表得关联，可以更好得进行索引优化；缺点:数据冗余以及数据异常，数据得修改需要更多的成本，常见的反范式设计有缓存、冗余等等。

## 数据库表设计时，字段你会如何选择？

更小的通常更好，应该尽量使用可以正确存储数据的最小数据类型。更小的数据类型通常更快，因为它们占用更少的磁盘、内存和CPU缓存，并且处理时需要的CPU周期也更少。但是要确保没有低估需要存储的值的范围。

简单就好，简单数据类型的操作通常需要更少的CPU周期。例如，整型比字符操作代价更低，比如应该使用MySQL内建的类型而不是字符串来存储日期和时间。

尽量避免NULL，如果查询中包含可为NULL的列，对MySQL来说更难优化，因为可为NULL的列使得索引、索引统计和值比较都更复杂。可为NULL的列会使用更多的存储空间，在MySQL里也需要特殊处理。当可为NULL的列被索引时，每个索引记录需要一个额外的字节。

## mysql里记录货币用什么字段类型好？

MySQL既支持精确类型的存储DECIMAL类型，也支持不精确类型存储FLOAT和 DOUBLE类型。对于货币记录，应该选择DECIMAL类型，但是DECIMAL类型是以字符串形式存放的，所以性能会有影响。

作为替代方案，可以在数据量比较大的而且要求精度时，虑使用BIGINT代替DECIMAL，将需要存储的货币单位根据小数的位数乘以相应的倍数即可。

## 谈谈MySQL里的字符串类型

MySQL里的字符串类型有：SET、BLOB、ENUM、VARCHAR、CHAR、TEXT。VARCHAR和 CHAR是两种最主要的字符串类型。VARCHAR类型用于存储可变长字符串，大部分的业务情况下比定长类型更节省空间，CHAR类型是定长的，CHAR适合存储很短的字符串，或者所有值定长或都接近同一个长度。

使用BLOB和TEXT则要慎重，一般把 BLOB或TEXT 列分离到单独的表中，还可以对BLOB或TEXT 列使用合成的(Synthetic)索引，就是根据大文本字段的内容建立一个散列值并单独存储在数据列中，可以通过检索散列值找到数据行。如果表中的字段的取值是固定几个字符串，可以使用枚举列代替常用的字符串类型。



## 三高项目数据库设计？

分库分表的情况：

单库出现性能瓶颈，通常有以下几种情况：

- 数据库服务器磁盘空间不足，但是无法扩容，导致写数据异常；
- 数据库服务器 CPU 压力过大，无法升配，导致读写性能较慢；
- 数据库服务器内存不足，无法扩容，导致读写性能瓶颈；
- 数据库服务器网络带宽不足，无法升配，导致读写性能瓶颈；
- 数据库服务器连接数过多，无法升配，导致客户端连接等待/超时；

单表出现性能瓶颈，通常是因为单表数据量过大，导致读写性能较慢。



**水平分库**

水平分库是指，将表水平切分后分到不同的数据库，使得每个库具有相同的表，表中的数据不相同，水平分库一般是伴随水平分表。

水平分表指的表结构不变，将单表数据切分成多表。切分后的结果：

- 每个表的结构一样；
- 每个表的数据不一样；
- 所有表的数据并集为全量数据

 **垂直分表**

垂直分表指将存在一张表中的字段切分到多张表。切分后的结果：

- 每个表的结构不一样；
- 每个表的数据不一样；
- 所有表的字段并集是原表的字段；



#### 实战：

可借助mycat 或shardingJDBC

配置：1。master主节点 开启binlog

默认关闭。开启1%性能损耗，cnf配置文件指定 log-bin=binlog-name 或者默认主机名用set sql_log_bin=1 命令开启

show global variables like "%log_bin%";  查看相关参数情况

binlog 的三种 类型

show global variables like "binlog_format"

参数开启 binlog_format=row | statement | mixed

**Binary Logging Formats API查看**

https://dev.mysql.com/doc/refman/5.7/en/binary-log-formats.html

建议生产环境用row每行(默认：修改的行。更好恢复但量大少用alter table) ，

statement(会修改的sql。特殊情况会出问题比如 sleep() ;last_insert_id(); user-defined function)  

 mixed自动选择

2.

slave节点指定某个binlog 文件，以及同步的offset  , 以及主节点IP  用户名密码

在MySQL 5.7.7之前，默认的格式是STATEMENT。 在MySQL 5.7.7及以上版本中，默认为ROW。 异常:在NDB集群中，默认是MIXED; NDB集群不支持基于语句的复制。

**具体操作：**

我这里的 主从虚拟机 分别是  172.31.26.120    和  172.31.23.118

开启 主节点的binlog

 我这 虚拟机  安装路径cd /var/lib/mysql/ 

修改 my.cnf    目录在 vi  /etc/my.cnf

加入	 log-bin=/var/lib/mysql/mysql-bin

服务标记 server-id=1001 

然后重启服务：

systemctl restart mysqld

   当然你也到安装目录去重启

监测是否主已 OK

ls /var/lib/mysql/   查看是否已有bin.前缀的 文件    当然你也可以通过命令查看参数 show global variables like "%log_bin%";

设置白名单 用户：系统库mysql里面的user表加入 tianming   IP地址为 172.31.23.118

-- 创建用户和授权

GRANT REPLICATION SLAVE  ON*.* TO 'gp'@'172.31.23.118'IDENTIFIED BY 'Admin_123';

--刷新权限

flush privileges;

接下来slave 节点  连上slave节点的 mysql 

mysql -uroot -pAdmin_123

配置 ：my.conf 添加  server-id=1002

否则会报错：ERROR 1794 (HY000): Slave is not configured or failed to initialize properly. You must at least set --server-id to enable either a master or a slave. Additional error messages can be found in the MySQL error log

然后重启服务：systemctl restart mysqld   当然你也到安装目录去重启

再执行 脚本命令  . 设置主节点的IP  连上去的用户名密码   以及master 节点的

show master status\G;

 的file 和position   文件和位置  11278   206215

再到从节点执行如下命令：注意修改 ip 用户名密码以及 主节点查的 position

change master to master_host='172.28.55.36',master_user='root', master_password='Admin_123', master_port=3306, master_log_file='mysql-bin.000001', master_log_pos=206215;

可能异常 ：STOP SLAVE IO_THREAD FOR CHANNEL ''； 执行如上命令  

```
start slave;
查看slave 同步状态
show slave status\G;
-- 可见Slave_IO_Running  和 Slave_SQL_Running  是否YES
可能异常 连接失败：可在IO_Error Master command COM_REGISTER_SLAVE failed: Access denied for user 'tm'@'%' (using password: YES) (Errno: 1045)
当权限显示为
REPLICATION是方才正确。此时，登陆从服务器再次执行
start slave命令即可。

可能异常：Could not execute Delete_rows event on table mysql.user; Can't find record in 'user', Error_code: 1032; handler error HA_ERR_KEY_NOT_FOUND; the event's master log mysql-bin.000001, end_log_pos 5551
原因：master需要删除 从不存在出错  可能节点位置变更了 
方案1尝试跳过：stop slave;set global sql_slave_skip_counter=1;start slave;
方案2修改配置的post：重新查看 主节点的status 修改post

change master to master_host='172.31.26.120',master_user='tm', master_password='Admin_123', master_port=3306, master_log_file='mysql-bin.000001', master_log_pos=8784;
注意如果主从库原本库不同，需要新建否则binlog中没有此 是无法同步的。
```



测试 主库新建数据库，刷新从 即可见到同步的情况

**主从不同步怎么办？**

可能异常：不能同步 原因同步已不一致 。重新拿到master的 position 207888

stop slave；  再次 

change master to master_host='172.28.55.36',master_user='root', master_password='Admin_123', master_port=3306, master_log_file='mysql-bin.000001', master_log_pos=207888;

再次开启 start slave；

问题： 从库也可新增和修改。

方案：

set global read_only=1; 

  \#1是只读，0是读写

查看状态 ：

show global variables like "%read_only%";

注意：read_only=1只读模式，不影响同步主库的新增和修改。 以及可以限定普通用户进行数据修改的操作，但不会限定具有super权限的用户的数据修改操作；在MySQL中设置read_only=1后，普通的应用用户进行insert、update、delete等会产生数据变化的DML操作时，都会报出数据库处于只读模式不能发生数据变化的错误，但具有super权限的用户，例如在本地或远程通过root用户登录到数据库，还是可以进行数据变化的DML操作；

如果需要设置root 的super权限用户也不能修改 可以  

set global super_read_only=1; 

如此：修改就会 ：ERROR 1290 (HY000): The MySQL server is running with the --super-read-only option so it cannot execute this statement

不推荐使用毕竟以防万一，还有个领导可以越权纠正问题。

当然如果搭建集群  

多个从节点的话 也提供了 负载均衡 的算法。

代码实战 ：

先主库手动创建 ：readwritedb   并选择utf8

 并创建表 ：

DROP TABLE IF EXISTS t_order;

CREATE TABLE t_order (

order_id bigint NOT NULL AUTO_INCREMENT,

user_id int NOT NULL,

address_id bigint NOT NULL,

status varchar(50) DEFAULT NULL,

PRIMARY KEY (order_id)

) ENGINE=InnoDB   DEFAULT CHARSET=utf8;

启动服务 

测试地址：http://localhost:8080/swagger-ui.html

这里配置集成了 swagger /ˈswæɡər/

进入 /order  根据example 改下ID 为1 可见结果200

可以到控制台搜（Ctrl+K）write-ds 看到时写到哪里。  当然也可到数据库确认 是否都OK

再试试查询：/order/{id}  

可见控制台 的 read-ds

主节点 能不能多个呢？可以借助第三方插件比如keepalied  backup一个



## VARCHAR(M)最多能存储多少数据？

对于VARCHAR(M)类型的列最多可以定义65535个字节。其中的M代表该类型最多存储的字符数量，但在实际存储时并不能放这么多。

MySQL对一条记录占用的最大存储空间是有限制的，除了BLOB或者TEXT类型的列之外，其他所有的列（不包括隐藏列和记录头信息）占用的字节长度加起来不能超过65535个字节。所以MySQL服务器建议我们把存储类型改为TEXT或者BLOB的类型。这个65535个字节除了列本身的数据之外，还包括一些其他的数据，从行记录格式我们可以得知，为了存储一个VARCHAR(M)类型的列，其实需要占用3部分存储空间：真实数据、真实数据占用字节的长度、NULL值标识，如果该列有NOT
NULL属性则可以没有这部分存储空间。

我们假设表中只有一个VARCHAR字段的情况：

如果该VARCHAR类型的列**没有**NOT NULL属性，那最多只能存储65532个字节的数据，因为真实数据的长度可能占用2个字节，NULL值标识需要占用1个字节。

如果VARCHAR类型的列**有**NOT NULL属性，那最多只能存储65533个字节的数据，因为真实数据的长度可能占用2个字节，不需要NULL值标识。

如果VARCHAR(M)类型的列使用的不是ascii字符集，那M的最大取值取决于该字符集表示一个字符最多需要的字节数。在列的值允许为NULL的情况下，gbk字符集表示一个字符最多需要2个字节，那在该字符集下，M的最大取值就是32766（也就是：65532/2），也就是说最多能存储32766个字符；utf8字符集表示一个字符最多需要3个字节，那在该字符集下，M的最大取值就是21844，就是说最多能存储21844（也就是：65532/3）个字符。

不管如何，请牢记：**MySQL****一个行中的所有列（不包括隐藏列和记录头信息）占用的字节长度加起来不能超过65535****个字节**。

## 什么是虚拟生成列？

虚拟生成列又叫GeneratedColumn，是MySQL 5.7引入的新特性，就是数据库中这一列由其他列计算而得。在MySQL 5.7中，支持两种Generated
Column，即Virtual
Generated Column（虚拟生成的列）和Stored
Generated Column（存储生成的列），二者含义如下：

1、Virtual
Generated Column（虚拟生成的列）：不存储该列值，即MySQL只是将这一列的元信息保存在数据字典中，并不会将这一列数据持久化到磁盘上，而是当读取该行时，触发触发器对该列进行计算显示。

2、Stored
Generated Column（存储生成的列）： 存储该列值，即该列值在插入或更新行时进行计算和存储。所以相对于Virtual Column列需要更多的磁盘空间，与Virtual
Column相比并没有优势。因此，MySQL
5.7中，不指定Generated
Column的类型，默认是Virtual
Column

在表中允许Virtual
Column和Stored
Column的混合使用

提高效率：由于mysql在普通索引上加函数会造成索引失效，造成查询性能下降，Generated Column（函数索引）刚好可以解决这个问题，可以在Generated Column加上索引来提高效率。但是不能建立虚拟列和真实列的联合索引，同时虚拟列是不允许创建主键索引和全文索引。

创建虚拟生成列的语法：

CREATE TABLE `triangle` (

`a` double DEFAULT NULL,

`b` double DEFAULT NULL,

`sidec` double GENERATED
ALWAYS AS (SQRT(a * a + b * b))

) ;

alter table triangle add column sided tinyint(1) generated always as
(a*b) virtual;

## 请说下事务的基本特性

事务应该具有4个属性：原子性、一致性、隔离性、持久性。这四个属性通常称为ACID特性。

原子性指的是一个事务中的操作要么全部成功，要么全部失败。

一致性指的是数据库总是从一个一致性的状态转换到另外一个一致性的状态。比如A转账给B100块钱，假设中间sql执行过程中系统崩溃A也不会损失100块，因为事务没有提交，修改也就不会保存到数据库。

隔离性指的是一个事务的修改在最终提交前，对其他事务是不可见的。

持久性指的是一旦事务提交，所做的修改就会永久保存到数据库中。

## 事务并发可能引发什么问题？

当一个事务读取到了另外一个事务修改但未提交的数据，被称为脏读。

当事务内相同的记录被检索两次，且两次得到的结果不同时，此现象称为不可重复读。

在事务执行过程中，事务2将新记录添加到正在读取的事务1中，导致事务1按照某个相同条件多次读取记录时，后读取时读到了之前没有读到的记录，发生幻读。

事务2中是删除了符合的记录而不是插入新记录，那事务1中之后再根据条件读取的记录变少了，在MySQL中这种现象不属于幻读，相当于对每一条记录都发生了不可重复读的现象。

## 请描述下MySQL中InnoDB支持的四种事务隔离和区别

read uncommitted：未提交读，可能发生脏读、不可重复读和幻读问题。

read committed：提交读，可能发生不可重复读和幻读问题，但是不会发生脏读问题。

repeatable read：可重复读，在SQL标准中可能发生幻读问题，但是不会发生脏读和不可重复读的问题，但是MySQL通过MVCC基本解决了幻读问题。这也是MySQL的缺省隔离级别。

serializable：串行化读，脏读、不可重复读和幻读问题都不会发生。

## MySQL有哪些索引类型

从数据结构角度可分为B+树索引、哈希索引、以及FULLTEXT索引（现在MyISAM和InnoDB引擎都支持了）和R-Tree索引（用于对GIS数据类型创建SPATIAL索引）；

从物理存储角度可分为聚集索引（clustered index）、非聚集索引（non-clustered index）；

从逻辑角度可分为主键索引、普通索引，或者单列索引、多列索引、唯一索引、非唯一索引等等。

## 简单描述MySQL各个索引的区别

索引是一种特殊的文件(InnoDB数据表上的索引是表空间的一个组成部分)，它们包含着对数据表里所有记录的引用指针。

普通索引(由关键字KEY或INDEX定义的索引)的唯一任务是加快对数据的访问速度。

普通索引允许被索引的数据列包含重复的值。如果能确定某个数据列将只包含彼此各不相同的值，在为这个数据列创建索引的时候就应该用关键字UNIQUE把它定义为一个唯一索引。也就是说，唯一索引可以保证数据记录的唯一性。

主键，是一种特殊的唯一索引，在一张表中只能定义一个主键索引，主键用于唯一标识一条记录，使用关键字 PRIMARY KEY 来创建。

索引可以覆盖多个数据列，如像INDEX(columnA, columnB)索引，这就是联合索引。

## MySQL的索引对数据库的性能有什么影响

索引（Index）是帮助MySQL高效获取数据的数据结构，所以索引可以极大的提高数据的查询速度。

但是每建立一个索引都要为它建立一棵B+树，一棵很大的B+树由许多数据页组成会占据很多的存储空间。

而且每次对表中的数据进行增、删、改操作时，都需要去修改各个B+树索引，同时这些操作可能会对节点和记录的排序造成破坏，所以存储引擎需要额外的时间进行一些记录移位，页面分裂、页面回收的操作来维护好节点和记录的排序。如果我们建了许多索引，每个索引对应的B+树都要进行相关的维护操作，这必然会对性能造成影响。

## 为什么MySQL的索引要使用B+树而不是B树？

答案见下一小节

## InnoDB一棵B+树可以存放多少行数据？

[当然在实际的数据库中，一个节点可以存储的数据可以很多，为什么？]()

计算机在存储数据的时候，有最小存储单元，这就好比我们今天进行现金的流通最小单位是一毛。在计算机中磁盘存储数据最小单元是扇区，一个扇区的大小是 512 字节，而文件系统（例如XFS/EXT4）他的最小单元是块，一个块的大小是 4k，而对于我们的 InnoDB 存储引擎也有自己的最小储存单元——页（Page），一个页的大小是 16K。Innodb 的所有数据文件（后缀为 ibd 的文件），他的大小始终都是 16384（16k）的整数倍。

数据表中的数据都是存储在页中的，所以一个页中能存储多少行数据呢？假设一行数据的大小是 1k，那么一个页可以存放 16 行这样的数据。

对于B+树而言，只有叶子节点存放数据，非叶子节点存放的是只保存索引信息和下一层节点的指针信息。一个非叶子节点能存放多少指针？

其实这也很好算，我们假设主键 ID 为常用的bigint 类型，长度为 8 字节，而指针大小在 InnoDB 源码中设置为 6 字节，这样一共 14 字节，我们一个页中能存放多少这样的单元，其实就代表有多少指针，即 16384/14=1170个。

那么可以算出一棵高度为2的B+树，存在一个根节点和若干个叶子节点能存放 1170*16=18720 条这样的数据记录。

根据同样的原理我们可以算出一个高度为 3 的
**B+ ****树可以存放： 1170*1170*16=21902400 ****条这样的记录。**

所以在 InnoDB 中 B+ 树高度一般为 1-3 层，就能满足千万级的数据存储。

**那么为什么MySQL****的索引要使用B+****树而不是B****树？**

而 B 树和B+树的最大区别就是，B 树不管叶子节点还是非叶子节点，都会保存数据，这样导致在非叶子节点中能保存的指针数量变少（有些资料也称为扇出），指针少的情况下要保存大量数据，只能增加树的高度，导致 IO 操作变多，查询性能变低。

## HashMap适合做数据库索引吗？

1、hash表只能匹配是否相等，不能实现范围查找；

2、当需要按照索引进行order by时，hash值没办法支持排序；

3、组合索引可以支持部分索引查询，如(a,b,c)的组合索引，查询中只用到了阿和b也可以查询的，如果使用hash表，组合索引会将几个字段合并hash，没办法支持部分索引；

4、当数据量很大时，hash冲突的概率也会非常大。

## InnoDB中只有B+树索引吗？

InnoDB存储引擎不仅仅有B+树索引，它还支持全文索引、哈希索引。

InnoDB存储引擎内部自己去监控索引表，如果监控到某个索引经常用，那么就认为是热数据，然后内部自己创建一个hash索引，称之为自适应哈希索引( Adaptive Hash Index,AHI)。使用的哈希函数采用除法散列方式，其冲突机制采用链表方式。我们对这个自适应哈希索引能够干预的地方很少，只能设定是否启用和分区个数。

从MySQL5.6.x开始，InnoDB开始支持全文检索，内部的实现机制就是倒排索引。但是MySQL整体架构上对全文检索支持并不好而且限制很多，比如每张表只能有一个全文检索的索引，不支持没有单词界定符( delimiter）的语言，所以如果有大批量或者专门的全文检索需求，还是应该选择专门的全文检索引擎。

## 什么是密集索引和[稀疏索引]()？

密集索引的定义：叶子节点保存的不只是键值，还保存了位于同一行记录里的其他列的信息，由于密集索引决定了表的物理排列顺序，一个表只有一个物理排列顺序，所以一个表只能创建一个密集索引。

稀疏索引：叶子节点仅保存了键位信息以及该行数据的地址，有的稀疏索引只保存了键位信息机器主键。

mysam存储引擎，不管是主键索引，唯一键索引还是普通索引都是稀疏索引，innodb存储引擎：有且只有一个密集索引。

所以，密集索引就是innodb存储引擎里的聚簇索引，稀疏索引就是innodb存储引擎里的普通二级索引。

## 为什么要用自增列作为主键？

1、如果我们定义了主键(PRIMARY
KEY)，那么InnoDB会选择主键作为聚集索引。

如果没有显式定义主键，则InnoDB会选择第一个不包含有NULL值的唯一索引作为主键索引。

如果也没有这样的唯一索引，则InnoDB会选择内置6字节长的ROWID作为隐含的聚集索引(ROWID随着行记录的写入而主键递增，这个ROWID不像ORACLE的ROWID那样可引用，是隐含的)。

2、[数据记录本身被存于主索引（一颗]()B+Tree）的叶子节点上，这就要求同一个叶子节点内（大小为一个内存页或磁盘页）的各条数据记录按主键顺序存放

因此每当有一条新的记录插入时，MySQL会根据其主键将其插入适当的节点和位置，如果页面达到装载因子（InnoDB默认为15/16），则开辟一个新的页（节点）

3、如果表使用自增主键，那么每次插入新的记录，记录就会顺序添加到当前索引节点的后续位置，当一页写满，就会自动开辟一个新的页

4、如果使用非自增主键（如果身份证号或学号等），由于每次插入主键的值近似于随机，因此每次新纪录都要被插到现有索引页得中间某个位置。此时MySQL不得不为了将新记录插到合适位置而移动数据，甚至目标页面可能已经被回写到磁盘上而从缓存中清掉，此时又要从磁盘上读回来，这增加了很多开销同时频繁的移动、分页操作造成了大量的碎片，得到了不够紧凑的索引结构，后续不得不通过OPTIMIZE
TABLE来重建表并优化填充页面。

## 主键和唯一键有什么区别？

主键不能重复，不能为空，唯一键不能重复，可以为空。

建立主键的目的是让外键来引用。

一个表最多只有一个主键，但可以有很多唯一键

## 说说对SQL语句优化有哪些方法？（选择几条）

（1）Where子句中：where表之间的连接必须写在其他Where条件之前，那些可以过滤掉最大数量记录的条件必须写在Where子句的末尾.HAVING最后。

（2）用EXISTS替代IN、用NOT EXISTS替代NOT IN。

（3） 避免在索引列上使用计算

（4）避免在索引列上使用IS NULL和IS NOT NULL

（5）对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。

（6）应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描

（7）应尽量避免在 where 子句中对字段进行表达式操作，这将导致引擎放弃使用索引而进行全表扫描。

## 如何提高insert的性能？

答：有如下方法：

a)合并多条 insert 为一条，即： insert into t values(a,b,c),  (d,e,f) ,,,

原因分析：主要原因是多条insert合并后日志量（MySQL的binlog和innodb的事务日志） 减少了，降低日志刷盘的数据量和频率，从而提高效率。通过合并SQL语句，同时也能减少SQL语句解析的次数，减少网络传输的IO。

b)修改参数bulk_insert_buffer_size， 调大批量插入的缓存；

c)设置 innodb_flush_log_at_trx_commit = 0 ，相对于 innodb_flush_log_at_trx_commit = 1 可以十分明显的提升导入速度；

（备注：innodb_flush_log_at_trx_commit
参数对 InnoDB Log 的写入性能有非常关键的影响。该参数可以设置为0，1，2，解释如下：

0：log buffer中的数据将以每秒一次的频率写入到log file中，且同时会进行文件系统到磁盘的同步操作，但是每个事务的commit并不会触发任何log buffer 到log file  的刷新或者文件系统到磁盘的刷新操作;

1：在每次事务提交的时候将log
buffer 中的数据都会写入到log file，同时也会触发文件系统到磁盘的同步;

2：事务提交会触发log buffer 到log file的刷新，但并不会触发磁盘文件系统到磁盘的同步。此外，每秒会有一次文件系统到磁盘同步操作。）

d）手动使用事务

因为mysql默认是autocommit的，这样每插入一条数据，都会进行一次commit；所以，为了减少创建事务的消耗，我们可用手工使用事务，即START TRANSACTION;insert 。。,insert。。 commit；即执行多个insert后再一起提交；一般1000条insert 提交一次。

## 什么是覆盖索引？什么是回表查询？

InnoDb存储引擎有两大类索引聚集索引和普通（辅助/二级）索引，聚簇索引的叶子节点存储行记录，因此InnoDb必须要有聚簇索引且仅有一个聚簇索引，而普通索引的叶子节点只存储索引值和主键值，所以，通过聚簇索引一次性能获取所有列的数据，普通索引一般不行。

当我们SQL语句的中列无法在普通索引中获得时，就需要主键值到聚簇索引中获取相关的数据，这个过程就被称为回表。

而如果我们使用联合索引，使得SQL所需的所有列数据在这个索引上就能获得时，我们称为发生了索引覆盖或者覆盖索引。

## 什么是三星索引？

对于一个查询而言，一个三星索引，可能是其最好的索引。

如果查询使用三星索引，一次查询通常只需要进行一次磁盘随机读以及一次窄索引片的扫描，因此其相应时间通常比使用一个普通索引的响应时间少几个数量级。

一个查询相关的索引行是相邻的或者至少相距足够靠近的则获得一星；

如果索引中的数据顺序和查找中的排列顺序一致则获得二星；

如果索引中的列包含了查询中需要的全部列则获得三星。

三星索引在实际的业务中如果无法同时达到，一般我们认为第三颗星最重要，第一和第二颗星重要性差不多，根据业务情况调整这两颗星的优先度。

## 大表关联查询优化

一个6亿的表a，一个3亿的表b，通过tid关联，你如何最快的查询出满足条件的第50000到第50200中的这200条数据记录。

1、如果A表TID是自增长,并且是连续的,B表的ID为索引

select * from
a,b where a.tid = b.id and a.tid>500000 limit 200;

2、如果A表的TID不是连续的,那么就需要使用覆盖索引.TID要么是主键,要么是辅助索引,B表ID也需要有索引。

select * from b
, (select tid from a limit 50000,200) a where b.id = a .tid;

## [SELECT *] 和[SELECT 全部字段]有何优缺点？

1>.前者要解析数据字典，后者不需要

2>.结果输出顺序，前者与建表列顺序相同，后者按指定字段顺序。

3>.表字段改名，前者不需要修改，后者需要改

4>.后者可以建立索引进行优化，前者无法优化

5>.后者的可读性比前者要高

## 请概述下什么是MySQL的分区表

表分区，是指根据一定规则，将数据库中的一张表分解成多个更小的，容易管理的部分。从逻辑上看，只有一张表，但是底层却是由多个物理分区组成。

1、表分区与分表的区别

分表：指的是通过一定规则，将一张表分解成多张不同的表。比如将用户订单记录根据时间成多个表。

分表与分区的区别在于：分区从逻辑上来讲只有一张表，而分表则是将一张表分解成多张表。

2、表分区的好处？

1）存储更多数据。分区表的数据可以分布在不同的物理设备上，从而高效地利用多个硬件设备。和单个磁盘或者文件系统相比，可以存储更多数据

2）优化查询。在where语句中包含分区条件时，可以只扫描一个或多个分区表来提高查询效率；涉及sum和count语句时，也可以在多个分区上并行处理，最后汇总结果。

3）分区表更容易维护。例如：想批量删除大量数据可以清除整个分区。

3、分区表的限制因素

一个表最多只能有1024个分区

如果分区字段中有主键或者唯一索引的列，那么多有主键列和唯一索引列都必须包含进来。即：分区字段要么不包含主键或者索引列，要么包含全部主键和索引列。

分区表中无法使用外键约束

MySQL的分区适用于一个表的所有数据和索引，不能只对表数据分区而不对索引分区，也不能只对索引分区而不对表分区，也不能只对表的一部分数据分区。

4、分区表的类型

RANGE分区： 这种模式允许将数据划分不同范围。例如可以将一个表通过年份划分成若干个分区

LIST分区： 这种模式允许系统通过预定义的列表的值来对数据进行分割。按照List中的值分区，与RANGE的区别是，range分区的区间范围值是连续的。

HASH分区 ：这中模式允许通过对表的一个或多个列的Hash
Key进行计算，最后通过这个Hash码不同数值对应的数据区域进行分区。例如可以建立一个对表主键进行分区的表。

KEY分区 ：上面Hash模式的一种延伸，这里的Hash
Key是MySQL系统产生的。

Column分区：需要和RANGE和List结合，支持字符串和日期的分区，也支持多列分区。

复合分区/子分区：分区之下还可以再分区。

5、在实际工作中用分区表比较少

1）分区表，分区键设计不太灵活，如果不走分区键，很容易出现全表锁

2）自己分库分表，自己掌控业务场景与访问模式，可控。分区表，研发写了一个sql，都不确定mysql是怎么操作的，不太可控

3）分区表无论怎么分，都是在一台机器上，天然就有性能的上限。

## 说几条MySQL对SQL的执行做的优化手段

1、对SQL语句的优化，MySQL会对我们的SQL语句做重写，包括条件化简，比如常量传递、除没用的条件等等；还会将一些外连接转换为内连接，然后选择成本最低的方式执行；对IN子查询会进行物化、物化表转连接查询、转换为半连接等方式进行。

2、在SQL语句的执行过程中，MySQL引入了索引条件下推。比如where后面的多个搜索条件都使用到了一个二级索引列，这些搜索条件中虽然出现了索引列，有些却不能使用到索引，像like ‘%...’查询，MySQL为了避免不必要的回表，从二级索引取得的索引记录，先做条件判断，如果条件不满足，则该二级索引记录不会去回表，这样可以大量的减少回表操作的随机IO成本。

3、在回表操作上，因为每次执行回表操作时都相当于要随机读取一个聚簇索引页面，而这些随机IO带来的性能开销比较大。MySQL中提出了一个名为Disk-Sweep Multi-Range Read (MRR，多范围读取)的优化措施，即先读取一部分二级索引记录，将它们的主键值排好序之后再统一执行回表操作。

4、MySQL在一般情况下执行一个查询时最多只会用到单个二级索引，但存在有特殊情况，也可能在一个查询中使用到多个二级索引，称之为：索引合并，比如Intersection交集合并、Union索引合并等等。

## InnoDB引擎的三大特性是什么？

InnoDB的三大特性是：Buffer Pool、自适应Hash索引、双写缓冲区。

自适应Hash索引，InnoDB存储引擎内部自己去监控索引表，如果监控到某个索引经常用，那么就认为是热数据，然后内部自己创建一个hash索引，称之为自适应哈希索引( Adaptive Hash Index,AHI)，创建以后，如果下次又查询到这个索引，那么直接通过hash算法推导出记录的地址，直接一次就能查到数据。

InnoDB存储引擎使用的哈希函数采用除法散列方式，其冲突机制采用链表方式。

Buffer Pool，为了提高访问速度，MySQL预先就分配/准备了许多这样的空间，为的就是与MySQL数据文件中的页做交换，来把数据文件中的页放到事先准备好的内存中。数据的访问是按照页（默认为16KB）的方式从数据文件中读取到 buffer pool中。Buffer Pool按照最少使用算法（LRU），来管理内存中的页。

Buffer Pool实例允许有多个，每个实例都有一个专门的mutex保护。Buffer Pool中缓存的数据页类型有: 索引页、数据页、undo页、插入缓冲（insert buffer)、自适应哈希索引、InnoDB存储的锁信息、数据字典信息（data dictionary)等等。

双写缓冲区，是一个位于系统表空间的存储区域，在写入时，InnoDB先把从缓冲池中的得到的page写入系统表空间的双写缓冲区。之后，再把page写到.ibd数据文件中相应的位置。如果在page写入数据文件的过程中发生意外崩溃，InnoDB在稍后的恢复过程中在doublewrite buffer中找到完好的page副本用于恢复。

doublewrite是顺序写，开销比较小。所以在正常的情况下, MySQL写数据page时，会写两遍到磁盘上，第一遍是写到doublewrite buffer，第二遍是从doublewrite buffer写到真正的数据文件中。

它的主要作用是为了避免partial
page write（部分页写入）的问题。因为InnoDB的page size一般是16KB，校验和写入到磁盘是以page为单位进行的。而操作系统写文件是以4KB作为单位的，每写一个page，操作系统需要写4个块，中间发生了系统断电或系统崩溃，只有一部分页面是写入成功的。这时page数据出现不一样的情形，从而形成一个"断裂"的page，使数据产生混乱。

## redolog和binlog的区别是什么？

答案见下一题

## MySQL崩溃后的恢复为什么不用binlog？

1、这两者使用方式不一样

binlog 会记录表所有更改操作，包括更新删除数据，更改表结构等等，主要用于人工恢复数据，而 redo log 对于我们是不可见的，它是 InnoDB 用于保证 crash-safe 能力的，也就是在事务提交后MySQL崩溃的话，可以保证事务的持久性，即事务提交后其更改是永久性的。

一句话概括：binlog 是用作人工恢复数据，redo log 是 MySQL 自己使用，用于保证在数据库崩溃时的事务持久性。

2、redo log 是 InnoDB 引擎特有的，binlog 是 MySQL 的 Server 层实现的,所有引擎都可以使用。

3、redo log是物理日志，记录的是“在某个数据页上做了什么修改”，恢复的速度更快；binlog是逻辑日志，记录的是这个语句的原始逻辑，比如“给ID=2这的c字段加1 ”，binlog有三种日志记录格式Row、SQL、混合模式。

4、redo log是“循环写”的日志文件，redo log 只会记录未刷盘的日志，已经刷入磁盘的数据都会从 redo log 这个有限大小的日志文件里删除。binlog 是追加日志，保存的是全量的日志。

5、最重要的是，当数据库 crash 后，想要恢复未刷盘但已经写入 redo log 和 binlog 的数据到内存时，binlog 是无法恢复的。虽然 binlog 拥有全量的日志，但没有一个标志让 innoDB 判断哪些数据已经入表(写入磁盘)，哪些数据还没有。

比如，binlog 记录了两条日志：

给 ID=2 这一行的 c 字段加1

给 ID=2 这一行的 c 字段加1

在记录1入表后，记录2未入表时，数据库
crash。重启后，只通过 binlog 数据库无法判断这两条记录哪条已经写入磁盘，哪条没有写入磁盘，不管是两条都恢复至内存，还是都不恢复，对 ID=2 这行数据来说，都不对。

但 redo log 不一样，只要刷入磁盘的数据，都会从 redo log 中抹掉，数据库重启后，直接把 redo log 中的数据都恢复至内存就可以了。

## MySQL如何实现事务的ACID？

参见下个问题。

## InnoDB事务是如何通过日志来实现的？

总的来说，事务的原子性是通过 undo
log 来实现的，事务的持久性性是通过 redo log 来实现的，事务的隔离性是通过读写锁+MVCC来实现的。

事务的一致性通过原子性、隔离性、持久性来保证。也就是说ACID四大特性之中，C(一致性)是目的，A(原子性)、I(隔离性)、D(持久性)是手段，是为了保证一致性，数据库提供的手段。数据库必须要实现AID三大特性，才有可能实现一致性。同时一致性也需要应用程序的支持，应用程序在事务里故意写出违反约束的代码，一致性还是无法保证的，例如，转账代码里从A账户扣钱而不给B账户加钱，那一致性还是无法保证。

至于InnoDB事务是如何通过日志来实现的，简单来说，因为事务在修改页时，要先记 undo，在记 undo 之前要记 undo 的 redo，
然后修改数据页，再记数据页修改的redo。 Redo（里面包括 undo 的修改）
一定要比数据页先持久化到磁盘。

当事务需要回滚时，因为有undo，可以把数据页回滚到前镜像的状态，崩溃恢复时，如果 redo log 中事务没有对应的 commit 记录，那么需要用 undo把该事务的修改回滚到事务开始之前。如果有 commit 记录，就用 redo 前滚到该事务完成时并提交掉。

更详细的回答是：

redo通常是物理日志，记录的是页的物理修改操作，用来恢复提交事务修改的页操作。而undo是逻辑日志，根据每行记录进行记录，用来回滚记录到某个特定的版本。

当事务提交之后会把所有修改信息都会存到redo日志中。redo日志由两部分组成，一个是在内存里的redo log buffer，另一个是在磁盘里的redo log文件。

mysql 为了提升性能不会把每次的修改都实时同步到磁盘，而是会先存到Buffer Pool(缓冲池)里头，把这个当作缓存来用。然后使用后台线程去做缓冲池和磁盘之间的同步。

系统重启后读取redo log恢复最新数据。虽然redo
log会在事务提交前做一次磁盘写入，但是这种IO操作相比于buffer pool这种以页（16kb）为管理单位的随机写入，它做的是几个字节的顺序写入，效率要高得多。

redo log buffer中的数据，会在一个合适的时间点刷入到磁盘中。

这个合适的时间点包括：

1、MySQL 正常关闭的时候；

2、MySQL 的后台线程每隔一段时间定时的讲 redo log buffer 刷入到磁盘，默认是每隔 1s 刷一次；

3、当 redo log
buffer 中的日志写入量超过 redo log buffer 内存的一半时，即超过 8MB 时，会触发 redo log buffer 的刷盘；

4、当事务提交时，根据配置的参数 innodb_flush_log_at_trx_commit 来决定是否刷盘。要严格保证数据不丢失，必须得保证 innodb_flush_log_at_trx_commit 配置为 1。

redo log 在进行数据重做时，只有读到了 commit 标识，才会认为这条 redo log 日志是完整的，才会进行数据重做，否则会认为这个 redo log 日志不完整，不会进行数据重做。

undo log和redo log记录物理日志不一样，它是逻辑日志。可以认为当delete一条记录时，undo log中会记录一条对应的insert记录，反之亦然，当update一条记录时，它记录一条对应相反的update记录。当执行回滚时，就可以从undo log中的逻辑记录读取到相应的内容并进行回滚。

而事务的隔离性，也可以通过undo log来实现的：当读取的某一行被其他事务锁定时，它可以从undo log中分析出该行记录以前的数据是什么，从而提供该行版本信息，帮助用户实现一致性非锁定读取，这也是MVCC的实现机制的组成部分。

## 什么是当前读和快照读？

当前读

像select lock in share  mode(共享锁), select for update ; update, insert ,delete(排他锁)这些操作都是一种当前读，就是它读取的是记录的最新版本，读取时还要保证其他并发事务不能修改当前记录，会对读取的记录进行加锁。是一种悲观锁的实现。

快照读

像不加锁的select操作就是快照读，即不加锁的非阻塞读；快照读的前提是隔离级别不是串行级别，串行级别下的快照读会退化成当前读；之所以出现快照读的情况，是基于提高并发性能的考虑，快照读的实现是基于多版本并发控制，即MVCC。

## 什么是MVCC？

MVCC
(Multi-Version Concurrency Control) ，叫做基于多版本的并发控制协议。他是和LBCC（Lock-Based Concurrency
Control）基于锁的并发控制概念是相对的。MVCC是乐观锁的一种实现方式，它在很多情况下，避免了加锁操作，降低了开销；既然是基于多版本，即快照读可能读到的并不一定是数据的最新版本，而有可能是之前的历史版本。

MVCC最大的好处：读不加锁，读写不冲突。在读多写少的OLTP应用中，读写不冲突是非常重要的，极大的增加了系统的并发性能，现阶段几乎所有的RDBMS包括MySQL，都支持了MVCC。

## MVCC的底层实现原理是什么？

MVCC实现原理主要是依赖记录中的隐式字段，undo日志
，Read View 来实现的。

MySQL中每行记录除了我们自定义的字段外，还有数据库隐式定义的DB_TRX_ID,DB_ROLL_PTR,DB_ROW_ID等字段。DB_TRX_ID是最近修改(修改/插入)事务ID，记录创建这条记录/最后一次修改该记录的事务ID。DB_ROLL_PTR，回滚指针，用于配合undo日志，指向这条记录的上一个版本。

不同事务或者相同事务的对同一记录的修改，会导致该记录的undo log成为一条记录版本线性表，也就是版本链。

事务进行快照读操作的时候产生一个Read
View，记录并维护系统当前活跃事务的ID，因为当每个事务开启时，都会被分配一个ID, 这个ID是递增的，所以最新的事务，ID值越大。

Read View主要是将要被修改的数据的最新记录中的DB_TRX_ID（即当前事务ID）取出来，与系统当前其他活跃事务的ID去对比（由Read View维护），如果DB_TRX_ID跟Read View的属性做了某些比较，不符合可见性，那就就通过DB_ROLL_PTR回滚指针去取出Undo Log中的DB_TRX_ID再比较，即遍历链表的DB_TRX_ID（从链首到链尾，即从最近的一次修改查起），直到找到满足特定条件的DB_TRX_ID, 那么这个DB_TRX_ID所在的旧记录就是当前事务能看见的最新老版本。

RC,RR级别下Read View生成时机的不同，造成RC,RR级别下快照读的结果的不同。RC隔离级别下，是每个快照读都会生成并获取最新的Read View，也就是说事务中，每次快照读都会新生成一个快照和Read View, 这就是我们在RC级别下的事务中可以看到别的事务提交的更新的原因；而在RR隔离级别下，则是同一个事务中的第一个快照读才会创建Read View, 之后的快照读获取的都是同一个Read View，快照读生成Read View时，Read View会记录此时所有其他活动事务的快照，这些事务的修改对于当前事务都是不可见的。而早于Read View创建的事务所做的修改均是可见。

## 什么是锁？MySQL 中提供了几类锁？

锁是实现数据库并发控制的重要手段，可以保证数据库在多人同时操作时能够正常运行。MySQL 提供了全局锁、行级锁、表级锁。其中 InnoDB 支持表级锁和行级锁，MyISAM 只支持表级锁。

## 什么是全局锁、共享锁、排它锁？

全局锁就是对整个数据库实例加锁，它的典型使用场景就是做全库逻辑备份。 这个命令可以使整个库处于只读状态。使用该命令之后，数据更新语句、数据定义语句、更新类事务的提交语句等操作都会被阻塞。

共享锁又称读锁 (read lock)，是读取操作创建的锁。其他用户可以并发读取数据，但任何事务都不能对数据进行修改（获取数据上的排他锁），直到已释放所有共享锁。当如果事务对读锁进行修改操作，很可能会造成死锁。

排他锁 exclusive lock（也叫 writer lock）又称写锁。

若某个事物对某一行加上了排他锁，只能这个事务对其进行读写，在此事务结束之前，其他事务不能对其进行加任何锁，其他进程可以读取,不能进行写操作，需等待其释放。排它锁是悲观锁的一种实现。

若事务 1 对数据对象 A 加上 X 锁，事务 1 可以读 A 也可以修改 A，其他事务不能再对 A 加任何锁，直到事物 1 释放 A 上的锁。这保证了其他事务在事物 1 释放 A 上的锁之前不能再读取和修改 A。排它锁会阻塞所有的排它锁和共享锁。

## MySQL中的表锁有哪些？

MySQL 里表级锁有两种：普通表级锁、元数据锁（meta data lock）简称 MDL和AUTO-INC锁。表锁的语法是 lock tables t read/write。

可以用 unlock tables 主动释放锁，也可以在客户端断开的时候自动释放。lock tables 语法除了会限制别的线程的读写外，也限定了本线程接下来的操作对象。

对于 InnoDB 这种支持行锁的引擎，一般不使用 lock tables 命令来控制并发，毕竟锁住整个表的影响面还是太大。

MDL：不需要显式使用，在访问一个表的时候会被自动加上。

MDL 的作用：保证读写的正确性。

在对一个表做增删改查操作的时候，加 MDL
读锁；当要对表做结构变更操作的时候，加 MDL 写锁。

读锁之间不互斥，读写锁之间，写锁之间是互斥的，用来保证变更表结构操作的安全性。

AUTO-INC锁，也就是在执行插入语句时就在表级别加一个AUTO-INC锁，然后为每条待插入记录的AUTO_INCREMENT修饰的列分配递增的值。

## InnoDB引擎的行锁是怎么实现的？

InnoDB是基于索引来完成行锁，在锁的算法实现上有三种：

· Record lock：单个行记录上的锁

· Gap lock：间隙锁，锁定一个范围，不包括记录本身

· Next-key lock：record+gap 锁定一个范围，包含记录本身

Gap锁设计的目的是为了阻止多个事务将记录插入到同一范围内，而这会导致幻读问题的产生，innodb对于行的查询使用next-key lock，Next-locking keying是Record lock和Gap lock的组合。当查询的索引含有唯一属性时，将next-key lock降级为record key。

有两种方式显式关闭gap锁 ，第一种. 将事务隔离级别设置为RC ；第二种. 将参数innodb_locks_unsafe_for_binlog设置为1。

## 谈一下MySQL中的死锁

死锁是指两个或两个以上的进程在执行过程中，因争夺资源而造成的一种互相等待的现象,若无外力作用,它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁。

如何查看死锁？

使用命令 show engine
innodb status 查看最近的一次死锁。

InnoDB Lock
Monitor 打开锁监控，每 15s 输出一次日志。使用完毕后建议关闭，否则会影响数据库性能。

对待死锁常见的两种策略：

通过 innodblockwait_timeout
来设置超时时间，一直等待直到超时；

发起死锁检测，发现死锁之后，主动回滚死锁中的某一个事务，让其它事务继续执行。

## 简述下MySQL8中的新增特性有哪些

MySQL8在功能上的我们需要关注增强主要有：1、账户与安全；2、索引3、InnoDB 增强。

主要表现在：

1、用户的创建与授权需要两条单独的SQL语句执行。认证插件更新。密码管理和角色管理发生变化。

2、隐藏索引，被隐藏的索引不会被优化器使用，但依然真实存在，主要用于软删除，可以根据需要后续真正删除或者重新可视化。

开始真正支持降序索引，以往的MySQL虽然支持降序索引，但是写盘的时候依然是升序保存。MySQL8.0中则是真正的按降序保存。

不再对group by操作进行隐式排序。

索引中可以使用函数表达式，创建表时创建一个函数索引，查询的时候使用同样的函数就可以利用索引了。

3、原子ddl操作，MySQL5.7执行drop命令 drop table
t1,t2; 如果t1存在，t2不存在，会提示t2表不存在，但是t1表仍然会被删除，MySQL8.0执行同样的drop命令，会提示t2表不存在，而且t1表不会被删除，保证了原子性。

自增列持久化，解决了之前的版本，主键重复的问题。MySQL5.7及其以前的版本，MySQL服务器重启，会重新扫描表的主键最大值，如果之前已经删除过id=100的数据，但是表中当前记录的最大值如果是99，那么经过扫描，下一条记录的id是100，而不是101。MySQL8.0则是每次在变化的时候，都会将自增计数器的最大值写入redo log，同时在每次检查点将其写入引擎私有的系统表。则不会出现自增主键重复的问题。

