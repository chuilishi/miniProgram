# MySQL/JDBC

**Tips**

分配用户权限:(先登陆root)

```
GRANT ALL ON *.* TO 'someuser'@'somehost';  //给'某用户'的'某ip分配权限
//这里ALL是所有权限,还有一些权限:https://dev.mysql.com/doc/refman/8.0/en/grant.html
```



关系型数据库: 以表的形式来存储数据



MySQL是这样的结构

![image-20230115133831013](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115133831013.png)

其中数据库就是一个个文件夹

​		数据表就是frm文件

​		数据就是MYD文件



以分号结尾,没见到分号就不停地让你输入

不区分大小写

两个横杠,接一个注释,横杠左边连着分号,右边要一个空格

分号,空格,井号,接一个注释

分号/*,执行完再输入xxx */ 也是注释 

### 客户端相关



命令行启动和停止服务:

```
net start 服务名 //chuiSQL 
net stop 服务名  
```

或者service.msc中找



打开客户端:

1. 直接打开shell

2. 命令行mysql [-h 127.0.0.1] [-P 3306] -u root -p

   两个大括号里的东西不是必填项,只是指定端口和地址

### 分类

![image-20230115135040951](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115135040951.png)

DDL: 操作数据库本身

DML: 增删改

DQL: 查

DCL: 用户相关





### DDL命令(创建)

SHOW DATABASES; //查询所有数据库

SELECT DATABASE(); //查询当前正在的数据库

CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE排序规则];       //创建  default charset和collate都是要打出来的

DROP DATABASE [IF EXISTS] 数据库名;    //删除

USE 数据库名;     // 使用

SHOW TABLES;  //查询当前数据库所有表

DESC 表名;         //查询表结构, 会在命令行画一个表出来  (describe的缩写)

SHOW CREATE TABLE;   //查询某表的建表语句,全部详细信息

**创建表:**

![image-20230115150700761](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115150700761.png)

**注意**:每一行之后都要加上逗号, 最后一行不用加, 最好一行行写,比较规整

一个例子:  id int comment '编号' ,

推荐charset: UTF8mb4 一个字符4个字节



修改相关命令:

ALTER TABLE 表名 RENAME TO 新表名;    // 修改表名

**ALTER TABLE  表名  ADD  列名  数据类型;    //添加一列**

ALTER TABLE 表名  MODIFY  列名  新数据类型;   //修改一列的数据类型

**ALTER TABLE 表名  CHANGE 列名 新列名 新数据类型;  //修改列名和数据类型**

**ALTER TABLE 表名  DROP  列名;     //删除列**



### DML命令(插入,修改) 

一行一行插入 ☆常用

INSERT  INTO  table_name  (列1, 列2,...)  VALUES  (值1, 值2,....)

// 列名可以省略

SELECT 查询

```
SELECT 列名,列名 from 表名,表名,...
FROM table_name
[WHERE Clause]   //where有点类似判断,后面跟的是多个判断语句,之间用and和or隔开
[LIMIT N][ OFFSET M]    //limit返回的记录数   offset偏移量
```

UPDATE  更新数据

```
UPDATE table_name SET field1=new_value1, field2=new_value2
[WHERE Clause] //先选择列,再用where id=2,选择一个方块
```

### 事务

将一段代码视为一个整体,有异常全部回归原来状态

BEGIN;    xxx      COMMIT    ROLLBACK;    

如果走到COMMIT就会真正更改数据.没有走到就会回滚

### 数据类型



| 类型         | 大小                                     | 有符号范围(signed)                                           | 无符号范围(unsigned)                                         |                 |
| ------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------- |
| TINYINT      | 1 Bytes                                  | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 Bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 Bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 Bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 Bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 Bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 Bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

日期和时间

| 类型      | 大小 ( bytes) | 范围                                                         | 格式                | 用途                     |
| :-------- | :------------ | :----------------------------------------------------------- | :------------------ | :----------------------- |
| DATE      | 3             | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3             | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1             | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8             | '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'               | YYYY-MM-DD hh:mm:ss | 混合日期和时间值         |
| TIMESTAMP | 4             | '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYY-MM-DD hh:mm:ss | 混合日期和时间值，时间戳 |

字符串类型

