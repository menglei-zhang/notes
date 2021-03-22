## 数据库    

```
用于存储和管理数据的仓库

内存储存、文件储存、数据库储存
```

## SQL 

```
Structured Query Language  结构化查询语言
```

## MySQL的使用

```
一个数据库服务器中可以有多个数据库 ；一个数据库当中可以有多张表用来存储数据 ；一个表中可以用来存储多条记录
```

### 启动 和 停止

#### window

	1. 通过Windows服务管理器启动MySQL服务
	通过Windows的运行，输入services.msc找到MySQL服务
	2. 通过DOS命令启动MySQL服务
	net start mysql	开启MySQL服务      net stop mysql	停止MySQL服务     
	MySQL退出 exit 或 quit
#### Mac

    sudo /usr/local/mysql/support-files/mysql.server start;  // 启动MySQL服务
    sudo /usr/local/mysql/support-files/mysql.server stop; // 停止MySQL服务
    sudo /usr/local/mysql/support-files/mysql.server restart; // 重启MySQL服务
    MySQL退出 exit 或 quit
    
    /applications/mamp/library/bin/mysql -uroot -p
    第一步 ：终端界面下输入:sudo mysql.server start
    第二步 ：启动mysql服务,启动成功后继续输入:mysql -u root -p
    mysql -> show global variables like 'port';  // 查看mysql端口

### 登录数据库

	打开命令台：mysql -hlocalhost -P3306 -uroot -p   //连接远程数据库服务器
	-h：主机名   -P：端口   -u：用户名   -p：密码
	mysql默认连接localhost和3306，所以可以省略-h和-P
	mysql -u root -p        // 本机连接
## SQL语言分类

	DDL 数据定义语言（Data Definition Language）
	    数据库定义语言主要用于定义数据库、表等，其中包括：
	        CREATE  语句用于创建数据库、数据表等
	        ALTER   语句用于修改表的定义等
	        DROP    语句用于删除数据库、删除表等
	DML	数据操纵语言（Data Manipulation Language）
	    数据操作语言主要用于对数据进行添加、修改和删除操作，其中包括：
	        INSERT 语句用于插入数据
	        UPDATE 语句用于修改数据
	        DELETE 语句用于删除数据
	DQL	数据查询语言 （Data Query Language）
	    数据查询语言主要用于查询数据，也就是SELECT语句，使用SELECT 语句可以查询数据库中一条数据或多条数据
	        数据库中的操作都是通过SQL语句来完成的，而且在应用程序中也经常使用SQL语句，
	        例如在Node.js中嵌入SQL语句，通过执行JavaScript语言来调用SQL语句，就可以完成数据的插入、修改、删除、查询等操作。
	        SQL语句还可以嵌入到其它语言中，如Java、PHP等。
	DCL 数据控制语言（了解）（Data Control Language）  如：对用户权限进行操作
## 数据库表的基本操作

### 创建数据库   

```
create database (if not exists) database_name;
```

### 查看数据库   

```
show databases;
```

### 删除数据库   

```
drop database database_name;
```

### 选择数据库   

```
use database_name;
```

### 数据类型		

```
整数类型、日期和时间、字符串、二进制 

数据类型是用来约束表当中每一列存放的数据类型。
int        age  int，
double     score double（5,2）
char
varchar
date       yyyy-MM-dd
datetime   yyyy-MM-dd  HH-mm-ss
timestamp  时间戳类型 
```

### 创建数据库表

    CREATE TABLE `order` (
    `id` int(8) unsigned NOT NULL AUTO_INCREMENT COMMENT 'Id',
    `user_id` int(8) unsigned NOT NULL DEFAULT '0' COMMENT '会员id',
    `total_price` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '定单总价',
    `pay_status` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '支付状态 1、已经支付0 未支付',
    `name` varchar(30) NOT NULL DEFAULT '' COMMENT '收货人姓名',
    `address` varchar(150) NOT NULL DEFAULT '' COMMENT '收货人详细地址',
    `tel` varchar(30) NOT NULL DEFAULT '' COMMENT '收货人电话',
    `addtime` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '下单时间',
    PRIMARY KEY (`id`),
    KEY `addtime` (`addtime`)
    ) ENGINE=MyISAM DEFAULT CHARSET=utf8 COMMENT='定单';
    
    create table student( 
    id int unsigned not null auto_increment primary key comment 'id',
    name varchar(30) not null comment '姓名',
    gender char(1) not null default '' comment '1:男生 2:女生' 
    )engine=innodb charset=utf8 comment='学生表';
### 查看数据表

	show tables;
	desc table_name;
	show create table table_name;
	show create database database_name;  // 查询某个数据库的创建语句
### 删除数据表

```
drop table table_name;
```

### 表的约束

	为了防止数据表中插入错误的数据，在MySQL中，定义了一些维护数据库完整性的规则，即表的约束。
	约束是用来约束每一列的整个数据的，保证这个数据的完整性。
	| 约束条件      	| 说明                         
	| PRIMARY KEY  	 | 主键约束，用于唯一标识对应的记录
	| FOREIGN KEY  	 | 外键约束                     
	| NOT NULL       | 非空约束                     
	| UNIQUE         | 唯一性约束                   
	| DEFAULT        | 默认值约束，用于设置字段的默认值
	表的约束条件都是针对表中字段进行限制，从而保证数据表中数据的正确性和唯一性。
