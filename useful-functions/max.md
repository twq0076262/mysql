# MySQL MAX 函数

**MAX** 函数就是用来寻找记录集中的最大值的。

为了理解这个函数，再次搬出 **employee_tbl** 表，其内容如下所示：   

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

假设要获取上表中 daily_typing_pages 的最大值，可以这样实现：   

``` 
mysql> SELECT MAX(daily_typing_pages)
    -> FROM employee_tbl;
+-------------------------+
| MAX(daily_typing_pages) |
+-------------------------+
|                     350 |
+-------------------------+
1 row in set (0.00 sec)
  
```
还可以结合利用 **GROUP BY** 子句，找出每个名字的最大值：
 
```  
mysql> SELECT id, name, MAX(daily_typing_pages)
    -> FROM employee_tbl GROUP BY name;
+------+------+-------------------------+
| id   | name | MAX(daily_typing_pages) |
+------+------+-------------------------+
|    3 | Jack |                     170 |
|    4 | Jill |                     220 |
|    1 | John |                     250 |
|    2 | Ram  |                     220 |
|    5 | Zara |                     350 |
+------+------+-------------------------+
5 rows in set (0.00 sec)

```
也可以组合使用 **MIN** 和 **MAX** 函数找出最小值，如下所示：  

```  
mysql> SELECT MIN(daily_typing_pages) least, MAX(daily_typing_pages) max
    -> FROM employee_tbl;
+-------+------+
| least | max  |
+-------+------+
|   100 |  350 |
+-------+------+
1 row in set (0.01 sec)
```