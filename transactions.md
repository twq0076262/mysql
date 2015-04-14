# MySQL 汇报

事务就是一组连续的数据库操作，执行起来仿佛像是单一的工作单元。换句话说，除非该组内所有操作都成功完成，否则事务永远不会结束。如果事务中的某一个操作失败，则整个事务也将失败。    

实际上，将在一个组中结合许多 SQL 查询，你将同时执行所有的事务，作为事务的一部分。    

## 事务的特点  

事务一般具有以下4种典型特点，人们通常会用这4种特点的英文首字母缩写组合词 ACID 来表示。  

- **原子性**（**Atomicity**）确保工作单元内的所有操作都能成功完成。如若不然，事务在遭受失败时就会被放弃，之前的种种操作就会被撤销回它们之前的状态。  
- **一致性**（**Consistency**）确保数据库能够在成功提交的事务的基础上正确改变状态。  
- **隔离性**（**Isolation**）使事务能够独立操作，事务之间彼此透明。  
- **持久性**（**Durability**）确保当系统发生失败时，已提交的事务的结果或者说效果能够持续存在。    

在 MySQL 中，事务通常以 BEGIN WORK 语句开始，以 COMMIT 或 ROLLBACK（只取其一） 语句结束。在开始与结束声明之间的 SQL 命令就构成了事务的主体。   


## COMMIT 与 ROLLBACK 

MySQL事务主要用到两个关键字 **COMMIT** 与 **ROLLBACK**：    

- 成功完成一个事务后，就会执行 COMMIT 命令，从而使施加于所涉及的表上的改变生效。 
- 如果事务失败，就会执行 ROLLBACK 命令，将事务中所引用的每一个表都回撤到之前的状态。



通过设定会话变量 **AUTOCOMMIT** 可以控制事务行为。如果 AUTOCOMMIT 被设为1（默认值），则每一个 SQL 语句（无论是否在事务中）都会被认为是一个完成的事务，则默认当它结束时予以提交。当 AUTOCOMMIT 被设为0（通过命令 SET AUTOCOMMIT=0）时，后续一系列语句就像是一个事务，直到 COMMIT 语句执行为止，不再提交任何行为。


可以在 PHP 中利用 mysql_query()执行 SQL 命令。


## 事务的常见范例  


这些事件都跟所用的编程语言无关。逻辑路径可以用你所使用的任何语言来创建。  

可以在 PHP 中利用 mysql_query()执行 SQL 命令。

- 通过执行 SQL 命令 BEGIN WORK 可开启事务。

- 执行一个或更多的如下 SQL 命令：SELECT、INSERT、UPDATE 或 DELETE。

- 检查是否有错，一切是否符合要求。

- 如果出错，执行 ROLLBACK 命令，否则利用 COMMIT 命令提交。

## MySQL 中的事务安全型表类型  



不能直接使用事务，如果强行使用，则无法保证它们的安全性。如果打算在 MySQL 编程中使用事务，就需要以特殊的方式来创建表。有很多种支持事务表可供选择，但其中最常见的是 InnoDB。

对 InnoDB 表的支持，需要在编译 MySQL 源码时用到一个特殊的编译参数。如果 MySQL 版本不支持 InnoDB，则需要请你的 ISP 构建一个支持 InnoDB 表类型的 MySQL 版本，或者下载安装一个用于 Windows 或 Linux/UNIX 系统的 MySQL-Max 二进制分发版，在其开发环境中使用这种表类型。

如果你的 MySQL 版本支持 InnoDB 表，则只需在表创建语句中添加一个 TYPE = InnoDB 定义即可。比如，下面这段代码就创建了一个叫做 tcount_tbl 的 InnoDB 表。




```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> create table tcount_tbl
    -> (
    -> tutorial_author varchar(40) NOT NULL,
    -> tutorial_count  INT
    -> ) TYPE=InnoDB;
Query OK, 0 rows affected (0.05 sec)
```

有关InnoDB的详细信息，可参看这个链接：   

如果你的 MySQL 支持 GEMINI 或 BDB 这两种表类型，也可以使用它们。