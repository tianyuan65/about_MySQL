## 第一章 MySQL简介
* 1.1 MySQL简介
    * MySQL是一种关系型数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。
* 1.2 MySQL安装与配置
* 1.3 sqlyog引入，非常方便，不用在命令提示符写一堆代码，可以直接在SQLyog创建并增删改查数据。

## 第二章 MySQL数据类型
* MySQL中定义数据字段的类型对数据库的优化是非常重要的。MySQL支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型。
* 2.1 数值类型(整数类型、浮点数类型、定点数类型)
    * MySQL支持所有标准SQL数值数据类型。这些类型包括严格数值数据(整数)类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据(浮点数)类型(FLOAT、REAL和DOUBLE PRECISION)。
    * 关键字INT是INTEGER的同义词，关键词DEC是DECIMAL的同义词
    * ![数值类型](images/数值类型.PNG)
* 2.2 日期类型、时间类型
    * 表示时间值的日期和事件的类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。每个时间类型有一个有效值范围和一个“零”值，当指定不合法的MySQL不能表示的值时使用“零”值。
        * ![时间/日期类型](images/时间、日期类型.PNG)
    * TIMESTAMP类型有专有的自动更新特性。
* 2.3 字符串(字符)类型
    * 字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET。
    * CHAR 和 VARCHAR 类型相似，但保存和检索的方式不同，他们的最大长度和是否为不空格被保留等方面也不同，在存储或检索过程中不进行大小写转换，也就是存储的是大写，检索出来的肯定也是大写。
    * BINARY 和 VARBINARY 类似于 CHAR 和 VARCHAR，不同的是它们包含二进制字符串而不要非二进制字符串。也就是说，它们包含字节字符串而不是字符字符串。这说明它们没有字符集，并且排序和比较基于列值字节的数值。
    * BLOB 是一个二进制大对象，可以容纳可变数量的数据。有 4 种 BLOB 类型：TINYBLOB、BLOB、MEDIUMBLOB 和 LONGBLOB。它们区别在于可容纳存储范围不同。
    * TEXT类型有四种，TINYTEXT、TEXT、MEDIUMTEXT 和 LONGTEXT。对应的这 4 种 BLOB 类型，可存储的最大长度不同，可根据实际情况选择。常用的有TEXT和MEDIUMTEXT，TINYTEXT太小，LONGTEXT初学者用不到。
        * ![字符类型](images/字符类型.PNG)

## 第三章 MySQL数据库和表的基本操作
* 3.1 数据库简介
    * 显而易见，就是存储数据的地方
* 3.2 数据库查看
    * 1. 首先，使用Win+R，cmd，```mysql -u root -p```，来连接数据库
    * 2. 其次，查看数据库的命令为 ```Show databases```
* 3.3 数据库创建
    * 创建数据库的命令 ```Create database db_test```。(格式要求：db->意为这是个数据库；test->数据库名)
* 3.4 数据库删除
    * 删除数据库命令 ```Drop database db_test```。

## 第四章 数据查询
* 4.1 单表查询
    * 1. 查询指定列，```SELECT t_student.name,t_student.age FROM t_student```
        * ![查询单个或指定列](images/查询单个或多个列.PNG)
    * 2. 查询全部列，```SELECT * FROM t_student```
    * 3. 查询经过计算的值(想查询18岁以上的人)，```SELECT t_student.name,t_student.gender,t_student.age-10 FROM t_student```
        * ![例：查询18岁以上的学生](images/查询经过计算的值.PNG)
    * 4. 消除取值重复的行，关键字为DISTINCT，```SELECT DISTINCT t_student.name FROM t_student```
        * ![例：消除重复的张三](images/消除取值重复的行.PNG)
    * 5. 查询满足条件的元祖(比较、确定范围、确定集合、字符匹配、空值、多重条件)
        * ![比较，关键字为WHERE，有大于、小于、等于、大于等于、小于等于，都可以写，但我不写](images/比较%20关键字为WHERE.PNG)
        * ![确定范围，找年龄为18到20的，关键字为第一个基础上BETWEEN ... AND ...](images/确定范围.PNG)
        * ![确定集合，找名字为李四，陈二，关键字为第一个基础上IN ('','')](images/确定集合.PNG)
        * ![字符匹配，找名字里有`老`的,关键字为第一个基础上LIKE ''](images/字符匹配`老`字开头.PNG)
        * 空值，找一个值为空值的和不是空值的，关键字为第一个基础上```IS (NOT) NULL```
            * ![IS NULL](images/查询的值为空值.PNG)
            * ![IS NOT NULL](images/查询的值不是空值.PNG)
        * ![多重条件，找20岁以上的男，关键字为第一个基础上AND...AND...](images/多重条件%2020岁以上的男.PNG)
    * 6. Order by 子句(用来排序)
        * ![升序，关键字为第一个基础上ORDER BY t_student.`age` ASC](images/年龄升序.PNG)
        * ![降序，关键字为第一个基础上ORDER BY t_student.`age` DESC](images/年龄降序.PNG)
    * 7. 聚集函数
        * ![统计了人数，关键字为COUNT(*)](images/统计了人数.PNG)
        * ![计算学生年龄之和，关键字为SUM(t_student.age)](images/统计年龄之和.PNG)
    * 8. Group by子句
        * ![统计出性别类别及其数量，关键字为COUNT(t_student.age) ... GROUP BY](images/统计性别分类和数量.PNG)
