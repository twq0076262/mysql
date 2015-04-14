# MySQL 删除查询

如果想从 MySQL 表中删除记录，就要用到 SQL 命令 **DELETE FROM** 。可以在命令行中使用该命令，也可以在 PHP 脚本中使用它。   

## 语法格式  

下面是利用 DELETE 命令删除 MySQL 表中数据的一般语法格式：  

`DELETE FROM table_name [WHERE Clause]`  

- 如果未指定 WHERE 子句，将删除指定表中的所有记录。    
- 可以在 WHERE 子句中指定任意条件。  
- 可以一次删除一张表中的所有记录。


在删除表中选定的行时，WHERE 子句是非常有用的。  

## 采用命令行方式删除数据  

下面将利用 DELETE 命令配合 WHERE 子句来删除表 tutorials_tbl 中的选定数据。  

### 范例  

下例将删除表 tutorials_tbl 中字段 tutorials_id 为 3 的所有记录。  

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> DELETE FROM tutorials_tbl WHERE tutorial_id=3;
Query OK, 1 row affected (0.23 sec)

mysql>
  
```  

## 利用 PHP 脚本来删除数据  

可以使用 PHP 的 `mysql_query()` 函数，配合 SQL 的 DELETE 命令以及 WHERE 子句（也可以不用该子句）删除数据。`mysql_query()` 函数执行 SQL 命令的方式类似于上面讲到的命令行方式。     

### 范例  

下面这个范例将删除表 tutorials_tbl 中字段tutorial_id为3的记录。   


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
$sql = 'DELETE FROM tutorials_tbl
        WHERE tutorial_id=3';

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not delete data: ' . mysql_error());
}
echo "Deleted data successfully\n";
mysql_close($conn);
?>
```
 



