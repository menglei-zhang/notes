问题分析
浏览器 => web服务器 => 后端脚本(php) => 数据库(mysql)
1、提供并发量  负载均衡（分布式服务器架构）  并发量更高的软件（nginx）
2、页面静态化
3、内存缓存优化
4、数据优化  读写频繁的数据可以写到缓存内存中，但是内存容量有限，仅此要进行数据库优化

### 优化方向（数据访问变慢，优化mysql）
## 储存层   存储引擎 列类型选择(column)  范式（三范式）
## 设计层   索引    缓存    分区分表
## SQL层(执行层)  使用效率更高的SQL语句
## 架构层   分布式数据库架构(mysql主从复制，实现读写分离)
 
数据库一般做读写操作，在大部分业务环境下，优化mysql的读操作。

### 存储引擎
show engines;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
常用的存储索引有两个
MyISAM -->  Collection of identical MyISAM tables 
InnoDB -->  Supports transactions, row-level locking, and foreign keys

### MyISAM
create table student(
    id int unsigned not null auto_increment comment "id",
    name varchar(30) not null comment "姓名",
    height decimal(10,2) not null default 0 comment "身高",
    age int not null default 1 comment "年龄",
    introduce text comment "介绍",
    primary key (id)
)engine=Myisam charset=utf8;
bd54e12d3cb24210fdfb532248623c96 into student values (22,'zhang','180',18,'自我介绍');
insert into student values (21,'wang','188',23,'自我介绍');
insert into student values (25,'li','178',22,'自我介绍');
insert into student values (10,'zhao','167',21,'自我介绍');
insert into student values (16,'zhu','200',19,'自我介绍');

create table tptest_users(
    id int unsigned not null auto_increment primary key,
    username varchar(40) not null default '' comment '用户名',
    password varchar(40) not null default '' comment '密码'
)engine = Innodb charset = utf8;

insert into student select null,name,height,age,introduce from student;   蠕虫复制

flush tables; 数据(从内存)写到磁盘中

.frm -->> 结构文件  .MYD -->> 数据文件   .MYI -->> 索引文件
数据文件和索引文件可以放置在不同的目录，平均分布io，获得更快的速度。
存储数据是插入数据，没有进行排序操作
数据表生成文件有三个，如果进行数据备份和恢复，直接复制粘贴三个文件恢复即可。
压缩机制：数据表进行压缩，节省储存空间。
压缩操作：
压缩表文件，并重建索引
压缩表只能读
解压缩会自动重建索引

myisam 如果进行并发写入时，为了保证数据的一致性，加锁，只能使用表锁，表锁会影响到整个数据表的操作。并发性稍微逊色

### InnoDB
create table student1(
    id int unsigned not null auto_increment comment "id",
    name varchar(30) not null comment "姓名",
    height decimal(10,2) not null default 0 comment "身高",
    age int not null default 1 comment "年龄",
    introduce text comment "介绍",
    primary key (id)
)engine=InnoDB charset=utf8;
insert into student1 values (22,'zhang','180',18,'自我介绍');
insert into student1 values (21,'wang','188',23,'自我介绍');
insert into student1 values (25,'li','178',22,'自我介绍');
insert into student1 values (10,'zhao','167',21,'自我介绍');
insert into student1 values (16,'zhu','200',19,'自我介绍');

ibdata1 数据库所有的innodb表数据和索引文件
默认是合一块的，查找和查询速度更快，文件损坏或者误删，会导致其他表格不能用
可以选择把innodb的数据和索引文件，根据表名进行分离，在创建表的时候，就进行分离。
临时设置分离
查看：mysql > show variables like "innodb_file_per%";
开启：mysql > set global innodb_file_per_table = 1;

.frm -->> 结构文件  .idb -->> 数据和索引文件

根据主键自动进行排序操作

innodb 表不能直接复制粘贴，备份恢复，需要导出SQL文件，在导入恢复

事务：保证数据的一致性、原子性
如果有多个业务操作，需要把所有操作都执行成功才可以，如果有不成功，则所有操作都不成功。
中间件可以代替事务

