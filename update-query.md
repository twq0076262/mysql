有时，MySQL 表中的已有数据可能需要修改，可以使用 SQL 的 **UPDATE** 命令来处理。它会修改MySQL表中任何字段的值。   

## 语法  

利用 UPDATE 命令修改 MySQL 表中数据的一般语法格式如下：   

```
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]

```  

- 可以一起更新一个或多个字段。   
- 可以使用 WHERE 子句指定任意条件。   
- 可以每次仅更新一张表中的数值。  

在需要更新表中选定行时，WHERE 子句是一个非常有用的工具。  

## 采用命令行方式更新数据   

下面我们将使用 SQL 的UPDATE 命令，再配合 WHERE 子句，来更新 MySQL 表 tutorials_tbl 中的选定数据。  

### 范例  

下面这个范例将为一个 tutorial_id 为 3 的记录添加一个新的 **tutorials_title** 字段。     

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> UPDATE tutorials_tbl 
    -> SET tutorial_title='Learning JAVA' 
    -> WHERE tutorial_id=3;
Query OK, 1 row affected (0.04 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql>

```  

## 使用 PHP 脚本来更新数据  

同样，也可以在 PHP 的 **mysql_query()** 函数中使用 SQL 的 UPDATE 命令和（ 或不用） WHERE 子句。该函数执行 SQL 命令的方式与 mysql> 命令行方式相同。

### 范例  

下面这个范例将为一个 tutorial_id 为 3 的记录添加一个新的 **tutorials_title** 字段。     


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
$sql = 'UPDATE tutorials_tbl
        SET tutorial_title="Learning JAVA"
        WHERE tutorial_id=3';

mysql_select_db('TUTORIALS');
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not update data: ' . mysql_error());
}
echo "Updated data successfully\n";
mysql_close($conn);
?>
```