### 增加数据

	INSERT INTO table_name (id,userame...) VALUES (value1,value2,value3...);
### 修改数据 

```
update...set..where...

UPDATE table_name SET col_name1=expr1 , col_name2=expr2 where condition;

UPDATE employee SET username='caidaguanren' WHERE id=2;
```

### 删除数据 

```
delete from ... where ...

delete from table_name  [WHERE where_definition];
DELETE FROM employee WHERE id =1;
```

### 查询数据

	SELECT [DISTINCT] * (colum1, colum2, colum3...) FROM table_name [WHERE ... ];
	DISTINCT 可选，指查询结果时，是否去除重复数据
	SELECT COUNT(*) FROM employee; 统计某张表里面的数据的数量
	select *|字段列表 from 表名 [where] [group by] [having] [order by] [limit] 
#### 读取满足特定条件的数据

	=	>	<	>=	<=	<>/!=	IS NOT NULL		IS NULL		BETWEEN		IN		NOT IN		LIKE		NOT LIKE	REGEXP
	=
	>
	<
	>=
	<=
	<>/!=
	IS NOT NULL		地址不为空
	IS NULL		地址为空
	BETWEEN		
	IN		city in ('beijing','shanghai')
	NOT IN		
	LIKE 	name like ("%ang")   name like ("_zhang")  "%"通配任意个数的字符  "_"表示通配任意单个字符
	NOT LIKE
	REGEXP(RLIKE)		name exgexp		用在正则表达式匹配场景，MySQL使用了POSIX正则表达式，PHP曾经支持POSIX风格的正则表达式
#### 多表获取数据

    select * from table_name left join teble_name2 on table_name.id = table_name2.userid;
#### 联表查询

    #关联查询
    #crud
    select * from emp;
#### 笛卡尔积 

```
两个集合的相乘 4 * 9 = 36;

select * from emp,dept;
```

#### 交叉连接

    select * from emp cross join dept;
    # mysql方言
    select * from emp cross join dept on emp.dept_id = dept.id;
#### 内连接 显 隐

    #隐
    select * from emp,dept where emp.dept_id = dept.id;
    #显
    select * from emp inner join dept on emp.dept_id = dept.id;
#### 自连接

    select a.*,b.`name` from emp a,emp b where a.leader = b.id;
    
    select a.*,b.`name` from emp a inner join emp b on a.leader = b.id;
#### 外连接

    #左外连接：左表为主表，右表为从表
    #主表所有数据都显示，从表匹配数据才显示
    select a.*,b.`name` from emp a left join emp b on a.leader = b.id;
    #右外连接：右表为主表，左表为从表
    #主表所有数据都显示，从表匹配数据才显示
    select a.*,b.`name` from emp a RIGHT join emp b on a.leader = b.id;
    #不同的表外连接
    #右外连接：当sql比较复杂时，不易调换表的位置，视情况使用右外连接
    select * from emp left join dept on emp.dept_id = dept.id;
    select * from emp right join dept on emp.dept_id = dept.id;
    #只查询不匹配的数据
    select * from emp left join dept on emp.dept_id = dept.id
    where dept.id is null;
    
    select * from emp right join dept on emp.dept_id = dept.id 
    where emp.dept_id is null;
    # on 和 where 的区别：on 两张表如何关联，where 表关联之后的筛选
### MySQL 事务
	处理操作量大，复杂度高的数据。
	比如说，在人员管理系统中，要删除一个人员，既需要删除人员的基本资料，也要删除和该人员相关的信息，如信箱，文章等等，这样，这些数据库操作语句就构成一个事务！
	
	在MySQL中，只有使用了innodb数据库引擎的数据库或者表才支持事务
	事务可以用来维护数据库的完整性，保证呈批的SQL语句要么全执行，要么不执行
	事务用来管理 insert,update,delete语句
	
	一般来说事务必须满足：原子性（不可分割），一致性，隔离性（独立），持久性
	
	BEGIN	// 开启一个事务
	ROLLBACK	// 事务回滚
	COMMIT	// 事务确认
	SET AUTOCOMMIT = 0	 // 禁止自动提交
	SET AUTOCOMMIT = 1   // 开启自动提交
	
	<?php
		$dbhost = 'localhost';  // mysql服务器主机地址
		$dbuser = 'root';            // mysql用户名
		$dbpass = '123456';          // mysql用户名密码
		$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
		if(! $conn )
		{
			die('连接失败: ' . mysqli_error($conn));
		}
		// 设置编码，防止中文乱码
		mysqli_query($conn, "set names utf8");
		mysqli_select_db( $conn, 'RUNOOB' );
		mysqli_query($conn, "SET AUTOCOMMIT=0"); // 设置为不自动提交，因为MYSQL默认立即执行
		mysqli_begin_transaction($conn);            // 开始事务定义
		
		if(!mysqli_query($conn, "insert into runoob_transaction_test (id) values(8)"))
		{
			mysqli_query($conn, "ROLLBACK");     // 判断当执行失败时回滚
		}
		
		if(!mysqli_query($conn, "insert into runoob_transaction_test (id) values(9)"))
		{
			mysqli_query($conn, "ROLLBACK");      // 判断执行失败时回滚
		}
		mysqli_commit($conn);            //执行事务
		mysqli_close($conn);
	?>

