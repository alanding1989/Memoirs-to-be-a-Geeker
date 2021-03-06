
<!-- vim-markdown-toc GFM -->

- [数据库](#数据库)
  - [数据库事务](#数据库事务)
  - [事务隔离级别](#事务隔离级别)
  - [锁](#锁)
  - [三大范式-解决如何设计数据库表的问题](#三大范式-解决如何设计数据库表的问题)
  - [多表联查](#多表联查)
  - [分页](#分页)
  - [索引](#索引)
  - [常用demo](#常用demo)
  - [MySQL](#mysql)
  - [MongoDB](#mongodb)
  - [全文检索 elasticSearch](#全文检索-elasticsearch)
  - [Redis](#redis)

<!-- vim-markdown-toc -->


## 数据库

### 数据库事务
> 指若干SQL语句构成的一个操作序列。  

- 为什么需要事务  
  解决并发访问数据库的问题，保证多个SQL语句全部执行，要么全部取消。  

- ACID特性  
  - Atomicity   : 原子性，一个事务虽然由多个SQL语句构成，但是操作本身是一个原子操作，要么全部成功，要么
    全部失败。  

  - Consistency : 一致性，一个事务在开始前和结束后，数据是完整的，不存在数据冲突。即事务被异常中断，也不会使数据库数据不一致。  

  - Isolation   : 隔离性，多个事务**并发**执行时，相互之间互不影响。  

  - Durability  : 持久性，一个事务一旦成功完成，对数据库的更改就是永久的，并且不会被回滚。  

  
### 事务隔离级别  
> 事务隔离级别是由于数据库允许多个连接同时执行事务引起的。当一个线程操作一个数据库连接时，另一个线程
  可能也在通过一个数据库连接更新数据，即多个线程并发操作数据库数据，它们之间就会遇到数据库隔离级别的问题。
  低级别的隔离一般支持更高的并发处理，并拥有更低的系统开销。

- 并发事务产生的问题
  - 脏读
    事务A更新一份数据还没提交，事务B读取这份数据，之后事务A进行了回滚，那么事务B读取的数据就是错误的。

  - 不可重复读  
    某事务两次查询同一数据结果不一致，因为另一个事务在该事务两次读取数据期间进行了修改并提交。

  - 幻读

- 为了解决上面的三个问题，数据库定义了四种事务的隔离级别
  
  - Read Uncommitted（读取未提交内容）－三个问题都会出现
    在该隔离级别，所有事务都可以看到其他未提交事务的执行结果。本隔离级别很少用于实际应用，
    因为它的性能也不比其他级别好多少。读取未提交的数据，也被称之为脏读（Dirty Read）。

  - Read Committed（读取提交内容）－可避免脏读
    它满足了隔离的简单定义：一个事务只能看见已经提交事务所做的改变。
    - 原理：读无锁，改用行级共享锁

  - Repeatable Read（可重读）－可避免脏读和不可重复读
    这是MySQL的默认事务隔离级别，确保同一连接的多个实例在并发读取数据时，会看到同样的数据行。
    在一个事务修改数据过程中，如果事务还没提交，其他事务不能读该数据。
    - 原理：读取行级共享锁，改行级互斥锁。

  - Serializable（可串行化）－可完全避免三个问题
    这是最高的隔离级别，它通过强制事务排序(串行执行)，使之不可能相互冲突，从而解决幻读问题。
    它在每个读的数据行上加上共享锁。在这个级别，可能导致大量的超时现象和锁竞争。
    - 原理：读取`表级`共享锁直到事务结束释放。  
            写`表级`互斥锁直到事务结束释放。

  <img src=../0.Resources/database/database-isolationlevel.png>


### 锁
- 读写锁：支持多个事务读，但只有单个事务改

- 互斥锁：同一时间只允许单个事务对数据进行访问


### 三大范式-解决如何设计数据库表的问题
- 第一范式：非主键字段属性不可再分，例如出生年月日，如要分更细，那就不满足要求。

- 第二范式：消除非主键字段与主键无关的情况，例如主键为学号，字段课程号、学分不依赖主键，所以需剔除。
  
- 第三范式：消除非主建字段的传递依赖。


### 多表联查
  - 一对多：查询单个产品分类，显示多个产品
    产品分类表，某类的产品表。
    一个包类有若干个包产品，先不考虑包的不同用途分类。

  - 多对一：查询一个订单上的产品，显示多个产品类别
    包，显示包所属产品的类别。
    电视，显示电视所属产品的类别。

  - 多对多
    维护不同订单的表，order和orderItem，一对多关系。
    单个订单包含哪些产品的表。
    一张订单包含多种产品，但这没有类别从属关系，组合关系。


### 分页


### 索引


### 常用demo

- 新建用户  
  ```sql
  GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP
      ON TUTORIALS.*
      TO 'zara'@'localhost'
      IDENTIFIED BY 'zara123';
  ```

- 查询：
  ```sql
  select * from table order by id desc limit ?,?
  ```

- 建表：

  ```sql
  DROP DATABASE IF EXISTS mybatis;
  CREATE DATABASE mybatis DEFAULT CHARACTER SET utf8;

  use mybatis;
  CREATE TABLE student(
    id int(11) NOT NULL AUTO_INCREMENT,
    studentID int(11) NOT NULL UNIQUE,
    name varchar(255) NOT NULL,
    PRIMARY KEY (id)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

  INSERT INTO student VALUES(1,1,'小明');
  INSERT INTO student VALUES(2,2,'小红');
  INSERT INTO student VALUES(3,3,'小白');

  ```


### MySQL


### MongoDB


### 全文检索 elasticSearch


### Redis
