MySQL可为你提供3类有价值的信息：  

- **查询结果信息**  受SELECT、UPDATE 或 DELETE 语句影响的记录数量。
- **表与数据库的信息**  表及数据库的相关信息。
- **MySQL 服务器的信息** 数据库服务器的状态以及数据库版本号等信息。

通过命令行方式可以轻松获取以上这些信息，但如果使用 PERL 或 PHP API，就需要显式地调用各种 API 来获取这些信息。下面将介绍具体做法。   


## 获取受查询影响的行数   

### PERL 范例   

在 DBI 脚本中，根据执行查询的方式，通过 do() 或 execute() 返回受查询影响的行数。  

```
# Method 1
# execute $query using do( )
my $count = $dbh->do ($query);
# report 0 rows if an error occurred
printf "%d rows were affected\n", (defined ($count) ? $count : 0);

# Method 2
# execute query using prepare( ) plus execute( )
my $sth = $dbh->prepare ($query);
my $count = $sth->execute ( );
printf "%d rows were affected\n", (defined ($count) ? $count : 0);

```   

### PHP 范例  

在PHP中，调用 `mysql_affected_rows()` 函数来查找查询所影响的行数。  

```
$result_id = mysql_query ($query, $conn_id);
# report 0 rows if the query failed
$count = ($result_id ? mysql_affected_rows ($conn_id) : 0);
print ("$count rows were affected\n");

```  

## 输出表与数据库的相关信息   

很容易就能输出数据库服务器上的数据库及表的相关信息，但如果没有足够权限，则可能所得结果为空。    

除了下面将要介绍的方法之外，还可以使用 SHOW TABLES 或 SHOW DATABASES 查询来获取表与数据库的相关信息，这一点对于 PHP 和 PERL 都是适用的。   

### PERL 范例   

```
# 获取当前数据库中的所有表  
my @tables = $dbh->tables ( );
foreach $table (@tables ){
   print "Table Name $table\n";
}

``` 

### PHP 范例    

```
<?php
$con = mysql_connect("localhost", "userid", "password");
if (!$con)
{
  die('Could not connect: ' . mysql_error());
}

$db_list = mysql_list_dbs($con);

while ($db = mysql_fetch_object($db_list))
{
  echo $db->Database . "<br />";
}
mysql_close($con);
?>

```

## 获取服务器元数据   

利用下面5种命令可以获取数据库服务器上的各种关键信息。它们既适用于命令行，也适用于 PHP 或 PERL 脚本。   

|命令|描述|
|---|---|
|`SELECT VERSION()`|表明服务器版本的字符串|
|`SELECT DATABASE()`|当前数据库名称（如果没有则为空值）|
|`SELECT USER()`|当前用户名|
|`SHOW STATUS`|服务器状态指示器|
|`SHOW VARIABLES`|服务器配置变量|  

