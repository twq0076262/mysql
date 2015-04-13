MySQL 可以很好地适用于多种编程语言，比如PERL、C、C++、JAVA，以及 PHP。由于可以开发 Web 应用程序，PHP 是其中最流行的一门语言。  

本教程讲解重点在于PHP 环境中使用 MySQL。如果你对使用 PERL 来操作 MySQL 有兴趣，可以参看这个教程：**PERL 与 MySQL 教程**   

PHP 提供了多种能够访问 MySQL 数据库并且操纵数据记录的函数。这些函数的调用方式就跟其他 PHP 函数一样。   

PHP 中用于操作 MySQL 的函数一般都采取如下的格式：  

`mysql_function(value,value,...);`  

函数名称的第二部分是函数所专有的，通常是一个描述函数行为的词。下面是教程中将会用到的两个函数：  

```
mysqli_connect($connect);
mysqli_query($connect,"SQL statement");

```  


下面这个例子展示的是PHP调用MySQL函数的常见语法格式：  


```
<html>
<head>
<title>PHP with MySQL</title>
</head>
<body>
<?php
   $retval = mysql_function(value, [value,...]);
   if( !$retval )
   {
       die ( "Error: a related error message" );
   }
   // Otherwise MySQL  or PHP Statements
?>
</body>
</html>

```    

 

从下一节开始，我们将介绍与 PHP 相关的 MySQL 功能。   