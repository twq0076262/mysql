# 11.创建 MySQL 表


创建表的命令需要：  

- 表名  
- 字段名  
- 每一字段的定义  

## 语法格式  

下面就是一种常见的用来创建 MySQL 表的 SQL 语法。  

`CREATE TABLE table_name (column_name column_type);`

然后在 **TUTORIALS** 数据库创建如下表：   

```
tutorials_tbl(
   tutorial_id INT NOT NULL AUTO_INCREMENT,
   tutorial_title VARCHAR(100) NOT NULL,
   tutorial_author VARCHAR(40) NOT NULL,
   submission_date DATE,
   PRIMARY KEY ( tutorial_id )
);

```   


这里需要解释的项目是：  


- 使用字段属性 **NOT NULL** 是因为我们不想让该字段为空值。所以如果用户尝试创建空值记录，MySQL 就会抛出一个错误。   
- 字段属性 **AUTO_INCREMENT** 告诉 MySQL 继续为 id 字段增加下一个可能的数值。  
- 关键字 **PRIMARY KEY** 会将一列定义为主键。也可以使用由逗号分隔的多个列来定义主键。  

## 通过命令行方式创建表   

通过命令行来创建 MySQL 表是非常简单的一种方式。使用 SQL命令 **CREATE TABLE** 即可创建一个表。    



### 范例  

在下面这个范例中，创建了表 **tutorials_tbl**。   

```
root@host# mysql -u root -p
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> CREATE TABLE tutorials_tbl(
   -> tutorial_id INT NOT NULL AUTO_INCREMENT,
   -> tutorial_title VARCHAR(100) NOT NULL,
   -> tutorial_author VARCHAR(40) NOT NULL,
   -> submission_date DATE,
   -> PRIMARY KEY ( tutorial_id )
   -> );
Query OK, 0 rows affected (0.16 sec)
mysql>

```   

> **注意**：只有在SQL命令末尾加上分号（`;`）才能终止这个命令。    

## 利用 PHP 脚本创建表  

在已有的数据库中创建新表，可以使用 PHP 的 **mysql_query()** 函数。利用正确的SQL命令为其传入第二个参数，就能创建出一张表。   



### 范例  

以下范例展示如何利用 PHP 脚本来创建表。    

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
$sql = "CREATE TABLE tutorials_tbl( ".
       "tutorial_id INT NOT NULL AUTO_INCREMENT, ".
       "tutorial_title VARCHAR(100) NOT NULL, ".
       "tutorial_author VARCHAR(40) NOT NULL, ".
       "submission_date DATE, ".
       "PRIMARY KEY ( tutorial_id )); ";
mysql_select_db( 'TUTORIALS' );
$retval = mysql_query( $sql, $conn );
if(! $retval )
{
  die('Could not create table: ' . mysql_error());
}
echo "Table created successfully\n";
mysql_close($conn);
?>
</body>
</html>
```





