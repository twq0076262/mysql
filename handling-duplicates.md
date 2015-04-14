# MySQL Handling Duplicates

表或结果集有时会包含重复记录。这种情况一般来说是允许出现的，但有时却需要终止这些重复记录。在某些情况下，需要找出重复记录并将其删除。下面就来介绍一下如何防止表中出现重复记录，如何删除已有的重复记录。  

## 防止表中出现重复记录   

可以在表中正确的字段内使用 PRIMARY KEY 或 UNIQUE 索引来终止重复记录。比如下面这张表，由于没有这样的索引或主键，因此 first_name与last_name 就被重复记录了下来。   

```
CREATE TABLE person_tbl
(
    first_name CHAR(20),
    last_name CHAR(20),
    sex CHAR(10)
);

```   

为了防止表中出现同样姓名的值，为其添加一个 PRIMARY KEY。同时要注意将索引列声明为 NOT NULL，这是因为 PRIMARY KEY 不允许出现空值。    

```
CREATE TABLE person_tbl
(
   first_name CHAR(20) NOT NULL,
   last_name CHAR(20) NOT NULL,
   sex CHAR(10),
   PRIMARY KEY (last_name, first_name)
);

```

表中的唯一索引通常会造成错误，如果往表中插入一个记录，复制了定义该索引的一个列（或多个列）中的一个已存记录，问题就会产生。   




不要使用 **INSERT** ，使用 **INSERT IGNORE**。如果一个记录没有复制一个已存在的记录，MySQL 就会将它照常插入。如果该记录与现存的某个记录重复，IGNORE 关键字就会让 MySQL 默默地将其摒弃，不会产生任何错误。   

下面这个范例不会产生任何错误，不会插入会产生重复的记录。   


```
mysql> INSERT IGNORE INTO person_tbl (last_name, first_name)
    -> VALUES( 'Jay', 'Thomas');
Query OK, 1 row affected (0.00 sec)
mysql> INSERT IGNORE INTO person_tbl (last_name, first_name)
    -> VALUES( 'Jay', 'Thomas');
Query OK, 0 rows affected (0.00 sec)

``` 


使用 **REPLACE** 而不是 INSERT。如果记录是一个新记录，使用 INSERT 就可以了。如果是一个重复记录，新的记录将会替换旧有记录。   

```
mysql> REPLACE INTO person_tbl (last_name, first_name)
    -> VALUES( 'Ajay', 'Kumar');
Query OK, 1 row affected (0.00 sec)
mysql> REPLACE INTO person_tbl (last_name, first_name)
    -> VALUES( 'Ajay', 'Kumar');
Query OK, 2 rows affected (0.00 sec)

```

应该根据想要达到的重复处理行为来选择INSERT IGNORE 和 REPLACE。INSERT IGNORE 会保存重复记录的第一个，抛弃其余的记录；REPLACE 则正好相反，保存最后一个记录，去掉在其之前的所有记录。   

强制唯一性的另一种办法是为表添加 UNIQUE 索引而不是主键。   

```
CREATE TABLE person_tbl
(
   first_name CHAR(20) NOT NULL,
   last_name CHAR(20) NOT NULL,
   sex CHAR(10)
   UNIQUE (last_name, first_name)
);

```


## 确认重复记录，并计算重复记录数   

下面是计算表中姓名记录重复的查询：   

```
mysql> SELECT COUNT(*) as repetitions, last_name, first_name
    -> FROM person_tbl
    -> GROUP BY last_name, first_name
    -> HAVING repetitions > 1;

``` 

该查询返回表 person_tbl 中所有的重复记录。一般来说，要想确认重复记录，需要采取以下步骤：   

- 确定可能产生重复记录的列。  
- 在列选择列表中显示所有列，利用 COUNT(*) 。  
- 利用 GROUP BY 子句列出列。
- 加入 HAVING 子句排除唯一值。需要让组计数大于1。  

## 从查询结果中消除重复记录  

使用DISTINCT 和 SELECT 语句来查找表中的重复记录。  

```
mysql> SELECT DISTINCT last_name, first_name
    -> FROM person_tbl
    -> ORDER BY last_name;

```  

另一种办法是添加 GROUP BY 子句，命名选择的列。消除重复记录并只选择指定列中的唯一值组合。   

```
mysql> SELECT last_name, first_name
    -> FROM person_tbl
    -> GROUP BY (last_name, first_name);

```

## 使用表替换去除重复记录  

下面这种技巧也可以消除表中存在的所有重复记录。  


```
mysql> CREATE TABLE tmp SELECT last_name, first_name, sex
    ->                  FROM person_tbl;
    ->                  GROUP BY (last_name, first_name);
mysql> DROP TABLE person_tbl;
mysql> ALTER TABLE tmp RENAME TO person_tbl;

```   

为表加入 INDEX 或 PRIMARY KEY 。即使该表已经存在，你也可以利用这种技巧消除重复记录，这种做法将来也依然保险。


```
mysql> ALTER IGNORE TABLE person_tbl
    -> ADD PRIMARY KEY (last_name, first_name);


```



