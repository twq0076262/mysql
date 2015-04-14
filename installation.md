# MySQL 安装

## 下载 MySQL  

MySQL 的全部下载链接都在这个页面：[MySQL 下载](http://www.mysql.com/downloads/)。选择所需的 *MySQL Community Server* 版本号，并且尽可能准确地选择所需平台。    

## 在 Linux/Unix 上安装 MySQL   

在 Linux 系统上安装 MySQL，建议采用 RPM 形式进行安装。MySQL AB 在其网站上提供了以下几种 RPM 文件包：    

- **MySQL** MySQL 数据库服务器，用于管理数据库与表，控制用户访问，以及处理 SQL 查询。  
- **MySQL-client** MySQL 客户端程序，实现用户与服务器的连接与交互功能。   
- **MySQL-devel** 编译使用 MySQL 的其他程序的过程中会用到的一些库及头文件。      
- **MySQL-shared** MySQL 客户端的共享库。     
- **MySQL-bench**  用于MySQL 服务器的基准测试与性能测试工具。  

这里列出的 MySQL RPM 都是基于 Linux 的 SuSE 分发版系统构建的，但它们一般也能轻松地运行在其他 Linux 变种系统上。    

接着按照以下步骤完成安装：  

- 使用 **root** 用户登录系统。      
- 切换到含有 RPM 文件包的目录中。     
- 执行下面命令，安装 MySQL 服务器。记住，用你自己的 RPM 文件名替换命令中斜体标识的文件名：   
  
	`[root@host]# rpm -i MySQL-5.0.9-0.i386.rpm`  
	  
	上面的命令安装 MySQL 服务器，创建了一个 MySQL 用户，进行了必要的配置，并开始自动启动 MySQL 服务器。  
	
	在 /usr/bin 与 /usr/sbin 可找到 MySQL 所有的相关库。创建的所有的表和数据库都在 /var/lib/mysql 目录下。  
	
- 安装剩下的RPM，可参照下列命令（但建议采用这种方式）进行：    
	
	```  
	[root@host]# rpm -i MySQL-client-5.0.9-0.i386.rpm  
	[root@host]# rpm -i MySQL-devel-5.0.9-0.i386.rpm  
	[root@host]# rpm -i MySQL-shared-5.0.9-0.i386.rpm  
	[root@host]# rpm -i MySQL-bench-5.0.9-0.i386.rpm    
	```

## 在 Windows 下安装 MySQL   

现在，Windows 系统下的 MySQL 默认安装方式都比过去容易多了，因为已经利用安装程序将所需的 MySQL 内容精心打包起来。只需下载安装程序包，随便将它解压缩在某个目录，然后运行 setup.exe 就可以了。  

默认的安装程序 setup.exe 能帮你打理琐碎的安装过程，同时默认安装在 C:\mysql 目录下。  

首次测试服务器，可以采用命令行方式。找到 mysqld 服务器的位置（可能位于 C:\mysql\bin），输入如下命令：  

`mysqld.exe --console`    

> **注意**：如果是 NT 系统，就不能使用 mysqld.exe 了，必须使用 mysqld-nt.exe。   

 


不出意外的话，你就会看到一些关于启动和 InnoDB 的信息。如果没有出现这类信息，那么可能是因为你的许可权限有问题。确保所有用户（可能是 mysql）都能访问存储数据的目录。  

MySQL 不会自动将其自身添加到开始菜单中，而且目前也没有一些比较好的能够用来停止服务的GUI。因此，假如你喜欢通过双击 mysqld 可执行文件来启动服务器，那么当要关闭服务器时，记得要手动借助 mysqladmin、任务列表、任务管理器或者 Windows 的一些专用方法来进行。   

## MySQL 安装验证  

成功安装完 MySQL 后，就会初始化基表，启动服务器。可以通过一些简单的测试来验证安装是否一切正常。   

### 使用 mysqladmin 工具来获取服务器状态  

使用 **mysqladmin** 工具来查看服务器版本。在Linux下，这一工具位于 /usr/bin；Windows下则在C:\mysql\bin。  

`[root@host]# mysqladmin --version`  

在 Linux 下，上述命令可能会产生如下结果。根据你安装的 Linux 版本的差异，结果也可能会有些许不同。   

`mysqladmin  Ver 8.23 Distrib 5.0.9-0, for redhat-linux-gnu on i386`  

如果没有显示类似这样的信息，则说明安装可能出现了一些问题，需要借助一些帮助来修补它们。  


### 使用MySQL客户端来执行简单的SQL命令  

你可以通过在MySQL客户端上使用 **mysql** 命令去连接 MySQL 服务器。这时，不需要输入任何密码，因为默认情况下会设置为空白。   


所以只需输入如下命令即可：     

`[root@host]# mysql`    

系统应该显示出 mysql> 提示符，这就表明你已经连接上了 MySQL 服务器，可以在提示符后输入一些 SQL 命令了，如下所示：   

```  
mysql> SHOW DATABASES;  
+----------+  
| Database |  
+----------+  
| mysql    |   
| test     |  
+----------+  
2 rows in set (0.13 sec)

```     


## 安装后的一些步骤   

对于根用户，MySQL初始是不需要密码的。一旦成功安装好数据库和客户端后，你就需要设置一个根用户密码，如下所示：   

`[root@host]# mysqladmin -u root password "new_password";`  

接着连接MySQL服务器，就会要求你输入密码了：   

```  
[root@host]# mysql -u root -p
Enter password:*******
```  

对于UNIX用户来说，同样也必须把MySQL目录放入PATH环境变量中，这样在使用命令行客户端时，就不必每次手动输入路径全称了。对于bash shell 来说，应该这样设置：   

`export PATH=$PATH:/usr/bin:/usr/sbin`  

## 启动时运行 MySQL  

如果想让 MySQL 在系统启动时自动运行，则可以 /etc/rc.local 文件中加入下列项：   

`/etc/init.d/mysqld start`  

另外，在 etc/init.d/ 目录中必须存在 mysqld 工具。




	  



