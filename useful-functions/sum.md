# MySQL SUM 函数

**SUM** 函数用来在不同记录中计算某一字段的总和值。  

例如，在表 **employee_tbl** 中，所有记录如下：  

```  
mysql> SELECT * FROM employee_tbl;
+------+------+------------+--------------------+
| id   | name | work_date  | daily_typing_pages |
+------+------+------------+--------------------+
|    1 | John | 2007-01-24 |                250 |
|    2 | Ram  | 2007-05-27 |                220 |
|    3 | Jack | 2007-05-06 |                170 |
|    3 | Jack | 2007-04-06 |                100 |
|    4 | Jill | 2007-04-06 |                220 |
|    5 | Zara | 2007-06-06 |                300 |
|    5 | Zara | 2007-02-06 |                350 |
+------+------+------------+--------------------+
7 rows in set (0.00 sec)

```

如果想根据该表计算字段 dialy_typing_pages 的总值，可以使用如下命令：  

```  
mysql> SELECT SUM(daily_typing_pages)
    -> FROM employee_tbl;
+-------------------------+
| SUM(daily_typing_pages) |
+-------------------------+
|                    1610 |
+-------------------------+
1 row in set (0.00 sec)


```
   

还可以使用 **GROUP BY** 子句来计算多种记录集的平均值。下面这个范例将计算每个人的所有记录的总值，将得到每个人的平均输入页面。  

```  
mysql> SELECT name, SUM(daily_typing_pages)
    -> FROM employee_tbl GROUP BY name;
+------+-------------------------+
| name | SUM(daily_typing_pages) |
+------+-------------------------+
| Jack |                     270 |
| Jill |                     220 |
| John |                     250 |
| Ram  |                     220 |
| Zara |                     650 |
+------+-------------------------+
5 rows in set (0.17 sec) 

```
