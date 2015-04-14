# MySQL 插入查询

要想在 MySQL 表中插入数据，需要使用 **INSERT INTO** 这个 SQL 命令。既可以使用mysql> 提示符方式，也可以使用 PHP 等脚本来完成。  

## 语法格式 

利用 INSERT INTO 命令为表插入数据的一般语法如下所示：  

```
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );

``` 

要想插入字符串类型的数据，需要把值用双引号或单引号包括起来，比如：`"value"`。   

## 从命令提示符中插入数据  


我们将使用 INSERT INTO 命令为表 tutorials_tbl 插入数据。     

### 范例  

在下面的范例中，我们将为表 `tutorials_tbl` 创建3条记录。   

```
root@host# mysql -u root -p password;
Enter password:*******
mysql> use TUTORIALS;
Database changed
mysql> INSERT INTO tutorials_tbl 
     ->(tutorial_title, tutorial_author, submission_date)
     ->VALUES
     ->("Learn PHP", "John Poul", NOW());
Query OK, 1 row affected (0.01 sec)
mysql> INSERT INTO tutorials_tbl
     ->(tutorial_title, tutorial_author, submission_date)
     ->VALUES
     ->("Learn MySQL", "Abdul S", NOW());
Query OK, 1 row affected (0.01 sec)
mysql> INSERT INTO tutorials_tbl
     ->(tutorial_title, tutorial_author, submission_date)
     ->VALUES
     ->("JAVA Tutorial", "Sanjay", '2007-05-06');
Query OK, 1 row affected (0.01 sec)
mysql>

``` 



> **注意**：代码中的箭头符号（`->`）不属于 SQL 命令。它们只是用来表示换行，如果我们在每行命令末尾不添加分号（`;`），按下回车键时，MySQL 命令提示符就会自动创建出这个符号。   


在上面的范例中，我们没有提供 tutorial_id，因为在创建表时，已为该字段提供了 AUTO_INCREMENT 选项。因此 MySQL 会自动知道插入 ID。`NOW()` 是一个能够返回当前日期与时间的 MySQL 函数。   

## 利用 PHP 脚本插入数据 

同样，也可以在 PHP 的 **mysql_query()**函数中使用 SQL 命令 INSERT INTO 为 MySQL 表插入数据。   

### 范例  

在下面这个范例中，从用户那里接收3个参数，然后将这些参数插入到 MySQL 表中。     


  
 
```
	<html>
	<head>
	<title>Add New Record in MySQL Database</title>
	</head>
	<body>
	<?php
	if(isset($_POST['add']))
	{
	$dbhost = 'localhost:3036';
	$dbuser = 'root';
	$dbpass = 'rootpassword';
	$conn = mysql_connect($dbhost, $dbuser, $dbpass);
	if(! $conn )
	{
  		die('Could not connect: ' . mysql_error());
	}

	if(! get_magic_quotes_gpc() )
	{
   	$tutorial_title = addslashes ($_POST['tutorial_title']);
   	$tutorial_author = addslashes ($_POST['tutorial_author']);
	}
	else
	{
   	$tutorial_title = $_POST['tutorial_title'];
   	$tutorial_author = $_POST['tutorial_author'];
	}
	$submission_date = $_POST['submission_date'];

	$sql = "INSERT INTO tutorials_tbl ".
   	    "(tutorial_title,tutorial_author, submission_date) ".
     	  "VALUES ".
       	"('$tutorial_title','$tutorial_author','$submission_date')";
	mysql_select_db('TUTORIALS');
	$retval = mysql_query( $sql, $conn );
	if(! $retval )
	{
  		die('Could not enter data: ' . mysql_error());
	}
	echo "Entered data successfully\n";
	mysql_close($conn);
	}
		else
	{
	?>
	<form method="post" action="<?php $_PHP_SELF ?>">
	<table width="600" border="0" cellspacing="1" cellpadding="2">
	<tr>
	<td width="250">Tutorial Title</td>
	<td>
	<input name="tutorial_title" type="text" id="tutorial_title">
	</td>
	</tr>
	<tr>
	<td width="250">Tutorial Author</td>
	<td>
	<input name="tutorial_author" type="text" id="tutorial_author">
	</td>
	</tr>
	<tr>
	<td width="250">Submission Date [ yyyy-mm-dd ]</td>
	<td>
	<input name="submission_date" type="text" id="submission_date">
	</td>
	</tr>
	<tr>
	<td width="250"> </td>
	<td> </td>
	</tr>
	<tr>
	<td width="250"> </td>
	<td>
	<input name="add" type="submit" id="add" value="Add Tutorial">
	</td>
	</tr>
	</table>
	</form>
	<?php
	}
	?>
	</body>
	</html>
```





在输入数据时，使用函数 **get_magic_quotes_gpc()** 检查当前是否配置了魔术引号。如果函数返回 false，则使用 **addslashes()** 在引号前添加反斜杠。    


另外，还可以针对输入数据进行多种验证，确保数据的合法性，并对其采取正确行为。   


  

