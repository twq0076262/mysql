数据库索引是一种能够改善表操作速度的数据结构。索引可以通过一个或多个列来创建，它可以提高随机查询的速度，并在检索记录时实现高效排序。  

在创建索引时，需要考虑哪些列会用于 SQL 查询，然后为这些列创建一个或多个索引。  

事实上，索引也是一种表，保存着主键或索引字段，以及一个能将每个记录指向实际表的指针。   


数据库用户是看不到索引的，它们只是用来加速查询的。数据库搜索引擎使用索引来快速定位记录。  

INSERT 与 UPDATE 语句在拥有索引的表中执行会花费更多的时间，而 SELECT 语句却会执行得更快。这是因为，在进行插入或更新时，数据库也需要插入或更新索引值。   

## 简单而唯一的索引  

可以为表创建唯一索引。唯一索引要求任意两行的索引值不能相同。下面展示的就是在表中创建索引的语法格式：   

```
CREATE UNIQUE INDEX index_name
ON table_name ( column1, column2,...);

```  

也可以使用一或多个列来创建索引。比如说，表 tutorials_tbl 中，使用 tutorial_author 来创建索引。   

```
CREATE UNIQUE INDEX AUTHOR_INDEX
ON tutorials_tbl (tutorial_author)

```


还可以为表创建简单索引，只需要在查询时不带 UNIQUE 关键字，就可创建简单索引。简单索引允许在表中复制值。   

如果打算按照降序在列中索引数值，可以在列名后添加保留字 DESC。   

```
mysql> CREATE UNIQUE INDEX AUTHOR_INDEX
ON tutorials_tbl (tutorial_author DESC)

```  


## 添加与删除 INDEX 的ALTER 命令   

为表添加索引，可以采用4种语句。

- `ALTER TABLE tbl_name ADD PRIMARY KEY (column_list)` 该语句添加一个主键。意味着索引值必须是唯一的，不能为 NULL。   
- `ALTER TABLE tbl_name ADD UNIQUE index_name (column_list)` 该语句为必须唯一的值（除了 NULL 值之外，NULL 值可以多次出现）创建索引。   
- `ALTER TABLE tbl_name ADD INDEX index_name (column_list)` 语句为可能多次出现的值创建一般索引。  
- `ALTER TABLE tbl_name ADD FULLTEXT index_name (column_list)` 语句创建专用于文本搜索的 FULLTEXT 索引。   


下面这个范例将为现有表添加索引。    


`mysql> ALTER TABLE testalter_tbl ADD INDEX (c);`   


可以使用 DROP 子句以及 ALTER 命令删除索引，通过下面这个范例来删除之前创建的索引。   


`mysql> ALTER TABLE testalter_tbl DROP INDEX (c);`


## 利用 ALTER 命令来添加与删除主键   

添加主键也采用类似方式，但要保证主键一定在列上，是 NOT NULL。   



下面这个范例将在现有表中添加主键，先使列为 NOT NULL，然后再将其作为主键。  

```
mysql> ALTER TABLE testalter_tbl MODIFY i INT NOT NULL;
mysql> ALTER TABLE testalter_tbl ADD PRIMARY KEY (i);

```  

同样，也可以使用 ALTER 命令删除一个主键。   

`mysql> ALTER TABLE testalter_tbl DROP PRIMARY KEY;`
 

如果要删除非主键的索引，则必须指定索引名称。   

## 显示索引信息  

使用 SHOW INDEX 命令可以列出表的所有索引。以垂直格式输出（标识为 `\G`）会比较便于查看，可避免单行内容过长。语法格式如下：   

```
mysql> SHOW INDEX FROM table_name\G
........

```  





