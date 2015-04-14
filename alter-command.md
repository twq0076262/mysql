# MySQL ALTER 命令

利用 MySQL 的 **ALTER** 命令可以很方便地修改表名与表字段名，以及添加或删除表中已有的列。    

为了实践 **ALTER** 命令，下面先来创建一个名为 **testalter_tbl** 的表。  

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> create table testalter_tbl
    -> (
    -> i INT,
    -> c CHAR(1)
    -> );
Query OK, 0 rows affected (0.05 sec)
mysql> SHOW COLUMNS FROM testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| i     | int(11) | YES  |     | NULL    |       |
| c     | char(1) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)

```

## 删除、添加列或对其重新定位   

假如要从上面我们创建的这张表中删除 **i** 这一列，那么应该使用 **DROP** 子句和 **ALTER** 命令，如下所示：   

`mysql> ALTER TABLE testalter_tbl  DROP i;`  

如果表中只有一列，则 **DROP** 子句不起作用。   

添加一列，使用 ADD 并指定列定义。下面我们再把 **i** 这一列恢复到 testalter_tbl 中。    

`mysql> ALTER TABLE testalter_tbl ADD i INT;`   

输入该语句之后，这张表将跟之前创建时一样，含有2列。但结构却稍有差异。默认情况下，新增加的列位于表的末尾。在创建表时，**i** 是第一列，现在却成为最后一列。   

```
mysql> SHOW COLUMNS FROM testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)

```    

要想把列放到一个特定位置，可以使用两种方法。第一种方法是使用 FIRST，让指定列成为第一列；第二种则采用 AFTER 后跟给定列名的方式，指示新列应该放到给定列名的后面。下面分别利用 ALTER TABLE 语句对列进行操作，每执行完一行后，我们可以使用 SHOW COLUMNS 来查看一下各自的效果。   

```
ALTER TABLE testalter_tbl DROP i;
ALTER TABLE testalter_tbl ADD i INT FIRST;
ALTER TABLE testalter_tbl DROP i;
ALTER TABLE testalter_tbl ADD i INT AFTER c;

```  

标识符 FIRST 和 AFTER 只能和 ADD 子句一起使用。这也意味着，如果要重新定位一列，就必须先用 DROP 删除它，然后再用 ADD 将它添加到新的位置。  

## 改变一列的定义或名称   

要想改变列的定义，需要使用 **MODIFY** 或 **CHANGE** 子句，并配合使用 ALTER 命令。例如，把列 **c** 从 CHAR(1) 变为 CHAR(10)：     

`mysql> ALTER TABLE testalter_tbl MODIFY c CHAR(10);`  

CHANGE 的语法稍有不同。必须把所要改变的列名放到 CHANGE 关键字的后面，然后指定新的列定义。相关范例如下所示：   

`mysql> ALTER TABLE testalter_tbl CHANGE i j BIGINT;`   

同理，如果想利用 CHANGE 将 j 从 BIGINT 转为 INT，并且不改变列名，则语句如下：   

`mysql> ALTER TABLE testalter_tbl CHANGE j j INT;`    




## ALTER TABLE 对 Null 及默认值属性的作用


在利用 MODIFY 或 CHANGE 修改列时，还可以指定该列是否能有 NULL 值，以及它的默认值。事实上，如果我们不这样处理，MySQL 会自动为这些属性指定相关值。  

例如，NOT NULL 列默认值为100：   

```
mysql> ALTER TABLE testalter_tbl 
    -> MODIFY j BIGINT NOT NULL DEFAULT 100;

```

如果不使用上述命令，则MySQL 会在所有这些列中填充 NULL 值。   


## 改变列的默认值  

使用 ALTER 命令可以改变任何列的默认值，如下例所示：   

```
mysql> ALTER TABLE testalter_tbl ALTER i SET DEFAULT 1000;
mysql> SHOW COLUMNS FROM testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | 1000    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)

```

使用 DROP 子句与 ALTER 命令，可以去除任何列中的默认限制。  

```
mysql> ALTER TABLE testalter_tbl ALTER i DROP DEFAULT;
mysql> SHOW COLUMNS FROM testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)

```

## 改变表类型   


结合使用 **TYPE** 子句与 ALTER 命令，可以使用表类型。在下面范例中，将表 testalter_tbl 的表类型变为 **MYISAM**。   

通过 SHOW TABLE STATUS 语句可以显示当前的表类型。   

```
mysql> ALTER TABLE testalter_tbl TYPE = MYISAM;
mysql>  SHOW TABLE STATUS LIKE 'testalter_tbl'\G
*************************** 1. row ****************
           Name: testalter_tbl
           Type: MyISAM
     Row_format: Fixed
           Rows: 0
 Avg_row_length: 0
    Data_length: 0
Max_data_length: 25769803775
   Index_length: 1024
      Data_free: 0
 Auto_increment: NULL
    Create_time: 2007-06-03 08:04:36
    Update_time: 2007-06-03 08:04:36
     Check_time: NULL
 Create_options:
        Comment:
1 row in set (0.00 sec)

```

## 对表进行重命名  

使用 ALTER TABLE 语句的 **RENAME** 选项可以对表进行重命名。下面范例将表 testalter_tbl 重新命名为 alter_tbl。  


`mysql> ALTER TABLE testalter_tbl RENAME TO alter_tbl;`  

还可以使用 ALTER 命令来创建并删除 MySQL 文件中的索引。下一节再介绍这种用法。




