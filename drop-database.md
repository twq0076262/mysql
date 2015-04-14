# MySQL 终止数据库

## 利用 mysqladmin 删除 MySQL 数据库  


同上一节的情况完全一样，创建或删除 MySQL 数据库需要特殊的权限。假如有了 root 用户权限，那就可以用 **mysqladmin** 二进制命令来随意创建数据库了。      


删除数据库要非常谨慎，因为这样做会丢失数据库中所保存的全部数据。  

在下面这个范例中，删除了上一节所创建的数据库。     

```
[root@host]# mysqladmin -u root -p drop TUTORIALS
Enter password:******
  
```

这时，系统会显示一条警示消息，询问是否确定要删除数据库。  

```
Dropping the database is potentially a very bad thing to do.
Any data stored in the database will be destroyed.

Do you really want to drop the 'TUTORIALS' database [y/N] y
Database "TUTORIALS" dropped

```  

## 使用 PHP 脚本删除数据库  

PHP 使用 **mysql_query** 函数来创建或删除 MySQL 数据库。该函数包含两个参数，如果成功执行操作，返回 TRUE，否则返回 FALSE。      

## 语法格式   

`bool mysql_query( sql, connection );`  

## 范例   

下面这个范例展示了如何删除一个数据库。     

```
<html>
<head>
<title>Deleting MySQL Database</title>
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
$sql = 'DROP DATABASE TUTORIALS';
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not delete database: ' . mysql_error());
}
echo "Database TUTORIALS deleted successfully\n";
mysql_close($conn);
?>
</body>
</html>

```

> **警告**：在利用 PHP 脚本删除数据库时，它不会提供任何确认提示，因此一定要小心。