外键：是一种约束，
主表 主键id
副表 id
主表id 和 副表id 进行关联，设定一个取值范围

并发性：擅长并发
innodb在进行并发操作是，为了数据的一致性，可以使用行锁机制（锁表粒度），影响数据只为当前行，并发性较好一些。

### 如何选择 myisam 和 innodb 
## 根据存储的功能和特点进行选择
1、一般 使用 读写较多 备份恢复方便 压缩机制 用 myisam （默认有一个计数器）
cms(内容管理系统，快速搭建网站)
2、并发写入多(行锁) 事务(可以通过前端控制) 外键 innodb
订单系统(并发较多)

## 其他存储引擎
1、Memory 数据置于内存的存储引擎，拥有极高的插入、更新和查询效率，但是会占用和数据量成正比的内存空间。
内容会在mysql重新启动是丢失。
introduce text comment "介绍"   不支持text类型
create table student2(
    id int unsigned not null auto_increment comment "id",
    name varchar(30) not null comment "姓名",
    height decimal(10,2) not null default 0 comment "身高",
    age int not null default 1 comment "年龄",
    primary key (id)
)engine=Memory charset=utf8;
2、Archive 归档存储引擎，只支持数据的查询和写入，经常用于存储日志等相关信息。

### 字段选取  
## 数字占用空间小，查询速度快
## 选取占据空间小的字段    占用小，数据查询遍历就会快
## 内容长度固定字段
char 定长   255字符
varchar 变长    65535字节   如果使用utf-8的编码，3个字节一个字符，可以储存最大的字符数 65535/3-1 个字符，使用1个字符保存长度
电话号码   固定11位  char
邮箱地址   varchar
如果数据不定长，使用varchar会节省空间
如果追求查询效率，就需要使用char
## 整形存储  尽量使用能够整形储存数据
1、时间戳使用
使用int类型存储，节省空间，时间范围更好计算确定
mysql 中时间戳相关函数
unix_timestamp()   当前时间戳
from_unixtime()    读取一个时间戳信息
PHP中时间戳相关函数
php 要设置时间区  date_default_timezone_set("Asia/Shanghai");
time()   获取当前时间戳
date("Y-m-d H:i:s",$time);   时间戳函数转成时间格式
strtotime(时间格式)         时间格式转为时间戳

2、IP储存使用  IP转为int储存
mysql ->  inet_aton   /     inet_ntoa
select inet_aton('192.168.50.6');
+---------------------------+
| inet_aton('192.168.50.6') |
+---------------------------+
|                3232248326 |
+---------------------------+

select inet_ntoa(3232248326);
+-----------------------+
| inet_ntoa(3232248326) |
+-----------------------+
| 192.168.50.6          |
+-----------------------+

php ->   ip2long   /    long2ip

<?php
    $ip = "192.168.50.6";
    echo $ipInt = ip2long($ip);   // 3232248326
    echo "<hr />";
    echo long2ip($ipInt);  // 192.168.50.6
?>

### 范式  范式是一种规范或者约束，如果设计的数据库表是符合范式的，被认为是良好的数据设计
## 三范式  1NF < 2NF < 3NF
# 第一范式：数据字段具有原子性，业务上不可以在分割。
# 第二范式：数据具有唯一性(主键id)。
# 第三范式：数据字段和主键具有紧密联系，不允许出现冗余(重复)字段

## 逆（反）范式  在真实的业务环境中，为了更好的数据库的性能，会选择不遵守规范操作。遵守第三范式，查询数据，需要连表操作，如果数据表数据很多，连表操作会消耗大量时间，为了查询效率，可以选择吧数据字段存储到同一个表中。


