# 数据库 MySQL

### 数据库的增删切换：
    创建数据库：create database test;
    切换数据库：use test;
    删除数据库：drop database test;
### 数据类型
- 数值类型

        TINYINT    1字节    
        SMALLINT    2字节    
        MEDIUMINT    3字节    
        INT 或INTEGER    4字节
        BIGINT    8字节
        FLOAT    4字节
        DOUBLE    8字节
        DECIMAL    小数值，依赖于M和D
- 日期和时间类型
        
        DATE    3字节    YYYY-MM-DD
        TIME    3字节    HH:MM:SS
        YEAR    1字节    YYYY
        DATETIME    8字节    YYYY-MM-DD HH:MM:SS
        TIMESTAMP    4字节    YYYYMMDD HHMMSS    时间戳
- 字符串类型
        
        CHAR    0-255字节    定长字符串
        VARCHAR    0-65535字节    边长字符串
        TINYBLOB    0-255字节    不超过255个字符的二进制字符串
        TINYTEXT    0-255字节    短文本字符串
        BLOB    0-65535字节    二进制形式的长文本数据
        TEXT 0-65535字节    长文本数据
        MEDIUMBLOB    ...    二进制形式的中等长度文本数据
        MEDIUMTEXT    ...    中等长度文本数据
        LONGBLOG    ....    二进制形式的极大文本数据
        LONGTEXT    ....    极大文本数据
### 事务的四个条件
- 原子性（Atomicity）：

        事务作为一个整体被执行，包含在其中的对数据库的操作要么全部被执行，要么都不执行。
- 一致性（Consistency）：
        
        事务应确保数据库的状态从一个一致状态转变为另一个一致状态。一致状态的含义是数据库中的数据应满足完整性约束。
- 隔离性（Isolation）：
        
        多个事务并发执行时，一个事务的执行不应影响其他事务的执行。
- 持久性（Durability）：

        一个事务一旦提交，他对数据库的修改应该永久保存在数据库中。
### 创建索引的几种方式
- 直接创建
        
        create index first_index on student(username(length));
- 修改表结构

        alter table student add index first_index(username);
- 创建时直接指定

        CREATE TABLE mytable(  

        ID INT NOT NULL,   

        username VARCHAR(16) NOT NULL,  

        INDEX [indexName] (username(length))  

        );  
- 删除索引
        
        drop index first_index on student;
- 显示索引信息

        show index from student;
- 唯一索引
        
        create unique index first_index on student(username(length));
### MySQL分页查询的几种方法
#### limit基本实现方式
一般情况下，客户端通过传递 pageNo（页码）、pageSize（每页条数）两个参数去分页查询数据库中的数据，在数据量较小（元组百/千级）时使用 MySQL自带的 limit 来解决这个问题：
    
        收到客户端{pageNo:1,pagesize:10}
        select * from table limit (pageNo-1)*pageSize, pageSize;
        收到客户端{pageNo:5,pageSize:30}
        select * from table limit (pageNo-1)*pageSize,pageSize;
#### 建立主键或者唯一索引
在数据量较小的时候简单的使用 limit 进行数据分页在性能上面不会有明显的缓慢，但是数据量达到了 万级到百万级 sql语句的性能将会影响数据的返回。这时需要利用主键或者唯一索引进行数据分页；
        
        假设主键或者唯一索引为 good_id
        收到客户端{pageNo:5,pagesize:10}
        select * from table where good_id > (pageNo-1)*pageSize limit pageSize;
        返回good_id为40到50之间的数据
#### 基于数据再排序
当需要返回的信息为顺序或者倒序时，对上面的语句基于数据再排序。order by ASC/DESC 顺序或倒序 默认为顺序

        select * from table where good_id > (pageNo-1)*pageSize order by good_id limit pageSize;
        返回good_id为40到50之间的数据,数据依据good_id顺序排列

        

