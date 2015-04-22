# MySQL COUNT 函数

**COUNT** 函数的用法很简单，就是为了统计记录数。SELECT 语句所返回的。  

为了理解这个函数，让我们再次搬出 **employee_tbl** 表，它的所有记录如下所示：  

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

假设要根据上表统计行的总数，当然可以这样做：  

```
mysql>SELECT COUNT(*) FROM employee_tbl ;
+----------+
| COUNT(*) |
+----------+
|        7 |
+----------+
1 row in set (0.01 sec)

```

同样，如果希望计算 Zara 的记录数，可以这样实现：   

```
mysql>SELECT COUNT(*) FROM employee_tbl
    -> WHERE name="Zara";
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
1 row in set (0.04 sec)


```   

> **注意**：由于 SQL 查询对大小写不敏感，所以在 WHERE 条件中，无论是写成 ZARA  还是 Zara，结果都是一样的。   


