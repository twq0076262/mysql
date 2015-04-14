# MySQL Using Join

迄今为止，我们每次只能从一张表里获取数据。这足以应付简单的任务了，但大多数真实的 MySQL 应用场景却经常会需要通过一次查询，从多张表中获取数据。    

在一个 SQL 查询中使用多张表，联结（join）行为在 MySQL 数据库中指的就是将2张或更多的表合为一张表。    

你可以在 SELECT、UPDATE、DELETE语句中使用 JOIN 来联结 MySQL 表。下面还将介绍一个左联结（LEFT JOIN）的范例，了解一下它与 JOIN 的区别。     

## 在命令行中使用 JOIN 

假设数据库 TUTORIALS 中有两张表：**tcount_tbl** 和 **tutorials_tbl**。完整的代码清单如下所示。   

### 范例   

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT * FROM tcount_tbl;
+-----------------+----------------+
| tutorial_author | tutorial_count |
+-----------------+----------------+
| mahran          |             20 |
| mahnaz          |           NULL |
| Jen             |           NULL |
| Gill            |             20 |
| John Poul       |              1 |
| Sanjay          |              1 |
+-----------------+----------------+
6 rows in set (0.01 sec)
mysql> SELECT * from tutorials_tbl;
+-------------+----------------+-----------------+-----------------+
| tutorial_id | tutorial_title | tutorial_author | submission_date |
+-------------+----------------+-----------------+-----------------+
|           1 | Learn PHP      | John Poul       | 2007-05-24      |
|           2 | Learn MySQL    | Abdul S         | 2007-05-24      |
|           3 | JAVA Tutorial  | Sanjay          | 2007-05-06      |
+-------------+----------------+-----------------+-----------------+
3 rows in set (0.00 sec)
mysql>

```

上例通过一个 SQL 查询将两张表联结到一起。这次查询选择了表 **tutorials_tbl** 中所有的作者，然后获取表 **tcount_tbl** 中这些作者相应的教程数量。  

```
mysql> SELECT a.tutorial_id, a.tutorial_author, b.tutorial_count
    -> FROM tutorials_tbl a, tcount_tbl b
    -> WHERE a.tutorial_author = b.tutorial_author;
+-------------+-----------------+----------------+
| tutorial_id | tutorial_author | tutorial_count |
+-------------+-----------------+----------------+
|           1 | John Poul       |              1 |
|           3 | Sanjay          |              1 |
+-------------+-----------------+----------------+
2 rows in set (0.01 sec)
mysql>

```   


## 在 PHP 脚本中使用JOIN   

可以在 PHP 脚本中使用以前学到过的任何一种 SQL 查询。只需要将 SQL 查询传入 PHP 函数 `mysql_query()` 中，就能按照之前的方式获得结果。 

### 范例   

相关范例如下：   

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
$sql = 'SELECT a.tutorial_id, a.tutorial_author, b.tutorial_count
        FROM tutorials_tbl a, tcount_tbl b
        WHERE a.tutorial_author = b.tutorial_author';

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
         "Tutorial ID: {$row['tutorial_id']} <br> ".
         "--------------------------------<br>";
} 
echo "Fetched data successfully\n";
mysql_close($conn);
?>

```   

## MySQL的左联结（LEFT JOIN）  

MySQL 的左联结（LEFT JOIN）与简单使用 JOIN 的效果不同。左联结侧重考虑左侧的表。  

如果进行左联结，除了得到所有跟以上联结同样的匹配记录之外，还会得到左侧表中未曾匹配的记录，从而保证了（在该范例中）照顾到了每一位作者。      


### 范例   

下面这个范例可以帮我们更好地理解左联结。   

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT a.tutorial_id, a.tutorial_author, b.tutorial_count
    -> FROM tutorials_tbl a LEFT JOIN tcount_tbl b
    -> ON a.tutorial_author = b.tutorial_author;
+-------------+-----------------+----------------+
| tutorial_id | tutorial_author | tutorial_count |
+-------------+-----------------+----------------+
|           1 | John Poul       |              1 |
|           2 | Abdul S         |           NULL |
|           3 | Sanjay          |              1 |
+-------------+-----------------+----------------+
3 rows in set (0.02 sec)

```  

必须多加练习，才能熟悉 JOIN。这是 MySQL/SQL 中的一个比较复杂的概念，必须经过一番真实的案例磨炼才能真正地掌握它。

