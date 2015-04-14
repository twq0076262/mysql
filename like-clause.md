# MySQL Like Clause

前面几节讲解了如何利用 SQL 的 **SELECT** 命令来获取 MySQL 表中的数据，以及如何利用 **WHERE** 子句这种条件子句来选择所需的记录。  

当我们需要进行精确匹配时，可以在WHERE子句中加入等号（`=`），就像是 `if tutorial_author = 'Sanjay'` 这种 `if` 条件语句一样。但有时我们会想在所有的结果中过滤 tutorial_author 字段包含 "jay" 字符的结果。这时就应该利用 SQL 的 **LIKE** 子句搭配 WHERE 子句来解决。

如果 SQL 的 LIKE 子句带有 `%` 字符，则相当于 UNIX 中的元字符（`*`），在命令行中列出所有的文件或目录。   

如果 LIKE 子句不带 `%` 字符，则就相当于 WHERE 子句中带有等号的情况。   

## 语法格式  

使用 SQL 的 SELECT 命令，并配合 LIKE 子句，从 MySQL 表中获取数据的一般语法格式如下所示：  

```
SELECT field1, field2,...fieldN table_name1, table_name2...
WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue'

```   

- 可以使用 WHERE 子句来指定任何条件。  
- 可以搭配使用 LIKE 子句与 WHERE 子句。   
- LIKE 子句可以代替WHERE子句中的等号。  
- 当 LIKE 子句带有 百分号（`%`）时，会按照元字符搜索那样执行。  
- 使用 **AND** 或 **OR** 运算符，可以指定一个或多个条件。    
- WHERE...LIKE 子句组合还可以搭配 DELETE 或UPDATE 这样的 SQL 命令一起使用。其中，WHERE…LIKE 子句组合的作用同样是指定条件。  

## 在命令行中使用 LIKE 子句    

我们将使用 SQL 的SELECT 命令搭配WHERE...LIKE 子句组合，从 MySQL 的表 tutorials_tbl 中获取选定数据。  

### 范例  

下面这个范例将返回表 **tutorials_tbl** 中作者名结尾带有 **jay** 的所有记录。   

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT * from tutorials_tbl 
    -> WHERE tutorial_author LIKE '%jay';
+-------------+----------------+-----------------+-----------------+
| tutorial_id | tutorial_title | tutorial_author | submission_date |
+-------------+----------------+-----------------+-----------------+
|           3 | JAVA Tutorial  | Sanjay          | 2007-05-21      |
+-------------+----------------+-----------------+-----------------+
1 rows in set (0.01 sec)

mysql>

```   

## 在 PHP 脚本中使用 LIKE 子句  

在利用PHP 的 `mysql_query()` 函数过程中，我们可以照常使用 WHERE...LIKE 子句组合的语法。如果 WHERE...LIKE 子句组合和 SELECT 命令一起使用，那么先利用 `mysql_query()` 函数执行相关的 SQL 命令，然后再用另一个 PHP 函数 `mysql_fetch_array()` 获取所有的数据。     

但如果 WHERE...LIKE 子句组合是和 DELETE 或 UPDATE 命令一起使用的话，就不需要再调用 PHP 函数了。  

### 范例  

下面这个范例将返回表 **tutorials_tbl** 中所有作者名包含 **jay** 的记录。   


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
        WHERE tutorial_author LIKE "%jay%"';

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