### 索引  书的目录  指引   一种数据结构(存储数据的方式)，存储字段值的内容和对应真实数据的物理地址。查询数据通过索引定位到物理地址，在通过物理地址查询数据 
MyISAM -> .MYI -->> 索引文件  InnoDb -> .idb -->> 数据和索引文件
索引是一种以空间取时间的方式，牺牲了写的速度，提高了查询的速度
## 是否使用索引的差别
1、复制恢复表
2、建立主键索引  alter table table_name add primary key (要创建索引的列名);
## 索引为什么速度快
之前查询数据需要遍历整个数据表，建立索引之后，查询变为：查询字段 => 物理地址 => 真实数据
## 创建索引
索引的类型：
mysql 中使用关键字 key index 标识索引
# 主键索引  主键约束  唯一性  不能为null   primary key
# 唯一索引  唯一约束  唯一性  可以为null   unique key
# 普通索引    key
# 全文索引  只支持文本类型。文本中的类型(char、varchar、text)，文本中的内容进行分词，分别建立索引  mysql 5.6以下，InnoDB 不支持索引
特殊索引类型
# 复合（联合）索引 多个字段共同组成一个索引
# 前缀索引

创建索引的方式：
# 建立表结构设计索引
create table 表名(
    字段 ......
    primary key (id),
    unique index 名字(字段),
        index 名字(字段),
        index 名字(字段，字段),  -- 复合索引
    fulltext index 名字(字段);
)
# 使用修改结构语法的语句（alter table）
alter table table_name add
    primary key (id),
    unique index 名字(字段),
    key 名字(字段),
    key 名字(字段，字段),  -- 复合索引
    fulltext key 名字(字段);
如果不指定索引名称，会默认选择字段名称是复合索引的话，选择第一个字段作为索引名称。

CREATE TABLE `student` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT 'id',
  `name` varchar(30) NOT NULL COMMENT '姓名',
  `height` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '身高',
  `age` int(11) NOT NULL DEFAULT '1' COMMENT '年龄',
  `introduce` text COMMENT '介绍',
  PRIMARY KEY (`id`)
) ENGINE=MyISAM AUTO_INCREMENT=5242901 DEFAULT CHARSET=utf8;

alter table student add unique key(name);
alter table student add key(age);
alter table student add key(name,age);
alter table student add fulltext key(introduce);

