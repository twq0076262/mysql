MySQL 可以采用2种简单的方法将之前备份文件中的数据加载进 MySQL 数据库。   



## 利用 LOAD DATA 导入数据   

MySQL 利用 LOAD DATA 语句作为批量数据加载器。下面这个范例将从当前目录中读取 dump.txt 文件，然后把它加载进当前数据库的表 mytbl 中。  

`mysql> LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl;
`   

- 如果不写 LOCAL 关键字，MySQL 会从服务器主机文件系统的根目录开始，以完整指明文件位置的绝对路径名方式开始查找数据文件。MySQL 会从给定位置读取文件。   
- 默认情况下，LOAD DATA 假定数据文件中每行都由换行符所终止，每行的数据值由制表符所分隔开。   
- 为了明确指定文件格式，使用 FIELDS 子句来描述行内字段特征， LINES 子句指定行末尾序列。下例中的 LOAD DATA 语句表明，数据文件中的值由冒号（`:`）分隔，每行由换行符及回车符所终止。   


```
mysql> LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl
  -> FIELDS TERMINATED BY ':'
  -> LINES TERMINATED BY '\r\n';

```

- LOAD DATA 假定数据文件中的列的顺序与表中列的顺序相同。如果不为真，可以指定一个列表来指示数据文件中具体表列的加载方式。假如表有3个列：a、b和c，但数据文件中对应的是列b、c与a，则可以这样加载。        


```
mysql> LOAD DATA LOCAL INFILE 'dump.txt' 
    -> INTO TABLE mytbl (b, c, a);

```   

## 利用mysqlimport 导入数据    

MySQL 还包含一个工具程序：`mysqlimport`。它相当于 LOAD DATA 的一个封装器，因而你可以直接从命令行中加载输入文件。   

将 dump.txt 中的数据加载进表 mytbl，可以在 UNIX 系统的命令行中使用以下命令：   

```
$ mysqlimport -u root -p --local database_name dump.txt
password *****

``` 

如果使用mysqlimport，命令行选项就会提供格式说明符。mysqlimport 命令作用相当于前面的两个LOAD DATA 语句，语法如下：


```
$ mysqlimport -u root -p --local --fields-terminated-by=":" \
   --lines-terminated-by="\r\n"  database_name dump.txt
password *****

```     




对于 mysqlimport 来说，你怎么指定选项的次序并不重要，只要把它们写在数据库名称前面就可以了。   

**mysqlimport** 语句使用 --columns 选项来指定列次序。  

```
$ mysqlimport -u root -p --local --columns=b,c,a \
    database_name dump.txt
password *****

```



## 处理引号与特殊字符    


The FIELDS clause can specify other format options besides TERMINATED BY. By default, LOAD DATA assumes that values are unquoted and interprets the backslash (\) as an escape character for special characters. To indicate the value quoting character explicitly, use ENCLOSED BY; MySQL will strip that character from the ends of data values during input processing. To change the default escape character, use ESCAPED BY.  


FIELDS 子句能指定除了 TERMINATED BY 之外的其他格式选项。默认情况下，LOAD DATA 会假定值不加引号，并把反斜杠（`\`）解释为表示特殊意义的转义字符。要想明确指出》，使用 ENCLOSED BY 即可。MySQL 会在处理输入时将该字符从数据值末尾清除掉。改变默认的转义字符，使用 ESCAPED BY。  

When you specify ENCLOSED BY to indicate that quote characters should be stripped from data values, it's possible to include the quote character literally within data values by doubling it or by preceding it with the escape character. For example, if the quote and escape characters are " and \, the input value "a""b\"c" will be interpreted as a"b"c.


在指定 ENCLOSED BY 来表示引号字符应该从数据值末尾清除时，有可能在数据值中包含引号字符，或在其之前添加转义字符。比如，如果引号和转义字符是`"`和`\`，那么输入值`"a""b\"c"`就会被解读为`a"b"c`。  


对于 mysqlimport 而言，相应的指定引号和转义值的命令行选项是`--fields-enclosed-by`和`--fields-escaped-by`。







