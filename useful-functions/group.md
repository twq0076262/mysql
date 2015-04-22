# MySQL Group By 子句

可以使用 **GROUP BY** 子句对列中的值进行分组。如果你愿意，还可以对列实施某种计算。可以对分组的列使用COUNT、SUM以及AVG等函数。

为了理解 GROUP BY 子句，考虑表 **employee_tbl**，它包含如下记录：  

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

现在，根据上面这张表，我们来计算一下每位员工的工作天数。    

如果像下面这样写 SQL 查询，那么将得到下列结果：    

```
mysql> SELECT COUNT(*) FROM employee_tbl;
+---------------------------+
| COUNT(*)                  |
+---------------------------+
| 7                         |
+---------------------------+

```  

但这并不符合预期，我们希望的是输出每位员工输入的页数。可以结合使用聚合函数与 GROUP BY 子句，如下所示：  

```
mysql> SELECT name, COUNT(*)
    -> FROM   employee_tbl 
    -> GROUP BY name;
+------+----------+
| name | COUNT(*) |
+------+----------+
| Jack |        2 |
| Jill |        1 |
| John |        1 |
| Ram  |        1 |
| Zara |        2 |
+------+----------+
5 rows in set (0.04 sec)

```   

以后，我们还将介绍更多 GROUP BY 与 SUM、AVG 等函数相结合的用法。