# MySQL 临时表

当需要保存临时数据时，使用临时表就会很方便。需要注意的一点是：在当前用户会话终止时，临时表会被清除。  

MySQL 是从 3.23 版开始引入临时表这一概念。如果使用 3.23 之前的 MySQL版本，则无法使用临时表，但可以使用堆表（HEAP table）。   

如上所述，临时表只能在会话生存期内存在。如果在 PHP 脚本中运行代码，那么当脚本结束执行时，就会自动清除临时表。如果通过 MySQL 客户端程序连接 MySQL 数据库服务器，那么临时表就会一直存在，除非关闭客户端或者手动清除该表。   

## 范例   

下面范例将展示临时表的用法。同样的代码也可通过 **mysql_query()** 用于 PHP 脚本中。  


```
mysql> CREATE TEMPORARY TABLE SalesSummary (
    -> product_name VARCHAR(50) NOT NULL
    -> , total_sales DECIMAL(12,2) NOT NULL DEFAULT 0.00
    -> , avg_unit_price DECIMAL(7,2) NOT NULL DEFAULT 0.00
    -> , total_units_sold INT UNSIGNED NOT NULL DEFAULT 0
);
Query OK, 0 rows affected (0.00 sec)

mysql> INSERT INTO SalesSummary
    -> (product_name, total_sales, avg_unit_price, total_units_sold)
    -> VALUES
    -> ('cucumber', 100.25, 90, 2);

mysql> SELECT * FROM SalesSummary;
+--------------+-------------+----------------+------------------+
| product_name | total_sales | avg_unit_price | total_units_sold |
+--------------+-------------+----------------+------------------+
| cucumber     |      100.25 |          90.00 |                2 |
+--------------+-------------+----------------+------------------+
1 row in set (0.00 sec)

```

利用 SHOW TABLES 命令显示表时，临时表不会出现在结果列表中。如果退出 MySQL 会话，就会执行 SELECT 命令，那么数据库中将没有任何数据，甚至临时表也不存在了。


## 删除临时表    

默认情况下，当与数据库的连接终止时，临时表就不再存在。不过如果想在数据库处于连接时就删除它们，可以用 DROP TABLE 命令来删除。   

下面就是一个删除临时表的范例：   

```
mysql> CREATE TEMPORARY TABLE SalesSummary (
    -> product_name VARCHAR(50) NOT NULL
    -> , total_sales DECIMAL(12,2) NOT NULL DEFAULT 0.00
    -> , avg_unit_price DECIMAL(7,2) NOT NULL DEFAULT 0.00
    -> , total_units_sold INT UNSIGNED NOT NULL DEFAULT 0
);
Query OK, 0 rows affected (0.00 sec)

mysql> INSERT INTO SalesSummary
    -> (product_name, total_sales, avg_unit_price, total_units_sold)
    -> VALUES
    -> ('cucumber', 100.25, 90, 2);

mysql> SELECT * FROM SalesSummary;
+--------------+-------------+----------------+------------------+
| product_name | total_sales | avg_unit_price | total_units_sold |
+--------------+-------------+----------------+------------------+
| cucumber     |      100.25 |          90.00 |                2 |
+--------------+-------------+----------------+------------------+
1 row in set (0.00 sec)
mysql> DROP TABLE SalesSummary;
mysql>  SELECT * FROM SalesSummary;
ERROR 1146: Table 'TUTORIALS.SalesSummary' doesn't exist

```


  