CREATE TABLE `student` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT 'id',
  `name` varchar(30) NOT NULL COMMENT '姓名',
  `height` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '身高',
  `age` int(11) NOT NULL DEFAULT '1' COMMENT '年龄',
  `introduce` text COMMENT '介绍',
  PRIMARY KEY (`id`),
  UNIQUE KEY `name` (`name`),
  KEY `age` (`age`),
  KEY `name_2` (`name`,`age`),
  FULLTEXT KEY `introduce` (`introduce`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8;

## 删除索引
1、删除主键带自增属性的
需要先删除自增属性  
alter table table_name modify id int unsigned not null comment 'id属性';
alter table table_name drop primary key;
2、删除非主键索引
alter table table_name drop key key 名称;
alter table student drop key name_2;

### 执行计划 explain  不会真实执行，分析SQL语句执行的过程和使用的资源
explain sql   /    desc sql
建立索引是为了提高查询效率，检查索引是否使用到。
explain select * from student1 where id = 16\G;
+----+-------------+----------+-------+---------------+---------+---------+-------+------+-------+
| id | select_type | table    | type  | possible_keys | key     | key_len | ref   | rows | Extra |
+----+-------------+----------+-------+---------------+---------+---------+-------+------+-------+
|  1 | SIMPLE      | student1 | const | PRIMARY       | PRIMARY | 4       | const |    1 | NULL  |
+----+-------------+----------+-------+---------------+---------+---------+-------+------+-------+

### 索引的使用场合
在某些查询情况，建立索引能够提高茶饮效率，这些情况适合建立索引
1、where 条件字段
explain select * from student1 where id = 16\G;
2、order by 排序字段(配合limit语法可以使用到索引)
explain select * from student1 order by id limit 2\G;
3、索引覆盖 需要获取的字段值，正好是索引的内容
explain select id from student1\G;
4、联表字段 给连表的字段建立索引，可以使用发哦索引，提升查询速度
on 语法之后的关键字段

### 索引原则
建立的索引字段，可以没有使用到索引，原因是没有遵循索引的使用原则
1、列独立  列不能做运算  
explain select * from table_name where id+1 = 18\G;
2、左固定 (模糊查询 like)  like "00%";
alter table student1 add key(name);
explain select * from student1 where name like 'zh%';
3、复合索引
需要同时出现在条件中，才可以使用到复合索引，单独使用不到。
alter table student1 add key(height,age);
4、or条件 如果都有索引可用，则索引都可用，如果有一个字段索引不可用，则都不可用

### 前缀索引  可以通过数据的前一部分区分出数据的唯一性，把这一部分增加做阴。比把字段所有的内容增加索引更加节省空间，速度更快
比普通索引的好处 更加节省空间，速度更快；
去除掉重复的，通过前几位确定唯一性 distinct()
select count(*) from table_name;
select count(distinct(colunm)) from table_name;

select substr('zhang',2,3);
+---------------------+
| substr('zhang',2,3) |
+---------------------+
| han                 |
+---------------------+

1、确定建立索引前缀长度；
2、建立前缀索引
alter table table_name add key 索引名称 (addr(11))
alter table table_name drop key 索引名称;

### in 条件索引使用  可以同时查询出多条不连续的数据   in条件可以使用索引
某个字段经常是用in条件查询，可以选择给次字段增加索引，in条件可以使用索引
explain select * from table_name where id in (10000,100008)；

### 全文索引
文本类型  char varchar text
通过分词，给分词建立索引 ； 解决 like 查询，使用不到索引的问题
弥补 左固定 (模糊查询 like)  like "00%";   左边不固定like查询不能使用索引

alter table table_name add fulltext key (column);
explain select * from table_name where match (column) against('To')\G;

使用like不能使用到全文索引，使用match against 可以使用到全文索引

### 复合全文索引  字段全部出现才可以使用到复合索引

alter table table_name add fulltext key (column1,column2);

explain select * from table_name where match (column1,column2) against('To,you')\G;

alter table table_name drop key column;

match against 是查询全文索引的语法

全文索引里没有给查询的关键词建立索引，mysql本身不会把经常使用的一些词汇建立索引；

在实际开发环境中，经常使用管道的单词，反而没有建立索引，不适用于我们是使用需求，会选择一些第三方软件配合mysql是实现全文索引技术和搜索引擎技术

PHP  使用  sphinx  分词技术，全文索引技术  搜索技术

xunsearch

Java 使用  lucene  

全文索引只支持文本类型（text char  varchar)
mysql 5.6 以下，  仅myisam 支持
分词不适合实际使用（不支持中文）
选择sphinx等第三方软件来代替mysql的全文索引

### 分页优化  分页原理：集合SQL语法 limit(skip,length)
在大数据量大的表，进行汾阳王limit语法操作，出现分页skip太大，使用不到索引，
explain select * from table_name order by id desc limit skip,length;
优化方案：
1、进行数据的卡位操作；
explain select * from table_name where id > 199999 order by id limit 5\G;
先通过where确定一个位置，然后再查询数据
在进行where天剑限制范围的时候，注意参数的起始位置
 
### 索引结构的类型
1、聚集型索引
数据文件和索引文件是在一起的
InnoDB   .idb
2、非聚集型索引 非聚簇型索引
数据文件和索引文件是分离的
myisam     .MYD(数据文件)    .MYI(索引文件)

myisam   .MYD   .MYI
主键索引：primary key  查询关键字 => 主键索引 => 物理地址 => 真实数据
非主键索引：查询关键字 => 非主键索引 => 物理地址 => 真实数据

InnoDB    .idb
主键索引：关键字 => 主键索引 => 真实数据
非主键索引：关键字 => 非主键索引 => 主键索引 => 真实数据
如果InnoDB没有主键索引，非主键索引如何使用？记录一个数据的唯一值。如果没有主键，会生成一个rowid（唯一）。非主键索引就记录这个rowid。

### 缓存设置  有实效性  mysql提供了缓存机制，可以通过对应的SQL语句，把数据结果缓存起来，之后直接返回缓存数据的结果即可。提高了查询效率。
1、查看并开启缓存机制
mysql -> show variables like 'query_cache%';
mysql -> set global query_cach_size = 64*1024*1024;

mysql> show variables like "query_cache%";

