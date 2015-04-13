删除已有的 MySQL 表是很容易的，但你要非常小心，因为删除了表，就无法恢复数据了。  

## 语法  

删除 MySQL 表的常用 SQL 命令为：  
 
`DROP TABLE table_name ;`  



## 通过命令行方式删除表  

只需在命令行中使用 **DROP TABLE** 这个SQL命令即可。   

### 范例  

在以下范例中，删除了表`tutorials_tbl`。   

```
root@host# mysql -u root -p
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> DROP TABLE tutorials_tbl
Query OK, 0 rows affected (0.8 sec)
mysql>

```

## 利用 PHP 脚本删除表  

要想利用 PHP 脚本删除数据库中的表，需要使用函数 **mysql_query()**。将正确的 SQL 命令传入该函数的第二个参数中，就能将表删除。  


### 范例   


```
<html>
<head>
<title>Creating MySQL Tables</title>
</head>
<body>
<?php
$dbhost = 'localhost:3036';
$dbuser = 'root';
$dbpass = 'rootpassword';
$conn = mysql_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
  die('Could not connect: ' . mysql_error());
}
echo 'Connected successfully<br />';
$sql = "DROP TABLE tutorials_tbl";
mysql_select_db( 'TUTORIALS' );
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not delete table: ' . mysql_error());
}
echo "Table deleted successfully\n";
mysql_close($conn);
?>
</body>
</html>
``` 



