前面已经介绍了如何利用 SQL 的 **SELECT** 命令配合 **WHERE** 子句来获取 MySQL 表中的数据，但假如尝试给出一个条件，将字段或列值与 NULL 比对，则会出现异常。   

为了处理这种情况，MySQL 提供了三种运算符：   

- **IS NULL**：如果列值为 NULL，则该运算符返回 true。     
- **IS NOT NULL**：如果列值不为NULL，则该运算符返回 true。  
- **<=>**：该运算符用于两个值的对比，当两个值相等时（即使这两个值都为 NULL 时，这一点与 `=` 运算符不同）返回 true。  

包含 NULL 的条件都是比较特殊的。不能在列中使用 = NULL 或 ! = NULL 来寻找 NULL 值。这样的比对通常都是失败的，因为不可能得知这样的比对是否为真。即使 NULL = NULL 失败。   

要想确定列是否为 NULL，要使用 IS NULL 或 IS NOT NULL。   

## 在命令行中使用 NULL 值   

假设数据库 TUTORIALS 中包含一张叫做 **tcount_tbl** 的表，这张表包含两列 **tutorial_author** 与 **tutorial_count**，则 tutorial_count 中出现的 NULL 值代表该字段值未知。     

### 范例  

请看下面这个范例：   

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> create table tcount_tbl
    -> (
    -> tutorial_author varchar(40) NOT NULL,
    -> tutorial_count  INT
    -> );
Query OK, 0 rows affected (0.05 sec)
mysql> INSERT INTO tcount_tbl
    -> (tutorial_author, tutorial_count) values ('mahran', 20);
mysql> INSERT INTO tcount_tbl
    -> (tutorial_author, tutorial_count) values ('mahnaz', NULL);
mysql> INSERT INTO tcount_tbl
    -> (tutorial_author, tutorial_count) values ('Jen', NULL);
mysql> INSERT INTO tcount_tbl
    -> (tutorial_author, tutorial_count) values ('Gill', 20);

mysql> SELECT * from tcount_tbl;
+-----------------+----------------+
| tutorial_author | tutorial_count |
+-----------------+----------------+
| mahran          |             20 |
| mahnaz          |           NULL |
| Jen             |           NULL |
| Gill            |             20 |
+-----------------+----------------+
4 rows in set (0.00 sec)

mysql>

```   

下面，你会发现 = 和 != 并不适用于 NULL 值。   

```
mysql> SELECT * FROM tcount_tbl WHERE tutorial_count = NULL;
Empty set (0.00 sec)
mysql> SELECT * FROM tcount_tbl WHERE tutorial_count != NULL;
Empty set (0.01 sec)
```

所以，要想确定 tutorial_count 列中到底何值为 NULL，何值不为 NULL，查询应该这样写：   

```
mysql> SELECT * FROM tcount_tbl 
    -> WHERE tutorial_count IS NULL;
+-----------------+----------------+
| tutorial_author | tutorial_count |
+-----------------+----------------+
| mahnaz          |           NULL |
| Jen             |           NULL |
+-----------------+----------------+
2 rows in set (0.00 sec)
mysql> SELECT * from tcount_tbl 
    -> WHERE tutorial_count IS NOT NULL;
+-----------------+----------------+
| tutorial_author | tutorial_count |
+-----------------+----------------+
| mahran          |             20 |
| Gill            |             20 |
+-----------------+----------------+
2 rows in set (0.00 sec)

```  

## 在 PHP 脚本中处理 NULL 值   

可以使用 `if...else` 条件语句来准备一个基于 NULL 值的查询。  

### 范例  

下面这个例子获取外部的 tutorial_count，并将其与表中的值进行比对。  


```
<?php
$dbhost = 'localhost:3036';
$dbuser = 'root';
$dbpass = 'rootpassword';
$conn = mysql_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
  die('Could not connect: ' . mysql_error());
}
if( isset($tutorial_count ))
{
   $sql = 'SELECT tutorial_author, tutorial_count
           FROM  tcount_tbl
           WHERE tutorial_count = $tutorial_count';
}
else
{
   $sql = 'SELECT tutorial_author, tutorial_count
           FROM  tcount_tbl
           WHERE tutorial_count IS $tutorial_count';
}

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not get data: ' . mysql_error());
}
while($row = mysql_fetch_array($retval, MYSQL_ASSOC))
{
    echo "Author:{$row['tutorial_author']}  <br> ".
         "Count: {$row['tutorial_count']} <br> ".
         "--------------------------------<br>";
} 
echo "Fetched data successfully\n";
mysql_close($conn);
?>
```  