+------------------------------+---------+
| Variable_name                | Value   |
+------------------------------+---------+
| query_cache_limit            | 1048576 |
| query_cache_min_res_unit     | 4096    |
| query_cache_size             | 1048576 |
| query_cache_type             | OFF     |
| query_cache_wlock_invalidate | OFF     |
+------------------------------+---------+

通过mysql缓存  没存缓存

### 缓存实效  当数据表结构发生改变的时候缓存会失效
数据库的操作
写：insert update delete  会是数据表结构发生改变
读：select
### 使用不到缓存
随机值或者时间值出现在SQL语句中，使用不到缓存
now() rand()

### 生成多个缓存    由于SQL语句大小写、空格等等，会被认为是多条不同的SQL语句，就会生成多个缓存，浪费缓存空间
书写SQL语句一定要按照约定好的格式和规范书写

### 不使用缓存  sql_no_cache
select sql_no_cache * from table_name where ...;

### 缓存的其他操作
1、查看缓存的使用状态
show status like 'Qcache%';
2、清空缓存
reset query cache;

mysql> show status like 'Qcache%';
+-------------------------+----------+
| Variable_name           | Value    |
+-------------------------+----------+
| Qcache_free_blocks      | 1        |
| Qcache_free_memory      | 62896784 |   // 剩余空间
| Qcache_hits             | 0        |   // 缓存命中次数
| Qcache_inserts          | 0        |
| Qcache_lowmem_prunes    | 0        |
| Qcache_not_cached       | 31141    |   // 没有使用缓存的次数
| Qcache_queries_in_cache | 0        |
| Qcache_total_blocks     | 1        |
+-------------------------+----------+

### 分表设计  在一般业务环境中，使用 索引 、 缓存 、 内存缓存 优化，能够满足大部分业务使用需要的速度。
随着业务发展，数据表中的数据量增加太快，百万级以上，千万级别 亿级别时，单个数据表已经不能支撑业务需求了额，数据表表活性大大降低，可以选择分区表的方式，吧数据分配到多个数据表中，以提高数据的读写速度。

### 分区、表类型区别  
分区、分表的类型：
1、逻辑分区、分表   真实还是一个表，逻辑分为多个，使用的SQL语句和单表相同；
key  hash  (取余方式)
range  list  (条件方式)
2、物理分表  吧数据分配到几个真实数据表中，SQL欲哭需要确定操作哪个表；

### 四种格式的逻辑分表
逻辑分区类型：
1、取余方式  key/hash  会根据数据表的算法分配多个分表中
2、条件方式  range/list  数据满足某一个分表的条件，就会分配到分表
分表条件必须是主键或者主键的一部分（联合主键）

### key 分表    partition by key (id) partitions 5

CREATE TABLE `goods_key` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT 'id',
  `name` varchar(30) NOT NULL COMMENT '名称',
  `price` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '价格',
  `pubdate` datetime NOT NULL DEFAULT '0000-00-00 00:00:00' COMMENT '出厂时间',
  PRIMARY KEY (`id`)
) ENGINE=MyISAM AUTO_INCREMENT=15 DEFAULT CHARSET=utf8
partition by key (id) partitions 5;

insert into goods_key values (12,'htc','3451.1','2016-02-14 12:30:12');
insert into goods_key values (13,'apple','3451.3','2016-02-14 12:30:12');
insert into goods_key values (14,'nokia','3451.6','2016-02-14 12:30:12');

### hash 分表   partition by hash (month(pubdate)) partitions 12;
create table goods_hash(
    id int unsigned not null auto_increment comment "id",
    name varchar(30) not null comment "名称",
    price decimal(10,2) not null default 0 comment "价格",
    pubdate datetime not null default '0000-00-00 00:00:00' comment "出厂时间",
    primary key (id,pubdate)
)engine=InnoDb charset=utf8
partition by hash (month(pubdate)) partitions 12;

