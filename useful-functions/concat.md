# MySQL CONCAT 函数

**CONCAT** 函数用于将两个字符串合并为一个字符串。如下例所示：  

```
mysql> SELECT CONCAT('FIRST ', 'SECOND');
+----------------------------+
| CONCAT('FIRST ', 'SECOND') |
+----------------------------+
| FIRST SECOND               |
+----------------------------+
1 row in set (0.00 sec)

```
以下面这个表 **employee_tbl** 为例：

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

如果需要将id、name以及work_date这三个字段值合并起来，可以使用如下命令：  


```
mysql> SELECT CONCAT(id, name, work_date)
    -> FROM employee_tbl;
+-----------------------------+
| CONCAT(id, name, work_date) |
+-----------------------------+
| 1John2007-01-24             |
| 2Ram2007-05-27              |
| 3Jack2007-05-06             |
| 3Jack2007-04-06             |
| 4Jill2007-04-06             |
| 5Zara2007-06-06             |
| 5Zara2007-02-06             |
+-----------------------------+
7 rows in set (0.00 sec)
```


