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
- 原子性
- 一致性
- 隔离性
- 持久性
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
    
        
    
    
    