### MySQL 索引
	索引优化应该是对查询性能优化最有效的手段了。
	mysql只能高效地使用索引的最左前缀列。
	mysql中索引是在存储引擎层而不是服务器层实现的
	索引可以大大提高MySQL的检索效率
	如果合理的设计且使用索引的MySQL是一辆兰博基尼的话，那么没有设计和使用索引的MySQL就是一个人力三轮车。
	索引分单列索引和组合索引。单列索引，即一个索引只包含单个列，一个表可以有多个单列索引，但这不是组合索引。组合索引，即一个索引包含多个列。
	索引是应用在 SQL 查询语句的条件(一般作为 WHERE 子句的条件)。
	过多的使用索引将会造成滥用。
	缺点：索引大大提高了查询速度，
	缺点：会降低更新表的速度，如对表进行INSERT、UPDATE和DELETE。因为更新表时，MySQL不仅要保存数据，还要保存一下索引文件。建立索引会占用磁盘空间的索引文件。

### 正则表达式
	MySQL中使用 REGEXP 操作符来进行正则表达式匹配
	MySQL的正则表达式匹配与PHP 和 Perl 脚本类似
	
	1、它提供了强大而灵活的匹配模式，可以帮助我们为数据库系统实现强大的搜索实用程序。
	2、regexp是执行正则表达式模式匹配时使用的运算符，rlike是同义词。
	3、它还支持许多元字符，这些元字符在执行模式匹配时可以提供更大的灵活性和控制。
	4、反斜杠用作转义字符。如果使用了双反斜杠，则仅在模式匹配中考虑。
	5、不区分大小写。
	
	下表中的正则模式可应用于 REGEXP 操作符中。
	模式	描述
	^			匹配输入字符串的 开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。
	$			匹配输入字符串的 结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。
	.			匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用象 '[.\n]' 的模式。
	[...]		字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。
	[^...]		负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'。
	p1|p2|p3	匹配 p1 或 p2 或 p3。例如，'z|food' 能匹配 "z" 或 "food"。'(z|f)ood' 则匹配 "zood" 或 "food"。
	*			匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。
	+			匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
	{n}	n 		是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
	{n,m}		m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。
	
	了解以上的正则需求后，我们就可以根据自己的需求来编写带有正则表达式的SQL语句。以下我们将列出几个小实例(表名：person_tbl )来加深我们的理解：
	
	查找name字段中以'st'为开头的所有数据： SELECT name FROM person_tbl WHERE name REGEXP '^st';
	查找name字段中以'ok'为结尾的所有数据： SELECT name FROM person_tbl WHERE name REGEXP 'ok$';
	查找name字段中包含'mar'字符串的所有数据： SELECT name FROM person_tbl WHERE name REGEXP 'mar';
	查找name字段中以元音字符开头或以'ok'字符串结尾的所有数据： SELECT name FROM person_tbl WHERE name REGEXP '^[aeiou]|ok$';

##  数据库总结
	增
		database				
								create database database_name;
	
		table					
								create table user(
									id int not null auto_increment comment "ID",
									username varchar(50) not null default "" comment "用户名",
									password varchar(50) not null default "" comment "密码",
									address varchar(100) not null default "" comment "住址",
									tel varchar(30) not null default "" comment "联系电话",
									account float(8,2) not null default "0.00" comment "账户金额",
									addtime int not null default "0" comment "创建时间",
									primary key (id)
								);
								
								insert into user (username,password,address,tel,account,addtime) 
								values 
								('zhang','admin','河南省','110',199999.80,now());
	
								create table new_table_name like old_table_name;    // 复制表
	
		clolumn					
								alter table TABLE_NAME add column NEW_COLUMN_NAME varchar(20) not null;
	
		data         	        
								insert into table_name (username,password) values ("zml","zml123456");
	
	删
		database                
								drop database database_name;
	
		table                   
								drop table table_name;
								truncate table 表名;          // 先删除表，然后在创建一种一样的表格
								alert table table_name drop colum;           // 删除列
	
		data                   
	  						delete from table_name (where condition);
	    
	改
		database                
								alert database database_name character set character_name;
	    
		table                   
								rename table old_table_name to new_table_name;
								alert table table_name character set character_name;
								alert table table_name add colum new_column character_name;
								alert table table_name change colum new_colum character_name;     // 修改列名及字符集
								alert table table_name modify colum charcter_name;       // 修改字符集
								select username as my_username from user;     // 别名
	
		data                    update user set username="zxr" where id=2;
	
	查
	
		database                
								show databases;      
								show create database database_name;
								select database();   查看当前正在使用的数据库
	
		table                   
								show tables;
								desc table_name;   
								show create table table_name;
	                            
		data                   
	  						select * from table_name;  
