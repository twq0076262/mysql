# MySQL 排序结果

利用 SQL 的 **SELECT** 命令可以获取 MySQL 表中的数据。选择行时，如果不指定结果排序方式，MySQL 服务器所返回结果是没有一定的顺序的。指定想要排序的列，通过添加 ORDER BY 子句，就可以对结果集进行排序。

## 语法格式   

利用 SQL 的 SELECT 命令，配合 ORDER BY 子句，对 MySQL 表中的数据进行排序：  

```
SELECT field1, field2,...fieldN table_name1, table_name2...
ORDER BY field1, [field2...] [ASC [DESC]]

``` 


- 可以对列出的任何字段的返回结果进行排序。

- 可以对多个字段的返回结果进行排序。

- 可以使用关键字 ASC 或 DESC ，以升降序对结果进行排序。默认是采用升序排序。

- 通常可使用 WHERE...LIKE 子句设置条件。  




## 在命令行中使用 ORDER BY 子句  

我们将使用 SQL 的 SELECT 命令与 ORDER BY 子句，从 MySQL 表 tutorials_tbl 中获取数据。   

### 范例  

下面这个范例将采用升序的方式对返回结果进行排序。  

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT * from tutorials_tbl ORDER BY tutorial_author ASC
+-------------+----------------+-----------------+-----------------+
| tutorial_id | tutorial_title | tutorial_author | submission_date |
+-------------+----------------+-----------------+-----------------+
|           2 | Learn MySQL    | Abdul S         | 2007-05-24      |
|           1 | Learn PHP      | John Poul       | 2007-05-24      |
|           3 | JAVA Tutorial  | Sanjay          | 2007-05-06      |
+-------------+----------------+-----------------+-----------------+
3 rows in set (0.42 sec)

mysql>

```


如上所示，作者名称按照升序排列出来。   

## 在 PHP 脚本中使用 ORDER BY 子句  

除了在命令行中使用外，我们也可以在 PHP 函数 `mysql_query()` 中使用 ORDER BY 子句，两种情况下的语法都是相同的。先用 `mysql_query()` 执行 SQL 命令，然后再用 PHP 函数  `mysql_fetch_array()` 获取所有选定的数据。      


### 范例   

下面这个范例将按升序排列教程作者名称（`tutorial_author`）。  

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
$sql = 'SELECT tutorial_id, tutorial_title, 
               tutorial_author, submission_date
        FROM tutorials_tbl
        ORDER BY  tutorial_author DESC';

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not get data: ' . mysql_error());
}
while($row = mysql_fetch_array($retval, MYSQL_ASSOC))
{
    echo "Tutorial ID :{$row['tutorial_id']}  <br> ".
         "Title: {$row['tutorial_title']} <br> ".
         "Author: {$row['tutorial_author']} <br> ".
         "Submission Date : {$row['submission_date']} <br> ".
         "--------------------------------<br>";
} 
echo "Fetched data successfully\n";
mysql_close($conn);
?>
```   









