
# 7. 创建 MySQL 数据库  


## 使用 mysqladmin 创建数据库  

创建或删除数据库需要拥有特殊的权限。假设你获得了root用户权限，那么利用 mysqladmin 二进制命令可以创建任何数据库。   
  
  
## 范例  

下面就来创建一个名叫 **TUTORIALS** 的数据库：  

```
[root@host]# mysqladmin -u root -p create TUTORIALS
Enter password:******
  
```  

通过上述命令，就创建好了一个名叫 **TUTORIALS** 的 MySQL 数据库。    

## 利用PHP脚本创建数据库  


PHP利用 **mysql_query** 函数来创建或删除 MySQL 数据库。该函数有2个参数，成功执行操作则返回TRUE，失败则返回FALSE。   

## 语法  

`bool mysql_query( sql, connection );`  

|参数|说明|  
|---|---|  
|`sql`|必需参数。创建或删除 MySQL 数据库所用的 SQL 命令。|  
|`connection`|可选参数。如未指定，将使用最后一个由 `mysql_connect` 打开的连接。|

## 范例  

通过下面这个范例来了解如何创建数据库。     

```
<html>
<head>
<title>Creating MySQL Database</title>
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
$sql = 'CREATE DATABASE TUTORIALS';
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not create database: ' . mysql_error());
}
echo "Database TUTORIALS created successfully\n";
mysql_close($conn);
?>
</body>
</html>  
```