| 类型       | 大小                  | 用途                            |
| :--------- | :-------------------- | :------------------------------ |
| CHAR       | 0-255 bytes           | 定长字符串                      |
| VARCHAR    | 0-65535 bytes         | 变长字符串                      |
| TINYBLOB   | 0-255 bytes           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                    |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535 bytes        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                    |



# JDBC

Sun公司定义了一套操作数据库的接口

其他一些数据库公司为了适配Java,去写自己的实现类, 分别称为驱动

#### 基本流程

1. 导入对应数据库依赖jar包, 一般放到lib文件夹中

2. 注册驱动:

   ```
   Class.forName("com.mysql.jdbc.Driver");  //这个不用了,高版本自动执行

3. 连接:

   ```
   Connection conn= DriverManager.getConnection(url,username,password);

​		这里的url: " jdbc:mysql://127.0.0.1:3306/**db1**" db1是你数据库的名称

​		还要在末尾加?useUnicode=true&characterEncoding=utf8&useSSL=true&

serverTimezone=UTC  用来改变时区之类的,保证正常运行

4. 定义sql执行语句(String)

   ```
   String sql="select * from table";

5. 获取执行sql的对象,一个陈述(Statement)

   ```
   Statement stmt= conn.createStatement(); //conn是前面的连接对象

6. 执行:(execute)

   ```
   int count=stmt.executeUpdate(sql);  //返回值是受影响的行数

7. 释放资源:

   ```
   stmt.close() conn.close()

#### Connection

**事务管理**

![image-20230115191510054](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115191510054.png)

第一个设为true就开启事务

![image-20230115191806081](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115191806081.png)

一个经典的事务管理: 出现异常就回滚

连接SQL:

```
Connection conn= DriverManager.getConnection(url,username,password);
```

#### Statement

执行SQL语句

```
int executeUpdate(sql)  //返回修改行数  //执行DML,DDL语句(增删改语句)
返回值一般用来确认是否修改成功(>0)   如果是直接操作数据库,就不用这个

ResultSet executeQuery(sql) //返回结果集 //执行DQL语句 (查询语句)
resultSet中保存了查询结果

假设存储结果的是rs对象
两个方法:
rs.next()//指针移动到下一行,判断是否存在    rs.getXXX() //获取该行的XXX属性

有一个指针从第一行开始
while(rs.next()){   //每次循环都后移一个
	rs.getXXX(参数) //得到该行的某数据
}
```

防SQL注入:

![image-20230115210353352](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230115210353352.png)

#### 数据库连接池

一般情况下,一个get请求过来,就执行建立连接,完成查询和传输,关闭连接这几个步骤

但建立和关闭也是需要消耗性能.

数据库连接池帮你不需要频繁重新建立连接, 直接建几个长久的连接,每次都调用

当然,连接一直在内存里面跑.开太多连接也会导致内存不足

druid

先把jar包导入为库(add as library)

然后写一个druid.properties, 里面配置一些连接池属性

```
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql:///db_test?useSSL=false&useServerPrepStmts=true
//db_test是自己的数据库名
username=chui
password=zh356387
# 初始化连接数量
initialSize=5    //跟CPU的核数量有关系
# 最大连接数
maxActive=10
# 最大等待时间
maxWait=3000   //3秒
```

当然,与数据库连接的东西,最后都是要建立一个Connection

// 获取连接池对象

DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);

//  获取Connection

Connection connection = dataSource.getConnection( )

有Connection就可以开始描述sql了

### preparedStatement

PreparedStatement updateSales = con.prepareStatement("UPDATE COFFEES SET SALES = ? WHERE COF_NAME LIKE ? ");

// 用连接创建preparedStatement  就像statement一样
updateSales.setInt(1, 75);

updateSales.setString(2, "Colombian");

updateSales.executeUpdate( );

这里  ?  是占位符  由于在字符串当中不能直接写入动态内容

在之后的一堆set方法中设置具体的值



### 各个execute区别

**execute**执行增删改查操作

execute返回的结果是个boolean型，当返回的是true的时候，表明有ResultSet结果集，通常是执行了select操作，当返回的是false时，通常是执行了insert、update、delete等操作。execute通常用于执行不明确的sql语句。

**executeQuery**执行查询操作

executeQuery返回的是ResultSet结果集，通常是执行了select操作。

**executeUpdate**执行增删改操作