insert into goods_hash values (12,'htc','3451.1','2016-02-14 12:30:12');
insert into goods_hash values (13,'apple','3451.3','2016-03-14 12:30:12');
insert into goods_hash values (14,'nokia','3451.6','2016-04-14 12:30:12');
insert into goods_hash values (15,'nokia','3451.6','2016-05-14 12:30:12');
insert into goods_hash values (16,'nokia','3451.6','2016-06-14 12:30:12');

mysql> select day(now());
+------------+
| day(now()) |
+------------+
|          3 |
+------------+
mysql> select month(now());
+--------------+
| month(now()) |
+--------------+
|            7 |
+--------------+
mysql> select year(now());
+-------------+
| year(now()) |
+-------------+
|        2020 |
+-------------+
### range 分表  values less than (1980)
create table goods_range(
    id int unsigned not null auto_increment comment "id",
    name varchar(30) not null comment "名称",
    price decimal(10,2) not null default 0 comment "价格",
    pubdate datetime not null default '0000-00-00 00:00:00' comment "出厂时间",
    primary key (id,pubdate)
)engine=Myisam charset=utf8
partition by range (year(pubdate)) (
    partition hou70 values less than (1980),
    partition hou80 values less than (1990),
    partition hou90 values less than (2000)
);

insert into goods_range values (12,'htc','3451.1','1975-02-14 12:30:12');
insert into goods_range values (13,'apple','3451.3','1977-03-14 12:30:12');
insert into goods_range values (14,'nokia','3451.6','1979-04-14 12:30:12');
insert into goods_range values (15,'nokia','3451.6','1983-05-14 12:30:12');
insert into goods_range values (16,'nokia','3451.6','1996-06-14 12:30:12');

insert into goods_range values (16,'nokia','3451.6','2012-06-14 12:30:12');

### list 分表   values in (3,4,5)
create table goods_list(
    id int unsigned not null auto_increment comment "id",
    name varchar(30) not null comment "名称",
    price decimal(10,2) not null default 0 comment "价格",
    pubdate datetime not null default '0000-00-00 00:00:00' comment "出厂时间",
    primary key (id,pubdate)
)engine=InnoDb charset=utf8
partition by list (month(pubdate))(
    partition spring values in (3,4,5),
    partition summer values in (6,7,8),
    partition autumn values in (9,10,11),
    partition winder values in (12,1,2)
);

insert into goods_list values (14,'nokia','3451.6','1979-04-14 12:30:12');
insert into goods_list values (15,'nokia','3451.6','1983-07-14 12:30:12');
insert into goods_list values (16,'nokia','3451.6','1996-10-14 12:30:12');

### 分表管理  数据表已经建立好，或者分区数据后期需要增加或者删除表，可以对相应的数据表进行管理操作
## key / hash (求余方式) 分表管理  数据会根据算法自行分配，不会丢失数据  数据存储方式和业务（条件）联系不紧密
增加： alter table table_name add partition partitions 5;
减少： alter table table_name coalesce partition 12;

mysql> alter table goods_key add partition partitions 5;
mysql> alter table goods_key coalesce partition 9;

## range / list (条件方式) 分表管理  删除数据会丢失
增加：
alter table goods_range add partition(
    partition hou00 values less than (2010),
    partition hou10 values less than (2020)
);
减少：
alter table table_name drop partition 分区名称;

### 物理分表
## 水平分表
## 垂直分表


### 慢查询日志设置
慢查询：如果执行SQL语句，返回数据时间，大雨设置的设置（规定的时间），这个SQL语句就被认为是一个慢查询。
## 慢查询日志的开启、日志位置：
## mysql> show variables like 'slow_query%';
+---------------------+------------------------------------------------------------------+
| Variable_name       | Value                                                            |
+---------------------+------------------------------------------------------------------+
| slow_query_log      | OFF                                                              |
| slow_query_log_file | /Applications/MAMP/db/mysql56/zhangmengleideMacBook-Pro-slow.log |
+---------------------+------------------------------------------------------------------+

## 开启：set global slow_query_log = 1;
## 关闭：set global slow_query_log = 0;

