# MySQL 选择查询

SQL 的 **SELECT** 命令用于从 MySQL 数据库中获取数据。可以在mysql> 提示符中使用这一命令，也可以利用 PHP 等脚本来完成。   

## 语法格式   

利用 SELECT 命令从 MySQL 表中获取数据的一般语法格式如下：  


```  
SELECT field1, field2,...fieldN table_name1, table_name2...  
[WHERE Clause]  
[OFFSET M ][LIMIT N]  
```    

- 可以通过逗号分隔一个或多个表，利用 WHERE 子句包含进多种条件，但 WHERE 子句并不是 SELECT 命令的可选部分。   
- 可以在一个 SELECT 命令中获取一个或多个字段。  
- 可以用星型符号（`*`）代替字段。这时，SELECT 将返回所有字段。  
- 可以使用 WHERE 子句指定任何条件。  
- 在 SELECT 将要返回记录的位置处，使用 **OFFSET** 可以指定一个偏移。默认偏移为0。  
- 可以使用 **LIMIT** 属性来限制返回记录的数量。   


## 利用命令行方式获取数据  

使用 SELECT 命令从表 tutorials_tbl 中获取数据。  

### 范例   

下面这个范例将返回表 tutorials_tbl 中的所有记录。  

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT * from tutorials_tbl 
+-------------+----------------+-----------------+-----------------+
| tutorial_id | tutorial_title | tutorial_author | submission_date |
+-------------+----------------+-----------------+-----------------+
|           1 | Learn PHP      | John Poul       | 2007-05-21      |
|           2 | Learn MySQL    | Abdul S         | 2007-05-21      |
|           3 | JAVA Tutorial  | Sanjay          | 2007-05-21      |
+-------------+----------------+-----------------+-----------------+
3 rows in set (0.01 sec)

mysql>
 
```
  
  
## 使用 PHP 脚本获取数据   

同样，也可以在 **mysql_query()** 函数中使用 SQL 命令 SELECT。该函数用于执行 SQL 命令。随后另一个 PHP 函数 **mysql_fetch_array()** 会获取所有选定的数据，该函数会将行以关联数组或数值数组返回，或者还可能同时返回以上两种形式。如果再也没有行，则该函数返回 FALSE。  


下面通过一个简单的范例来了解如何获取 tutorials_tbl 表中的记录。  

### 范例  

下面这个范例会获取表 tutorials_tbl 中的所有记录。

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
        FROM tutorials_tbl';

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


行的内容被赋给变量 `$row`，随后输出行内所包含的值。  

> **注意**：一定要记住，在把一个数组值直接插入到字符串中时，一定要加花括号（`{`与`}`）。   


在上面的例子中，常量 `MYSQL_ASSOC` 被用作 PHP 函数 `mysql_fetch_array()` 的第二个参数，因此才会将行按照关联数组的形式返回。利用关联数组，我们可以使用字段的名字来访问字段，而不需要用到索引。     

PHP 还提供了另一个叫做 `mysql_fetch_assoc()` 的函数，也会将行以关联数组的形式返回。  

### 范例  

在下面的范例中，利用 `mysql_fetch_assoc()` 函数来显示 tutorials_tbl 表中的所有记录。  


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
        FROM tutorials_tbl';

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not get data: ' . mysql_error());
}
while($row = mysql_fetch_assoc($retval))
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


你可以使用常量 **MYSQL_NUM** 作为 `mysql_fetch_array()` 函数的第二个参数。这能让函数返回一个带有数字索引的数组。   


### 范例   

在下面的范例中，使用参数 MYSQL_NUM 来显示表 tutorials_tbl 中的所有记录。      

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
        FROM tutorials_tbl';

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not get data: ' . mysql_error());
}
while($row = mysql_fetch_array($retval, MYSQL_NUM))
{
    echo "Tutorial ID :{$row[0]}  <br> ".
         "Title: {$row[1]} <br> ".
         "Author: {$row[2]} <br> ".
         "Submission Date : {$row[3]} <br> ".
         "--------------------------------<br>";
}
echo "Fetched data successfully\n";
mysql_close($conn);
?>
  
```

以上三个范例都会产生同样的结果。    

## 释放内存   

在每个 SELECT 语句末尾释放游标内存是一个非常好的做法。使用 PHP 函数 **mysql_free_result()** 就可以实现这一点，如下例所示。  


### 范例   

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
        FROM tutorials_tbl';

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not get data: ' . mysql_error());
}
while($row = mysql_fetch_array($retval, MYSQL_NUM))
{
    echo "Tutorial ID :{$row[0]}  <br> ".
         "Title: {$row[1]} <br> ".
         "Author: {$row[2]} <br> ".
         "Submission Date : {$row[3]} <br> ".
         "--------------------------------<br>";
}
mysql_free_result($retval);
echo "Fetched data successfully\n";
mysql_close($conn);
?>

```

在获取数据时，还可以用更复杂的SQL语句。步骤和上面介绍的一样。   


