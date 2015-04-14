# MySQL 选择数据库

一旦连接上了 MySQL 服务器，就需要选择一个具体的用来运行的数据库。这是因为，有可能会有多个数据库挂接在MySQL服务器上。     

## 利用命令行方式选择 MySQL 数据库   
 
通过 mysql> 提示符来选择数据库是一种非常简单的方法。可以使用 SQL 命令 **use** 来选择某个数据库。   

## 范例    

下面这个范例展示了如何选择一个名为 **TUTORIALS** 的数据库。   

```
[root@host]# mysql -u root -p
Enter password:******
mysql> use TUTORIALS;
Database changed
mysql> 

```  

这样就能选择TUTORIALS数据库，所有后续操作都将在TUTORIALS数据库上进行。   

> **注意**：所有的数据库名称、表名、表字段名都是对大小写敏感的，因此使用SQL命令时，必须要使用正确的名称。   

## 使用PHP脚本选择MySQL数据库   

PHP 通过 **mysql_select_db** 函数来选择数据库。如果成功完成操作，返回 TRUE，否则返回 FALSE。   

## 语法格式    

`bool mysql_select_db( db_name, connection );`


|参数|说明|
|---|---|
|`db_name`|必需参数。要选择的 MySQL 数据库名称。|
|`connection`|可选参数。如未指定，则将使用`mysql_connect`最后打开的一个连接。|  

## 范例   

下面这个范例展示如何选择数据库。    

```
<html>
<head>
<title>Selecting MySQL Database</title>
</head>
<body>
<?php
$dbhost = 'localhost:3036';
$dbuser = 'guest';
$dbpass = 'guest123';
$conn = mysql_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
  die('Could not connect: ' . mysql_error());
}
echo 'Connected successfully';
mysql_select_db( 'TUTORIALS' );
mysql_close($conn);
?>
</body>
</html>
  
```








