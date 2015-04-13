前面介绍过 MySQL 。MySQL 还支持另一种基于正则表达式的模式匹配操作，使用的运算符是 **REGEXP**。如果你学过 PHP 或 PERL，那么这就很好理解了，因为这里讲的这种匹配方式跟那些脚本语言中的正则表达式很相似。   


下面就是一个模式列表，其中结合使用了 **REGEXP** 运算符。  

|模式|模式匹配对象|
|---|---|  
|`^`|字符串的开始位置|
|`$`|字符串的结尾|
|`.`|单个字符|
|`[...]`|一对方括号之间的字符|
|`[^...]`|未在一对方括号之间的字符|
|`p1|p2|p3`|交替匹配模式1、模式2或模式3|  
|`*`|匹配前面元素的零个或多个实例|  
|`+`|匹配前面元素的一个或多个实例|
|`{n}`|匹配前面元素的n个实例|
|`{m,n}`|匹配前面元素的m~n个实例，m <= n|



## 范例   

根据以上这张列表，可以设计出能够满足各种要求的 SQL 查询。下面就来列举一二。假设有一张表 person_tbl，其中包含一个name字段。   

寻找以 'st' 开头的名称，查询如下：   

`mysql> SELECT name FROM person_tbl WHERE name REGEXP '^st';`   

寻找以 'ok' 结尾的名称，查询如下：    

`mysql> SELECT name FROM person_tbl WHERE name REGEXP 'ok$';`
  
寻找包含 'mar' 的名称，查询如下：  

`mysql> SELECT name FROM person_tbl WHERE name REGEXP 'mar';`

寻找以元音字母开始并以 'ok' 结尾的名称，查询如下：  

`mysql> SELECT name FROM person_tbl WHERE name REGEXP '^[aeiou]|ok$';`

