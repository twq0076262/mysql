序列就是按照要求的顺序产生的一组整数，比如1、2、3……这样。数据库中经常会用到序列，因为很多应用程序都会需要让表中的每行的值唯一，而使用序列就可以轻松地解决这个问题。下面就来介绍 MySQL 中的序列使用。   

## 使用 AUTO_INCREMENT 列  

在MySQL中，序列最简单的用法就是将一列定义为 AUTO_INCREMENT ，然后让 MySQL 来处理剩下的任务。  

### 范例  

在下面这个范例中，先创建一个表，然后插入一些行。不需要提供记录ID，因为这是由 MySQL 自动增加的。   

```
mysql> CREATE TABLE insect
    -> (
    -> id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    -> PRIMARY KEY (id),
    -> name VARCHAR(30) NOT NULL, # type of insect
    -> date DATE NOT NULL, # date collected
    -> origin VARCHAR(30) NOT NULL # where collected
);
Query OK, 0 rows affected (0.02 sec)
mysql> INSERT INTO insect (id,name,date,origin) VALUES
    -> (NULL,'housefly','2001-09-10','kitchen'),
    -> (NULL,'millipede','2001-09-10','driveway'),
    -> (NULL,'grasshopper','2001-09-10','front yard');
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0
mysql> SELECT * FROM insect ORDER BY id;
+----+-------------+------------+------------+
| id | name        | date       | origin     |
+----+-------------+------------+------------+
|  1 | housefly    | 2001-09-10 | kitchen    |
|  2 | millipede   | 2001-09-10 | driveway   |
|  3 | grasshopper | 2001-09-10 | front yard |
+----+-------------+------------+------------+
3 rows in set (0.00 sec)

```

## 获取 AUTO_INCREMENT 的值  

`LAST_INSERT_ID()` 是一个 SQL 函数，所以可以把它用在任何能够理解 SQL 语句的客户端中。另外，PERL 和 PHP 还提供了一些专有的函数来获取最后记录的自动增加值。   

### PERL 范例  

使用 mysql_insertid 属性来获取查询所生成的 AUTO_INCREMENT 值。根据查询方式，该属性可通过数据库句柄或语句句柄来访问。下面这个范例是从数据库句柄来引用该属性的。    

```
$dbh->do ("INSERT INTO insect (name,date,origin)
VALUES('moth','2001-09-14','windowsill')");
my $seq = $dbh->{mysql_insertid};

```   

### PHP 范例  

当查询生成了 AUTO_INCREMENT 值后，通过调用 `mysql_insert_id()` 函数来获取该值。  

```
mysql_query ("INSERT INTO insect (name,date,origin)
VALUES('moth','2001-09-14','windowsill')", $conn_id);
$seq = mysql_insert_id ($conn_id);

```  

## 对已有序列进行重新编号  

假如从表中删除了许多记录，必须对记录再次排序。这时可以使用一个小技巧来解决，但要记住当表还连接着其他表时，一定要非常小心。   

如果一定要对 AUTO_INCREMENT 列进行重新排序，那么正确的方式是将该列从表中删除，然后再添加它。下面这个范例中就用了这个技巧，在 insect 表中对 id 值重新排序。   

```
mysql> ALTER TABLE insect DROP id;
mysql> ALTER TABLE insect
    -> ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT FIRST,
    -> ADD PRIMARY KEY (id);

```  


## 以特定值作为序列初始值 

MySQL 默认以 1 作为序列初始值，但你也可以在创建表时指定其他的数字。下面的范例以 100 作为序列初始值。  

```
mysql> CREATE TABLE insect
    -> (
    -> id INT UNSIGNED NOT NULL AUTO_INCREMENT = 100,
    -> PRIMARY KEY (id),
    -> name VARCHAR(30) NOT NULL, # type of insect
    -> date DATE NOT NULL, # date collected
    -> origin VARCHAR(30) NOT NULL # where collected
);

``` 

另外一种方法是，先创建表，然后再使用 ALTER TABLE 来改变初始序列值。   

`mysql> ALTER TABLE t AUTO_INCREMENT = 100;`