## mysql> show variables like 'slow_query%';
+---------------------+------------------------------------------------------------------+
| Variable_name       | Value                                                            |
+---------------------+------------------------------------------------------------------+
| slow_query_log      | ON                                                               |
| slow_query_log_file | /Applications/MAMP/db/mysql56/zhangmengleideMacBook-Pro-slow.log |
+---------------------+------------------------------------------------------------------+

快慢时间临界点
## show variables like "long_query_time";

## mysql> show variables like 'long_query_time';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+

## set long_query_time = 1;


### 其他操作
## 1、修复表  在长期的数据更改过程中，索引文件和数据文件都将产生空洞。形成碎片，我们可以通过一个操作(不产生对数据是指影响的操作)来修改表，修改表语法操作。

delete from student where name = 'zhang';
删除数据后数据表大小不变，通过修复表语句进行碎片修复
# optimize table table_name;
mysql> optimize table student;
+--------------+----------+----------+----------+
| Table        | Op       | Msg_type | Msg_text |
+--------------+----------+----------+----------+
| test.student | optimize | status   | OK       |
+--------------+----------+----------+----------+

修复表碎片需要时间，不要经常作此操作，可以周期性执行。

## 2、锁机制  所得使用就是为了能够让用户进行等待的操作，阻塞用户的操作。
# mysql中的所类型：
读锁：共享锁 锁定之后可读不可写
写锁：排它锁、独占锁，其他都不可以操作
# mysql中的锁力度类型：
表锁：锁定整个表 操作某一行数据锁定之后，其他数据也不能操作了 myisam 和 InnoDB 都支持;

lock table table_name 锁定方式;
锁定方式：read write
unlock table table_name;

行锁： 只有InnoDB支持。通过事务进行行锁定。
begin commit rollback

使用ab.exe 测试模拟并发

mysql -> ab.exe -c 10 -n 100 url;

flock

锁表其他操作也不能进行了，实际开发中，可以使用文件锁的方式，通过文件的表示来进行确定是否具有操作的权限和资格

实际应用：
抢购出去了超卖现象，如何避免？
1、把剩余的商品数量设置为unsigned（没有负数）；
2、在下订单抢购的时候，使用事务机制和锁机制实现；

### mysql 相关知识
## mysql 用户管理操作及其远程登录

mysql> select User,Password,Host from user;
+------+-------------------------------------------+---------------+
| User | Password                                  | Host          |
+------+-------------------------------------------+---------------+
| root | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | localhost     |
| root | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | devbook.local |
| root | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | 127.0.0.1     |
| root | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | ::1           |
+------+-------------------------------------------+---------------+

## 增加用户实现远程操作工作
# grant all[权限] on 数据库.数据表 to '用户名称'@'主机名或者ip地址' identified by '用户密码';
mysql> grant all on *.* to 'zhang'@'%' identified by '123456';
mysql库中的user表的host字段控制了ip的登录限制。
真实业务中，是不允许root远程登录。使用其他用户进行操作。一般情况下，最好是一个业务使用一个用户和数据库。

mysql> select user,Password,Host from mysql.user;
mysql> flush privileges;
+-------+-------------------------------------------+---------------+
| User  | Password                                  | Host          |
+-------+-------------------------------------------+---------------+
| root  | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | localhost     |
| root  | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | devbook.local |
| root  | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | 127.0.0.1     |
| root  | *81F5E21E35407D884A6CD4A731AEBFB6AF209E1B | ::1           |
| zhang | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 | %             |
+-------+-------------------------------------------+---------------+

还需要在防火墙中开启 3306 端口
sudo vi /etc/sysconfig/iptables 

# mysql 找回密码
开发环境中，可能会遇到数据库密码忘记，可以通过绕过权限，修改密码。
密码是不可能找回的，因为存储的是不可逆加密，只能验证用户具有权限，修改新的密码。
1、添加配置里的绕过参数  my.conf  skip-grant-tables；
2、重启mysql，查看是否启动成功；
3、无用户和密码登录，修改新密码  mysql 直接进入 然后修改密码；
update mysql.user set Password = password('root') where User = 'root';
flush privileges;
4、注释配置绕过项； 

