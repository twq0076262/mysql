# MySQL MIN 函数

**MIN** 函数用于寻找记录集中拥有最小值的记录。  

为了理解 MIN 函数，还是以 employee_tbl 表为例，它的所有记录如下所示：   

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

假设需要根据上表获取 daily_typing_pages 的最小值，只需使用如下命令即可：   

```
mysql> SELECT MIN(daily_typing_pages)
    -> FROM employee_tbl;
+-------------------------+
| MIN(daily_typing_pages) |
+-------------------------+
|                     100 |
+-------------------------+
1 row in set (0.00 sec)


```   


也可以使用 **GROUP BY** 子句找到每一名字下的最小值记录。  

```
mysql>SELECT id, name, MIN(daily_typing_pages)
    -> FROM employee_tbl GROUP BY name;
+------+------+-------------------------+
| id   | name | MIN(daily_typing_pages) |
+------+------+-------------------------+
|    3 | Jack |                     100 |
|    4 | Jill |                     220 |
|    1 | John |                     250 |
|    2 | Ram  |                     220 |
|    5 | Zara |                     300 |
+------+------+-------------------------+
5 rows in set (0.00 sec)

```   


还可以组合使用	MIN 与 MAX 函数找出最小值，如下所示：   

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