* 4.2 连接查询
    * 1. 等值与非等值连接查询
        * ![连接两个表](images/等值与非等值连接查询.PNG)
    * 2. 自身连接
        * ![score表和自身连接](images/score表自身连接.PNG)
    * 3. 外连接
        * 左外连接，列出左边关系的所有元祖，我没能列出来，命令为```SELECT t_student.`name`,t_student.`age`,t_student.`gender`,t_score.`score` FROM t_score LEFT OUTER JOIN  t_student stu ON (t_score.`stu_id`=t_student.`id`)```
        * 右外连接，列出右边关系的所有元祖，命令为```SELECT t_student.`name`,t_student.`age`,t_student.`gender`,t_score.`score` FROM t_score RIGHT OUTER JOIN  t_student stu ON (t_score.`stu_id`=t_student.`id`)```
    * 4. 复合条件连接，查找score>90的学生，命令为```SELECT t_student.`name`,t_student.`age`,t_student.`gender`,t_score.`score` FROM t_score,t_student WHERE t_score.`stu_id`=t_student.`id` AND t_score.`score`>90```
        * ![90分以上的学生](images/查找分数大于90.PNG)
* 4.3 嵌套查询
    * 1. 带有IN谓词的子查询
        * ![找出好学生，在这里是t_student表和t_good_stu表中name重合的学生](images/带有IN谓词的子查询.PNG)
    * 2. 带有比较运算符的子查询
        * ![找出t_student表和t_good_stu表中重合的李四](images/有比较运算符的子查询.PNG)
    * 3. 带有ANY(SOME)或者ALL谓词的子查询
        * ![ANY是小/大/等于子查询当中的某个值:首先查询t_score中score小于80的学生，再查询和展示刚才获取的score小于80的id、stu_id和score](images/带有ANY谓词的子查询.PNG)
        * ![ALL:是小/大/等于子查询当中的所有值](images/带有ALL谓词的子查询.PNG)
    * 4. 带有EXISTS谓词的子查询，EXIST:代表存在量词，不会返回任何数据，只产生逻辑结果，就是true/false。其对应的反义谓词为 NOT EXIST，就是使用EXIST后返回什么，NOT EXIST就反着来。
        * ![符合条件](images/存在符合条件的就列出来.PNG)
        * ![不符合条件](images/不存在符合条件的空集啥也不返回.PNG)
* 4.4 集合查询
    * 1. UNION并集，列出符合age大于20的不管gender是否为男，并列出符合gender为男不管age是否大于20。
        * ![条件为age大于20，gender为'男'](images/UNION并集.PNG)
    * 2. INTERSECTS交集，MySQL中无法使用，也看不到运行结果，用到时再说，其实就是列出同时符合条件的数据。
        * ```SELECT * FROM t_student WHERE t_student.`age`>20 INTERSECTS SELECT * FROM t_student WHERE t_student.`gender`="男"```
    * 3. EXCEPT差集，就是列出符合条件的数据以外的数据，
* 4.5 SELECT语句的一般格式
    * ```
        SELECT[ALL|DISTINCT]<目标列表达式> [AS列名] [,<目标列表达式> [AS列名]...] 
        FROM <表明或视图名> [别名][,<表名或视图名>[别名]]... 
        WHERE <条件表达式> [AND|OR<条件表达式>...]
        [GROUP BY 列名[HAVING <条件表达式>]]
        [ORDER BY 列名[ASC|DESC]]
      ```

## 第五章 数据更新
* 5.1 插入数据
* 5.2 修改数据
* 5.3 删除数据
