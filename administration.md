# MySQL 管理

## 运行与关闭 MySQL 服务器  

首先检查 MySQL 服务器是否正在运行。可以使用下列命令来确认这一点：  

`ps -ef | grep mysqld`  

如果 MySQL 正在运行，在上述命令的运行结果中就能看到 **mysqld** 进程。如果服务器没有运行，使用下列命令来启动它：   

```
root@host# cd /usr/bin
./safe_mysqld &

```

如果想关闭正在运行的 MySQL 服务器，使用如下命令即可：   

```
root@host# cd /usr/bin
./mysqladmin -u root -p shutdown
Enter password: ******

```




## 建立 MySQL 用户账号  

添加新的 MySQL 用户，只需在数据库 **mysql** 的 **user** 表中添加一个新项即可。   
   

在以下范例中，添加了一个新用户 guest，该用户具有 SELECT、INSERT、UPDATE 权限，密码是 guest123。SQL 查询如下：    

```
root@host# mysql -u root -p
Enter password:*******
mysql> use mysql;
Database changed

mysql> INSERT INTO user 
          (host, user, password, 
           select_priv, insert_priv, update_priv) 
           VALUES ('localhost', 'guest', 
           PASSWORD('guest123'), 'Y', 'Y', 'Y');
Query OK, 1 row affected (0.20 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 1 row affected (0.01 sec)

mysql> SELECT host, user, password FROM user WHERE user = 'guest';
+-----------+---------+------------------+
| host      | user    | password         |
+-----------+---------+------------------+
| localhost | guest | 6f8c114b58f2ce9e |
+-----------+---------+------------------+
1 row in set (0.00 sec)

```

在添加新用户时，记住要用 MySQL 提供的 `PASSWORD()` 函数对该用户的密码进行加密处理。如上例所示，密码 mypass 被加密成了 6f8c114b58f2ce9e。   

注意这里所用的 FLUSH PRIVILEGES 语句。它让服务器重新加载授权表。如果不使用它，就至少得等到服务器重新启动后，才能使用新用户账号连接 mysql。  

你也可以为新用户指定其他权限，在执行 INSERT 查询时，将用户表中的下面这些列的值都设为 ‘Y’，或者使用 UPDATE 查询稍后对它们进行更新。     

- Select_priv

- Insert_priv

- Update_priv

- Delete_priv

- Create_priv

- Drop_priv

- Reload_priv

- Shutdown_priv

- Process_priv

- File_priv

- Grant_priv

- References_priv

- Index_priv

- Alter_priv  






另外一种添加用户账号的方式是使用 SQL命令 GRANT。下面这个例子将在数据库 **TUTORIALS** 上添加一个名为 **zara** 的新用户，其密码为 **zara123**。如下所示：   


```  
root@host# mysql -u root -p password;
Enter password:*******
mysql> use mysql;
Database changed

mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP
    -> ON TUTORIALS.*
    -> TO 'zara'@'localhost'
    -> IDENTIFIED BY 'zara123';
   
```

这会在 mysql 数据库的 **user** 表中创建一个项。  

> **注意**：如果 SQL 命令不以分号（`;`）结束的话，MySQL 就不会终止这个命令。     


  


## 配置 /etc/my.cnf 文件    

大多数情况下，根本用不到这个文件。默认状态下，它应该包含如下项：   

```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock

[mysql.server]
user=mysql
basedir=/var/lib

[safe_mysqld]
err-log=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
  
```  

在这里，可以为 error log 更换不同的目录。另外，不要更改这张表中的其他项。  







## 用于管理 MySQL 的一些命令    

下面列出了一些重要且经常会用到的MySQL命令：     


- **USE *Databasename*** 用于在MySQL工作区内选择具体某个数据库。  
- **SHOW DATABASES** 列出 MySQL DBMS 所能访问的数据库。   
- **SHOW TABLES** 一旦数据库被 use 命令选中，显示数据库中的表。
- **SHOW COLUMNS FROM *tablename*** 显示表的属性、属性类型、键信息、是否允许 NULL 值，默认值，以及其他一些信息。  
- **SHOW INDEX FROM *tablename*** 显示表中所有索引的细节信息，包括PRIMARY KEY。  
- **SHOW TABLE STATUS LIKE *tablename*\G** 报告MySQL DBMS的性能及统计的细节信息。  




