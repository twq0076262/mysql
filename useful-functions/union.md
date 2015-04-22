# MySQL UNION 关键字

可以使用 **UNION** 从一些表中相继选择行，或从》》   

MySQL 是从 4.0 版本起开始加入的UNION 这个关键字，下面就来介绍一下它的用法。   

假设有3张表，它们分别列出了潜在顾客、实际顾客，以及你进货的供货商。现在你想建立一个邮件列表，将这3张表中的名字与地址合并起来。使用 UNION 就能办到这一点。假设这3张表内容如下：  

```
mysql> SELECT * FROM prospect;
+---------+-------+------------------------+
| fname   | lname | addr                   |
+---------+-------+------------------------+
| Peter   | Jones | 482 Rush St., Apt. 402 |
| Bernice | Smith | 916 Maple Dr.          |
+---------+-------+------------------------+
mysql> SELECT * FROM customer;
+-----------+------------+---------------------+
| last_name | first_name | address             |
+-----------+------------+---------------------+
| Peterson  | Grace      | 16055 Seminole Ave. |
| Smith     | Bernice    | 916 Maple Dr.       |
| Brown     | Walter     | 8602 1st St.        |
+-----------+------------+---------------------+
mysql> SELECT * FROM vendor;
+-------------------+---------------------+
| company           | street              |
+-------------------+---------------------+
| ReddyParts, Inc.  | 38 Industrial Blvd. |
| Parts-to-go, Ltd. | 213B Commerce Park. |
+-------------------+---------------------+

```  

3张表的列名称不同也没有关系。下面这个查询展示了如何一起选择3张表里的名字和地址。   

```
mysql> SELECT fname, lname, addr FROM prospect
-> UNION
-> SELECT first_name, last_name, address FROM customer
-> UNION
-> SELECT company, '', street FROM vendor;
+-------------------+----------+------------------------+
| fname             | lname    | addr                   |
+-------------------+----------+------------------------+
| Peter             | Jones    | 482 Rush St., Apt. 402 |
| Bernice           | Smith    | 916 Maple Dr.          |
| Grace             | Peterson | 16055 Seminole Ave.    |
| Walter            | Brown    | 8602 1st St.           |
| ReddyParts, Inc.  |          | 38 Industrial Blvd.    |
| Parts-to-go, Ltd. |          | 213B Commerce Park.    |
+-------------------+----------+------------------------+

```

如果想选择所有记录，包括那些重复记录，可以使用 UNION ALL 命令。

```
mysql> SELECT fname, lname, addr FROM prospect
-> UNION ALL
-> SELECT first_name, last_name, address FROM customer
-> UNION
-> SELECT company, '', street FROM vendor;
+-------------------+----------+------------------------+
| fname             | lname    | addr                   |
+-------------------+----------+------------------------+
| Peter             | Jones    | 482 Rush St., Apt. 402 |
| Bernice           | Smith    | 916 Maple Dr.          |
| Grace             | Peterson | 16055 Seminole Ave.    |
| Bernice           | Smith    | 916 Maple Dr.          |
| Walter            | Brown    | 8602 1st St.           |
| ReddyParts, Inc.  |          | 38 Industrial Blvd.    |
| Parts-to-go, Ltd. |          | 213B Commerce Park.    |
+-------------------+----------+------------------------+

```