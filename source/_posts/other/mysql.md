---
title: mysql自学笔记
categories: other
tags: 
- mysql
---

## 数据库的三层结构

* node应用程序
* dbms (数据库管理系统)  编译 （费时间）-》 执行 -》 缓存（分页存储过程， 触发器）
* 数据库

## 数据库优化

* 标的设计合理化 符合3NF
* 添加索引： 普通索引， 主键索引， 唯一索引， 全文索引
* 分表技术：  水平分割，垂直分割
* 读写 ：（写 updata, delete, add）分离
* 存储过程： 模块化编程 可以提高速度
* 对 mysql 配置的优化 （配置最大并发数 my.ini max_connections=100 (一般网站调到1000左右) ， 缓存的大小）
* 服务器硬件的升级 （内存小， cpu）
* 定时的清除不需要的数据， 定时进行碎片整理（MYISAM）

### 什么表是三范式的表（3NF）

* 表的范式： 首先符合1范式 才能满足2范式 进一步满足3范式 （最高6范式）
* 1NF: 及 属性的表的列具有原子性 不可在分解  及列的信息不可分解 （每个信息可以明确的表明含义） 关系型数据 自动满足1NF  
* 2NF 表中的记录是唯一的  （通常设置一个主键来满足  主键： 不含业务逻辑， 自增）
* 3NF 表中不应该有 冗余数据  （表中的数据如果能推导出来 就不应该单独写一个字段）----- 查询的时候，多表连续查询
* 在表 一对多的情况下 为了提高效率 做反3范式 可以存在冗余数据

### sql语句优化

--| 问题是： 如何在一个大项目中，迅速的定位执行慢的语句   （慢查询）

* 了解mysql 数据库的一些运行状态 如何查询  （比如： 想知道mysql 运行时间， 一共执行了多少次，add, update，  当前的链接）
* 常用的命令：  (语句一定要加分号)
    1. show status; 查看状态
    2. show [seesion|global] status like 'uptime';  启动时间  ‘com_select’ 'insert' 'delete'  默认 sesison 当前会话   global 从启动到现在所有
        'connections' 查看链接次数    / 显示慢查询  'slow_queries'
    3. 如何定位慢查询： （默认情况下 10s 才是慢查询 测试先修改为1s ）[慢查询命令](https://blog.csdn.net/keketrtr/article/details/78673565)
    4. show VARIABLES like 'long_query_time'; 显示当前慢查询时间
    5. set long_query_time=1; 设置慢查询时间

* 构建一个大表  400万条数据  （存储过程构建) 
* (花费我不少时间)创建函数时出现的问题：http://www.cnblogs.com/kerrycode/p/7641835.html  开启二进制日志  set log_bin_trust_function_creators=1;  （这知识临时创建的临时的函数）
    这里创建函数 跟 navicat 中创建事物不一样 这里是全局函数；
* call insert_emp(10001, 4000000); 插入数据 400万条数据；  （存储过程不写了 随机字符串函数也不写了）
* 这个时候如果我们慢查询就会被统计到到 （超过1s的）
* 把慢查询的记录到我们的日志当中（默认 MySQL不记录慢查询日志， 启动mysql 的时候启动慢查询记录）

### 开始优化（索引优化）

* 数据库第一次搜索响应会慢，如果使用相同的 sql 语句， sql 会缓存sql 查询的结果，响应给客户端；

* 四种索引（主键索引，全文索引，唯一索引， 普通索引）（索引会记录文件内容的物理位置）
    1. 添加索引
        * 主键索引添加  （概念： 把表中的某一列设置为主键的时候，该列就是主键索引）
        * 普通索引添加 （一般先创建表 在创建普通索引） create index 索引名 on 表 （列1， 列2）；
        * 全文索引  （主要是针对于文件， 文本检索。比如文章） 全文索引针对 MYISAm 有用  （myisam 介绍： https://www.cnblogs.com/avivahe/p/5427884.html）
            说明：
            1. fulltext 全文索引只针对 myisam 生效
            2. mysql 提供的 fulltext 针对英文生效 （中文： sphinx(coreseek)技术处理中文）
            3. 使用方法  match(字段名) against('关键字');
            4. 全文索引有停止词的概念， 对一些常见的词 不会创建索引。因为在文本中创建索引是一个无穷大的数。  这些词就成为 ’停止次‘
        * 当某一些被指定为 unique 时， 这一列就是唯一索引；unique 可以为 null 并且可以有多个 空字符串‘’ 只能有一个  、、   主键索引不能为空也不能重复  
            create table ddd(id int primary key auto_increment , name varchar(32) unique); 这时, name 列就是一个唯一索引.
        * 创建多列索引 alter talbe 表名 add index myind (dname, loc)  (解释： 会在当前表中 dname列于loc列 创建共同的索引， 索引名为 myind)
            把dept表中，我增加几个部门: alter table dept add index my_ind (dname,loc); //  dname 左边的列,loc就是右边的列
            说明，如果我们的表中有复合索引(索引作用在多列上)， 此时我们注意:
            1. 对于创建的多列索引，只要查询条件使用了最左边的列，索引一般就会被使用。 explain select * from dept where loc='aaa'\G (不会使用索引)
            2. 对于使用like的查询，查询如果是  ‘%aaa’ 不会使用到索引  *** ‘aaa%’ 会使用到索引。 ***
            3. 如果条件中有or，即使其中有条件带索引也不会使用。换言之，就是要求使用的所有字段，都必须建立索引, 我们建议大家尽量避免使用or 关键字   select * from dept where dname=’xxx’ or loc=’xx’ or deptno=45
            4. 如果列类型是字符串，那一定要在条件中将数据使用引号引用起来。    否则不使用索引。(添加时,字符串必须’’), 也就是，如果列是字符串类型，就一定要用 ‘’ 把他包括起来.
            5. 如果mysql估计使用全表扫描要比使用索引快，则不使用索引。

    2. 查询索引
        * desc 表名； （最简单 缺点：不能够显示索引的名字）
        * show index[es] from 表名；
        * show keys from 表名；
    3. 删除
        * alter table 表名 drop index 索引名；
        * 删除主键索引   alter table 表名 drop primary key; (因为只有一列是主键索引， 所以不需要指定列名)
    4. 修改
        * 先删除 在创建；

