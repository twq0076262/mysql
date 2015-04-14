# MySQL 数据导出

将表中数据导出为一个文本文件，最简单的方法是用 SELECT...INTO OUTFILE 语句，它会将查询结果直接导出为服务器主机上的一个文件。   

## 利用 SELECT...INTO OUTFILE 语句组合导出数据  

该语句组合的语法为：使用正常的 SELECT 语句，后跟 INTO OUTFILE，最后加上要导出的文件名。默认的输出格式和 LOAD DATA 一样，因此下列语句会将表 tutorials_tbl 导出为 /tmp/tutorials.txt，其中的数据以制表符分隔开，以换行符作为每行的终止符。

```
mysql> SELECT * FROM tutorials_tbl 
    -> INTO OUTFILE '/tmp/tutorials.txt';

``` 

你可以通过一些选项来改变输出格式，来指定如何以引用并限定列与记录。下面这个例子将表 tutorials_tbl 以逗号分隔各值，以 CRLF（回车换行符）来作为行的终止符：    

```
mysql> SELECT * FROM passwd INTO OUTFILE '/tmp/tutorials.txt'
    -> FIELDS TERMINATED BY ',' ENCLOSED BY '"'
    -> LINES TERMINATED BY '\r\n';

```

**SELECT ... INTO OUTFILE** 具有下列特点：   

- 输出文件直接由 MySQL 服务器创建，因此文件名应该指明其在服务器主机上的保存位置。该语句没有 LOCAL 版，这一点跟 LOAD DATA 不同。   
- 必须拥有 MySQL 的 FILE 权限，才能执行 SELECT ... INTO OUTFILE。   
- 输出文件不能是已有文件。这一特点保证了 MySQL 不会覆盖掉一些可能是非常重要的文件。   
- 你必须有服务器主机的登录账号，或者能够利用其它方式获取主机文件，否则 SELECT ... INTO OUTFILE 对你来说没有任何用处。  
- 在 UNIX 系统下，创建的文件是全局可读的，但可写权限却属于 MySQL 服务器。这意味着虽然你可以读取文件，但可能无法删除它。  

## 将表导出为原始数据   

`mysqldump` 程序用于复制或备份表与数据库。它能把表输出为一个原始数据文件，或者是一个能重建表中记录的 INSERT 语句集合。

要想把表转储为一个数据文件，必须指定一个 `--tab` 选项，用它来指明 MySQL 服务器写入文件的目录。   

例如，把数据库 TUTORIALS 中的表 tutorials_tbl 转储为 /tmp 中的一个文件，需要使用如下命令：    

```
$ mysqldump -u root -p --no-create-info \
            --tab=/tmp TUTORIALS tutorials_tbl
password ******

``` 

## 将表内容或定义以 SQL 格式导出  

以 SQL 格式将表导出为文件，使用类似下列命令：  

```
$ mysqldump -u root -p TUTORIALS tutorials_tbl > dump.txt
password ******

```  

这样创建的文件将包含如下内容：   

```
-- MySQL dump 8.23
--
-- Host: localhost    Database: TUTORIALS
---------------------------------------------------------
-- Server version       3.23.58

--
-- Table structure for table `tutorials_tbl`
--

CREATE TABLE tutorials_tbl (
  tutorial_id int(11) NOT NULL auto_increment,
  tutorial_title varchar(100) NOT NULL default '',
  tutorial_author varchar(40) NOT NULL default '',
  submission_date date default NULL,
  PRIMARY KEY  (tutorial_id),
  UNIQUE KEY AUTHOR_INDEX (tutorial_author)
) TYPE=MyISAM;

--
-- Dumping data for table `tutorials_tbl`
--

INSERT INTO tutorials_tbl 
       VALUES (1,'Learn PHP','John Poul','2007-05-24');
INSERT INTO tutorials_tbl 
       VALUES (2,'Learn MySQL','Abdul S','2007-05-24');
INSERT INTO tutorials_tbl 
       VALUES (3,'JAVA Tutorial','Sanjay','2007-05-06');

``` 

转储多张表，按照数据库命名》》。转储整个数据库，不需要命名数据库中的任何表：   

```
$ mysqldump -u root -p TUTORIALS > database_dump.txt
password ******

```

备份主机上的所有数据库，使用如下命令：  

```
$ mysqldump -u root -p --all-databases > database_dump.txt
password ******

``` 

自MySQL 3.23.12版本开始，可以使用 `--all-databases` 选项。   

这种方法可以实现数据库备份。   

## 将一台主机上的表或数据库复制到另一台主机上  

如果想把一台 MySQL 服务器上的表或数据库复制到另一台主机上，可以使用 mysqldump 程序，加上数据库名称和表名称。   

在源主机上运行以下命令，它会将整个数据库都转储到 dump.txt 文件中。   

```
$ mysqldump -u root -p database_name table_name > dump.txt
password *****

```  

如前所述，你可以将整个数据库都复制下来，无需使用任何具体的表名称。   

接下来，在另一台主机上ftp dump.txt 文件，并运行如下命令。在运行这行命令之前，先要确保已经在目标服务器上创建了 database_name。  

```
$ mysql -u root -p database_name < dump.txt
password *****

```

在主机间复制数据库也可以使用另一种方法，它的优点就是无需使用中介文件。将 mysqldump的输出结果直接通过网络传到远端的 MySQL 服务器上。如果你能从源数据库所在的主机上连接到两个服务器上，使用如下命令（一定要确保你能访问两台服务器）：   

```
$ mysqldump -u root -p database_name \
       | mysql -h other-host.com database_name

```

以上命令的 mysqldump 部分会连接本地服务器，将转储结果写入管线。剩下的命令连接到另一台主机的远端服务器上，读取管线上传来的转储结果，将每个语句送到目的主机所在的服务器上。   





