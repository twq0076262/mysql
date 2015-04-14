# MySQL 复制表

在某些情况下，你可能需要精确复制一个表。CREATE TABLE ... SELECT 并不适用于此要求，因为这个复制表必须与原有表在索引、默认值等方面都完全相同。   

可以采用如下步骤来处理这种情况。   

- 使用 SHOW CREATE TABLE 或 CREATE TABLE 语句指定源表的结构、索引以及所有的内容。    
- 调整语句，将表名改为克隆表的名称，执行语句。这样就对表进行了克隆。
- 另外，如果想要克隆表的全部内容，也可以使用 INSERT INTO ... SELECT 语句。




## 范例   

通过下面这个范例来创建表 tutorial_tbl 的克隆表：   

### 步骤1     

获取表的完整结构。  


```
mysql> SHOW CREATE TABLE tutorials_tbl \G;
*************************** 1. row ***************************
       Table: tutorials_tbl
Create Table: CREATE TABLE `tutorials_tbl` (
  `tutorial_id` int(11) NOT NULL auto_increment,
  `tutorial_title` varchar(100) NOT NULL default '',
  `tutorial_author` varchar(40) NOT NULL default '',
  `submission_date` date default NULL,
  PRIMARY KEY  (`tutorial_id`),
  UNIQUE KEY `AUTHOR_INDEX` (`tutorial_author`)
) TYPE=MyISAM
1 row in set (0.00 sec)

ERROR:
No query specified
```

### 步骤2   

重新命名该表，创建另一个表。  

```
mysql> CREATE TABLE `clone_tbl` (
  -> `tutorial_id` int(11) NOT NULL auto_increment,
  -> `tutorial_title` varchar(100) NOT NULL default '',
  -> `tutorial_author` varchar(40) NOT NULL default '',
  -> `submission_date` date default NULL,
  -> PRIMARY KEY  (`tutorial_id`),
  -> UNIQUE KEY `AUTHOR_INDEX` (`tutorial_author`)
-> ) TYPE=MyISAM;
Query OK, 0 rows affected (1.80 sec)

``` 

### 步骤3   

执行完步骤2后，就在数据库中创建了一个克隆表。如果想从旧表中复制数据，可以使用 INSERT INTO... SELECT 语句。  


```
mysql> INSERT INTO clone_tbl (tutorial_id,
    ->                        tutorial_title,
    ->                        tutorial_author,
    ->                        submission_date)
    -> SELECT tutorial_id,tutorial_title,
    ->        tutorial_author,submission_date,
    -> FROM tutorials_tbl;
Query OK, 3 rows affected (0.07 sec)
Records: 3  Duplicates: 0  Warnings: 0

```  

最终，果如所愿，你得到了精确的克隆表。