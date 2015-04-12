# 6. 连接 MySQL 服务器 

可以在命令行方式下使用 **mysql** 命令建立 MySQL数据库。   

## 范例：  

下面这个例子显示如何采用命令行方式连接 MySQL 服务器：     

```
[root@host]# mysql -u root -p
Enter password:******

```

上述命令将显示 mysql> 命令提示符。在该命令提示符后面，可以执行任何 SQL 命令。下面就是上述命令的显示结果：   

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2854760 to server version: 5.0.9

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

```


在上面这个例子中，使用 **root** 作为用户（你也可以使用其他用户）。任何用户都能执行 root 用户所能执行的全部 SQL 操作。   

无论何时，只要在 mysql> 提示符下输入 `exit`，就能随时中断与 MySQL 的连接。   

```  
mysql> exit   
Bye  
```   

## 使用 PHP 脚本连接 MySQL    

通过 PHP 的 `mysql_connect()` 函数，可以开启数据库连接。该函数有5个参数。当成功连接后，该函数返回一个 MySQL 连接标识；如连接失败，则返回FALSE。   

### 语法格式  

`connection mysql_connect(server,user,passwd,new_link,client_flag);`   
   

|参数|说明|   
|---|----|
|`server`|可选参数。运行数据库服务器的主机名。如未指定，则默认值 **localhost:3036**。|  
|`user`|可选参数。访问数据库的用户名。如未指定，则默认值为拥有服务器进程的用户名称。|  
|`passwd`|可选参数。用户访问数据库所用密码。如未指定，则默认没有密码。|  
|`new_link`|可选参数。如果利用同样的参数第二次调用`mysql_connect()`，则不会建立新的连接，而是返回已打开连接的标识。|  
|`client_flags`|可选参数。是由下列常量组合而成：<br><br><li>MYSQL_CLIENT_SSL——使用 SSL 加密。<li>MYSQL_CLIENT_COMPRESS——使用数据压缩协议。<li>MYSQL_CLIENT_IGNORE_SPACE——允许函数名后出现空格。<li>MYSQL_CLIENT_INTERACTIVE——关闭连接之前所空闲等候的交互超时秒数。|


通过 PHP 的 **mysql_close()** 函数，随时可以中断与 MySQL 数据库的连接。该函数只有一个参数，是一个由 **mysql_connect()**函数所返回的连接。    


### 语法格式     

`bool mysql_close ( resource $link_identifier );`  

如果某个资源未被指定，则最后打开的数据库就会被关闭。如果成功中断连接，该函数返回 true，否则返回 false。   

## 范例   

下面通过一个具体的范例来实际了解如何连接 MySQL 服务器。     

```
<html>
<head>
<title>Connecting MySQL Server</title>
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
   mysql_close($conn);
?>
</body>
</html>
  
```



