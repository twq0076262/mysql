# MySQL Where Clause

前面介绍了利用 **SELECT** 命令从表中获取数据。利用一种叫做 **WHERE** 子句的条件子句可以过滤结果。使用 WHERE 子句可以制定选择规则，从表中选择我们所需的记录。   


## 语法格式  

利用 SELECT 命令与 WHERE 子句从表中获取数据的一般语法格式如下所示：       

```
SELECT field1, field2,...fieldN table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....

```  

- 可以使用逗号分隔一个或多个表，从而在使用 WHERE 子句时，包含多个条件。但是 WHERE 子句并非 SELECT 命令的一个可选部分。   
- 可以在使用 WHERE 子句时指定任何条件。  
- 可以通过 **AND** 或 **OR** 运算符来指定一个或多个条件。  
- WHERE 子句可以和 DELETE 或 UPDATE 命令一起使用，同样是用于指定条件。  

**WHERE** 子句的运作方式就像编程语言中的 if 条件语句一样。它会将给定值与MySQL表中的字段值进行对比，如果两值相等，则返回MySQL表中字段值的所在的行。  

下面这张表列出了 **WHERE** 子句中使用的一些运算符。   

假设字段 A 保存 10 这个值，字段 B 保存着 20，那么：   


|运算符|说明|范例|
|---|---|---|
|`=`|检查两个操作数是否相等。如果相等，则条件为真。|`(A = B)`非真| 
|`!=`|检查两个操作数是否相等。如果不相等，则条件为真。|`(A != B)`为真|
|`>`|检查左侧操作数是否大于右边的操作数。如果大于，则条件为真。|`(A > B)`非真|  
|`<`|检查左侧操作数是否小于右侧操作数。如果小于，则条件为真。|`(A < B)`为真|  
|`>=`|检查左侧操作数是否大于或等于右侧操作数。如果是，则条件为真。|`(A >= B)`非真|
|`<=`|检查左侧操作数是否小于或等于右侧操作数。如果是，则条件为真|`(A <= B)`为真|  



**WHERE** 子句可以非常方便地获取表中选定的行，尤其与 MySQL 的 Join 一起使用时。Join 稍后将择章另述。   

另外，为了加快搜索，往往使用主键搜索记录。   

如果表中记录并不匹配给定条件，查询不会返回任何数据。     

## 采用命令行方式获取数据      

使用 SQL 的 SELECT 命令与 WHERE 子句获取 表 tutorials_tbl 中的选定数据。   


### 范例  

以下范例将返回表 tutorials_tbl 中作者名称（author name）为 **Sanjay** 的所有记录。   

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT * from tutorials_tbl WHERE tutorial_author='Sanjay';
+-------------+----------------+-----------------+-----------------+
| tutorial_id | tutorial_title | tutorial_author | submission_date |
+-------------+----------------+-----------------+-----------------+
|           3 | JAVA Tutorial  | Sanjay          | 2007-05-21      |
+-------------+----------------+-----------------+-----------------+
1 rows in set (0.01 sec)

mysql>
  

```


除非对字符串采用 **LIKE** 比对，否则默认比对是不区分大小写的。要想让搜索对大小写敏感，可以如下例一般，使用 **BINARY** 关键字。     

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> SELECT * from tutorials_tbl \
          WHERE BINARY tutorial_author='sanjay';
Empty set (0.02 sec)

mysql>

```


## 使用 PHP 脚本来获取数据   

要想获取表中数据，也可以使用 PHP 函数 **mysql_query()**，同时配合使用 SQL 的 SELECT 命令与 WHERE 子句。先用 `mysql_query()` 执行 SQL 命令，再用另一 PHP 函数 **mysql_fetch_array()** 来获取所有选定数据。`mysql_fetch_array()` 会将行以关联数组、数值数组，或者两种兼有》》的形式返回。如果未选定任何数据，则该函数返回 FALSE。  

### 范例  

以下范例将返回表 tutorials_tbl 中作者名为 Sanjay 的所有记录。  

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
        WHERE tutorial_author="Sanjay"';

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








