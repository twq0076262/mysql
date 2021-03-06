# MySQL BETWEEN 子句

**BETWEEN** 子句可以代替“大于等于XX，并且小于等于XX”这样的条件。   

为了理解 **BETWEEN** 子句，依旧来看 **employee_tbl** 这个例子，它的所有记录如下：  


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

假设要从上表中获取 daily_typing_pages 大于或等于170，小于或等于300的数据。可以利用 **>=**  与 **<=** 条件来实现。   


```
mysql>SELECT * FROM employee_tbl 
    ->WHERE daily_typing_pages >= 170 AND
    ->daily_typing_pages <= 300;
+------+------+------------+--------------------+
| id   | name | work_date  | daily_typing_pages |
+------+------+------------+--------------------+
|    1 | John | 2007-01-24 |                250 |
|    2 | Ram  | 2007-05-27 |                220 |
|    3 | Jack | 2007-05-06 |                170 |
|    4 | Jill | 2007-04-06 |                220 |
|    5 | Zara | 2007-06-06 |                300 |
+------+------+------------+--------------------+
5 rows in set (0.03 sec)

```  

用 **BETWEEN** 实现起来就简单多了，如下所示：   


```
mysql> SELECT * FROM employee_tbl 
    -> WHERE daily_typing_pages BETWEEN 170 AND 300; 
+------+------+------------+--------------------+
| id   | name | work_date  | daily_typing_pages |
+------+------+------------+--------------------+
|    1 | John | 2007-01-24 |                250 |
|    2 | Ram  | 2007-05-27 |                220 |
|    3 | Jack | 2007-05-06 |                170 |
|    4 | Jill | 2007-04-06 |                220 |
|    5 | Zara | 2007-06-06 |                300 |
+------+------+------------+--------------------+
5 rows in set (0.03 sec)
```