### mysql主从复制
## 1、主从复制和读写分离的概念介绍
分布式数据库架构：多台数据库的架构
# 主从复制：主服务器提供权限和数据，让从服务器进行同步和复制。客观上是存在数据延迟的。
使用范围：
1、实现后续业务的读写分离；
2、从服务器可以作为主服务器的备份服务器；
# 读写分离 将读写业务分配到不同的服务器上，让服务器做特定的操作，不需要不断的切换工作模式，是工作效率提高(切换会影响服务器的性能)；
## 主从复制的实现原理
# 一台服务器写操作，从服务器进行读操作，如果有很多从服务器，主服务器的压力很大，可以选择使用分流主服务器进行同步和复制。

## 配置主从复制 主从最少使用两台服务器。
# 建议搭建主从复制服务器的要求：1、同样的系统平台  2、mysql版本一致
建立服务器需要配置：
1、建立从服务器可以同步的用户及其权限；
2、开启记录日志  bin-log 日志文件
bin-log   binary log 二进制日志文件 记录数据库执行的SQL等操作
在安装mysql的时候，已经默认开启，配置文件路径 /etc/my.cnf   不需要修改，查看一下即可。
bin-log 的一些函数
show binary logs 或者 show master logs  查看所有的日志文件  mysql/data
show master status  查看正在写入的日志文件
使用mysqlbinlog的软件 查看当前binlog文件内容(bin/mysqlbinlog)  
reset master  清空日志，重新开始计数
二进制文件还可以进行数据的恢复操作，
凌晨两点数据丢失如何恢复？（如果没有备份，日志文件没有开 是不能恢复数据的）
1、恢复百分0点  查1—2点的数据
2、根据bin-log文件里记录的信息进行数据恢复
# 使用两台虚拟机进行模拟操作。
配置主服务器 master 
配置从服务器 slave

### 配置主服务器
# 1、建立一个同步权限的用户   Repl_slave_priv: Y
grant all[权限] on 数据库.数据表 to '用户名称'@'主机名或者ip地址' identified by '用户密码';
mysql> grant replication slave on *.* to 'wang'@'%' identified by '123456';
# 2、查看并确定开启了 bin-log  设置唯一的server-id

### 配置从服务器
# 1、修改 derver-id  和主服务器不一样即可
# 2、重启mysql
# 3、停止从服务，配置并启动从服务  stop slave(或者 slave stop);   slave start;

配置告知从服务器的相关信息

change master to master_host='主服务器ip地址',master_user='授权同步用户的名称',master_password='授权同步用户的密码',master_log_file='二进制日志文件的名称',master_log_pos=记录的pos位置;

change master to master_host='192.168.48.128',master_user='backup',master_password='backup',master_log_file='mysql-bin.000003',master_log_pos=401;

在主服务器（master) 查看日志文件记录的名称及其位置
show master status;   (如果没有进行写操作，是不会变的)  file   position

slave start;

查看从服务器的主从状态，并测试主从效果
show slave status;
如果连接失败：
1、主服务器 server-id = 1 ，开启bin-log ， 建立一个 replication slave 权限用户；
2、主服务器防火墙远程3306端口是否开启；
3、从服务器指向主服务器的参数信息是否正确；
然后 停止从服务，配置并启动从服务  stop slave(或者 slave stop);   slave start;

### 实现读写分离
在主从复制分布数据库架构中，写入操作在主服务器执行，读操作在从服务器中执行。不能写从服务器，因为主服务器不会同步服务器信息。
## 1、普通实现
## 2、框架实现
## 3、mysql代理

mysql -> show global variables like 'port';  // 查看mysql端口

sudo /usr/local/mysql/support-files/mysql.server start;  // 启动MySQL服务

sudo /usr/local/mysql/support-files/mysql.server stop; // 停止MySQL服务

sudo /usr/local/mysql/support-files/mysql.server restart; // 重启MySQL服务

/applications/mamp/library/bin/mysql -uroot -p

vim ~/.bash_profile  // 配置环境变量

source ./.bash_profile


mysqld，也称为MySQL Server，是一个单线程程序，可以完成MySQL安装中的大部分工作。它不会产生其他进程。