* 索引使用的注意事项
    索引的代价：
    1. 占用磁盘空间
    2. 对dml （updata delete insert）有影响 会维护索引文件  
    3. btree 检索方式 （存储引擎： myisam, innodb 都是 btree检索方式 二叉树）（ 存储引擎：memory（也叫堆）/heap 用 hash/btree   (比较古老)）

    在那些列上适合添加索引：
    1. 较为频繁作为 查询条件的  字段 应该创建索引
    2. 唯一性的词不适合作为索引 例如：性别-男
    3. 更新非常频繁的字段也不能创建索引   例如：登录的次数  select * from eee where logincount=1  

    总结：满足一下条件创建索引
    1. 肯定在 where 中经常使用的字段创建索引
    2. 该字段的内容不是唯一的几个值 例如性别 
    3. 字段内容不是频繁变化的

    如何查看索引使用的情况: show status like 'Handler_read%';
    大家可以注意：
    1. handler_read_key:这个值越高越好，越高表示使用索引查询到的次数。
	2. handler_read_rnd_next:这个值越高，说明查询低效

* 大批量插入数据（mysql 管理员）导数据的使用；了解
    1. 对于myisam
        * alter table table_anme disable keys; 关闭索引
        * loading data // insert 语句；
    * alter table table_name enable keys;
    2. 对于innodb;
        * 将要导入的数据按照主键排序
        * set unique_checks=0; 关闭唯一性校验
        * set autocommit=0 关闭自动提交


### sql 语句的优化 （小技巧）

* 在使用 group by 分组查询时 ，默认分组后 还会排序， 可能会降低速度；  解决方案：  在group by 后面增加 order by null 就可以防止排序.
* 有些时候可以用连接 （join）来替代子查询，因为使用join mysql 不需要再内存中创建临时表； select * from bbb left join emp1 on bbb.name=emp1.deptno (左外连接)
* myisam 存储引擎 ----》 要定时进行碎片整理； 当你删除数据后， 真正的文件不会缩小 ，整理语句：  optimize table test100; 

### 定时维护


### sql语句搜集

* 查看表的结构  desc dept;
* 创建表  create table bbb(id int, name varchar(32) not null defatul '');
* 给表添加索引 alter table bbb add primary key (id);
* 如何使用全文索引:
    错误用法:
    select * from articles where body like ‘%mysql%’; 【不会使用到全文索引】
    证明:
    explain  select * from articles where body like '%mysql%'
    正确的用法是:
    select * from articles where match(title,body) against(‘database’); 【可以】
 * group by 使用方式 https://blog.csdn.net/qq_15037231/article/details/79975646；
 * select * from bbb, emp1 where bbb.name=emp1.deptno;（简单的）  

### 数据库文件解释

* emp.frm 表的结构文件  
  emp.MYD 表的内容
  emp.MYI 表的索引

### 数据库存储引擎

* innodb （订单表， 账户表）（对事物要求高，保存的数据都是重要数据）
    1. 优点：支持事务和外键，数据完整性机制比较完备；可以用SHOW TABLE STATUS查得某个库或表的磁盘占用  
    2. 缺点：速度超慢，磁盘空间占用多；所有库都存于一个（通常情况）或数个文件中，无法通过操作系统了解某个库或表的占用空间
* myisam  （bbs 中的发帖表 和 回复表）（ 以查询和添加为主，对事物要求不高）
    1. 优点：速度快，磁盘空间占用少；某个库或表的磁盘占用情况既可以通过操作系统查相应的文件（夹）的大小得知，也可以通过SQL语句SHOW TABLE STATUS查得
    2. 缺点：没有数据完整性机制，即不支持事务和外键
* memory 存储， （使用推荐： 我们的数据变化频繁，不需要入库，同时又频繁的查询和修改）

* 问 MyISAM 和 INNODB的区别
    1. 事务安全
    2. 查询和添加速度
    3. 支持全文索引
    4. 锁机制
