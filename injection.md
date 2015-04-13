如果通过网页接收用户输入，而后再把这些数据插入到数据库中，那么你可能就会碰到 SQL 注入式攻击。本节简要介绍如何防范这种攻击，确保脚本和 MySQL 语句的安全性。       

注入式攻击往往发生在要求用户输入时，比如说要求他们输入自己的名字，但是他们却输入了一段 MySQL 语句，不知不觉地运行在数据库上。     

永远不要相信用户所提供的数据，只有在验证无误后，才能去处理数据。通常，利用模式匹配来实现。在下面这个范例中，username（用户名）被限定为字母数字混合编制的字符串，再加上下划线，长度限定为8~20个字符之间。当然，可以按需要修改这些规范。   

```
if (preg_match("/^\w{8,20}$/", $_GET['username'], $matches))
{
   $result = mysql_query("SELECT * FROM users 
                          WHERE username=$matches[0]");
}
 else 
{
   echo "username not accepted";
}

```

为了暴露问题所在，请考虑下面这段代码：   

```
// 本应该的输入
$name = "Qadir'; DELETE FROM users;";
mysql_query("SELECT * FROM users WHERE name='{$name}'");

```

函数调用原本会从 users 表中获取一个记录。name 列与用户所指定的名字所匹配。在一般情况下，$name 会包含字母数字混合编制的字符，或许还包含空格，such as the string ilia. 但这里，为 $name 添加了一个全新的查询，数据库调用就变成了灾难：注入的 DELETE 查询会删除 users 表中所有的记录。   

幸运的是，如果使用 MySQL，`mysql_query()` 函数不允许堆叠查询，或在一个函数调用中执行多个查询。如果尝试使用堆叠查询，则调用会失败。  

然而，有些 PHP 数据库扩展，比如 SQLite 或 PostgreSQL，却能很好地执行堆叠查询，能够执行一个字符串中所提供的所有查询，从而造成严重的安全隐患。   




## 防止 SQL 注入式攻击    

使用 PERL 或 PHP 这样的脚本语言，可以很巧妙地处理转义字符。MySQL 针对 PHP 的扩展也提供了 `mysql_real_escape_string()` ，可以将输入的字符转义为MySQL所特有的字符。   


```
if (get_magic_quotes_gpc()) 
{
  $name = stripslashes($name);
}
$name = mysql_real_escape_string($name);
mysql_query("SELECT * FROM users WHERE name='{$name}'");

```



## LIKE 窘境  

为了解决 LIKE 困境，常用的转义机制必须将	用户所输入的 `%` 和 `_` 字符转义为字面值。使用 `addcslashes()` 能为你指定一个转义字符范围。     

```
$sub = addcslashes(mysql_real_escape_string("%something_"), "%_");
// $sub == \%something\_
mysql_query("SELECT * FROM messages WHERE subject LIKE '{$sub}%'");
``` 




