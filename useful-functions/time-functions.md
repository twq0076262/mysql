# MySQL 日期与时间方面的函数

|函数名称|函数功能说明|    
|---|---|
|<a href = "#ADDDATE">`ADDDATE()`</a>|添加日期|  
|<a href = "#ADDTIME">`ADDTIME()`</a>|添加时间|
|<a href = "#CONVERT_TZ">`CONVERT_TZ()`</a>|转换不同时区|
|<a href = "#CURDATE">`CURDATE()`</a>|返回当前日期|
|<a href = "#CURRENT_DATE">`CURRENT_DATE()` 与 `CURRENT_DATE`</a>|等同于 `CURDATE()`|   
|<a href = "#CURRENT_TIME2">`CURRENT_TIME()` 与 `CURRENT_TIME`</a>|等同于 `CURTIME()`|
|<a href = "#CURRENT_TIMESTAMP">`CURRENT_TIMESTAMP()` 与 `CURRENT_TIMESTAMP`</a>|等同于 `NOW()`|
|<a href = "#CURTIME">`CURTIME()`</a>|返回当前时间|
|<a href = "#DATE_ADD">`DATE_ADD()`</a>|添加两个日期|
|<a href = "#DATE_FORMAT">`DATE_FORMAT()`</a>|按指定方式格式化日期|  
|<a href = "#DATE_SUB">`DATE_SUB()`</a>|求解两个日期的间隔|
|<a href = "#DATE">`DATE()`</a>|提取日期或日期时间表达式中的日期部分|
|<a href = "#DATEDIFF">`DATEDIFF()`</a>|求解两个日期的间隔|
|<a href = "#DAY">`DAY()`</a>|等同于 `DAYOFMONTH()`|
|<a href = "#DAYNAME">`DAYNAME()`</a>|返回星期中某天的名称|
|<a href = "#DAYOFMONTH">`DAYOFMONTH()`</a>|返回一月中某天的序号（1-31）|  
|<a href = "#DAYOFWEEK">`DAYOFWEEK()`</a>|返回参数所定影的一周中某天的索引值|
|<a href = "#DAYOFYEAR">`DAYOFYEAR()`</a>|返回一年中某天的序号（1-366）|  
|<a href = "#EXTRACT">`EXTRACT`</a>|提取日期中的相应部分|
|<a href = "#FROM_DAYS">`FROM_DAYS()`</a>|将一个天数序号转变为日期值|
|<a href = "#FROM_UNIXTIME">`FROM_UNIXTIME()`</a>|将日期格式化为 UNIX 的时间戳| 
|<a href = "#HOUR">`HOUR()`</a>|提取时间|
|<a href = "#LAST_DAY">`LAST_DAY`</a>|根据参数，返回月中最后一天|
|<a href = "#LOCALTIME">`LOCALTIME()` 和 `LOCALTIME`</a>|等同于 `NOW()`|
|<a href = "#LOCALTIMESTAMP">`LOCALTIMESTAMP` 和 `LOCALTIMESTAMP()`</a>|等同于 `NOW()`|  
|<a href = "#MAKEDATE">`MAKEDATE()`</a>|基于给定参数年份和所在年中的天数序号，返回一个日期|
|<a href = "#MAKETIME">`MAKETIME`</a>|`MAKETIME()`|
|<a href = "#MICROSECOND">`MICROSECOND()`</a>|返回参数所对应的毫秒数|  
|<a href = "#MINUTE">`MINUTE()`</a>|返回参数对应的分钟数|  
|<a href = "#MONTH">`MONTH()`</a>|返回传入日期所对应的月序数| 
|<a href = "#MONTHNAME">`MONTHNAME()`</a>|返回月的名称| 
|<a href = "#NOW">`NOW()`</a>|返回当前日期与时间|
|<a href = "#PERIOD_ADD">`PERIOD_ADD()`</a>|为年-月组合日期添加一个时段|
|<a href = "#PERIOD_DIFF">`PERIOD_DIFF()`|返回两个时段之间的月份差值|
|<a href = "#QUARTER">`QUARTER()`|返回日期参数所对应的季度序号|
|<a href = "#SEC_TO_TIME">`SEC_TO_TIME()`</a>|将描述转变成 'HH:MM:SS' 的格式|
|<a href = "#SECOND">`SECOND()`</a>|返回秒序号（0-59）|
|<a href = "#STR_TO_DATE">`STR_TO_DATE()`</a>|将字符串转变为日期|  
|<a href = "#SUBDATE">`SUBDATE()`</a>|三个参数的版本相当于 `DATE_SUB()`|   
|<a href = "#SUBTIME">`SUBTIME()`</a>|计算时间差值|
|<a href = "#SYSDATE">`SYSDATE()`</a>|返回函数执行时的时间|
|<a href = "#TIME_FORMAT">`TIME_FORMAT()`</a>|提取参数中的时间部分|
|<a href = "#TIME_TO_SEC">`TIME_TO_SEC()`</a>|将参数转化为秒数|
|<a href = "#TIME">`TIME()`</a>|提取传入表达式的时间部分|
|<a href = "#TIMEDIFF">`TIMEDIFF()`</a>|计算时间差值|
|<a href = "#TIMESTAMP">`TIMESTAMP()`</a>|单个参数时，函数返回日期或日期时间表达式；有2个参数时，将参数加和|  
|<a href = "#TIMESTAMPADD">`TIMESTAMPADD()`</a>|为日期时间表达式添加一个间隔 INTERVAL|
|<a href = "#TIMESTAMPDIFF">`TIMESTAMPDIFF()`</a>|从日期时间表达式中减去一个间隔 INTERVAL|
|<a href = "#TO_DAYS">`TO_DAYS()`</a>|返回转换成天数的日期参数|
|<a href = "#UNIX_TIMESTAMP">`UNIX_TIMESTAMP()`</a>|返回一个 UNIX 时间戳|
|<a href = "#UTC_DATE">`UTC_DATE()`</a>|返回当前的 UTC 日期|
|<a href = "#UTC_TIME">`UTC_TIME()`</a>|返回当前的 UTC 时间|
|<a href = "#UTC_TIMESTAMP">`UTC_TIMESTAMP()`</a>|返回当前的 UTC 时间与日期|
|<a href = "#WEEK">`WEEK()`</a>|返回周序号|
|<a href = "#WEEKDAY">`WEEKDAY()`</a>|返回某天在星期中的索引值|
|<a href = "#WEEKOFYEAR">`WEEKOFYEAR()`</a>|返回日期所对应的星期在一年当中的序号（1-53）|
|<a href = "#YEAR">`YEAR()`</a>|返回年份|
|<a href = "#YEARWEEK">`YEARWEEK()`</a>|返回年份及星期序号|  

----  


##<a name = "ADDDATE">ADDDATE(date,INTERVAL expr unit), ADDDATE(expr,days)</a>        


在第2个参数使用 INTERVAL 格式时，`ADDDATE()` 作用就相当于 `DATE_ADD()`。相关的函数 `SUBDATE()` 相当于 `DATE_SUB()`。要想了解 INTERVAL 单位参数，参看`DATE_ADD()`相关内容。示例如下：   

```
mysql> SELECT DATE_ADD('1998-01-02', INTERVAL 31 DAY);
+---------------------------------------------------------+
| DATE_ADD('1998-01-02', INTERVAL 31 DAY)                 |
+---------------------------------------------------------+
| 1998-02-02                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT ADDDATE('1998-01-02', INTERVAL 31 DAY);
+---------------------------------------------------------+
| ADDDATE('1998-01-02', INTERVAL 31 DAY)                  |
+---------------------------------------------------------+
| 1998-02-02                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

当函数的第2个参数采用 `days` 格式时，MySQL 会认为它是一个表示天数的整数，将它添加到 `expr` 上。示例如下：   

```
mysql> SELECT ADDDATE('1998-01-02', 31);
+---------------------------------------------------------+
| DATE_ADD('1998-01-02', INTERVAL 31 DAY)                 |
+---------------------------------------------------------+
| 1998-02-02                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```





## <a name = "ADDTIME">ADDTIME(expr1, expr2)</a>  

`ADDTIME()` 将 expr2 参数加到 expr1 参数上，返回结果。expr1 是一个时间或日期时间表达式。expr2 是一个时间表达式。   

```
mysql> SELECT ADDTIME('1997-12-31 23:59:59.999999','1 1:1:1.000002');
+---------------------------------------------------------+
| DATE_ADD('1997-12-31 23:59:59.999999','1 1:1:1.000002') |
+---------------------------------------------------------+
| 1998-01-02 01:01:01.000001                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "CONVERT_TZ">CONVERT_TZ(dt,from_tz,to_tz)</a>


这是一个转换时区的函数，将参数 `from_tz` 所定时区的日期时间值 `dt` 转变到参数 `to_tz` 所定时区，然后返回结果。如果参数无效，则该函数返回 NULL 值。   

```
mysql> SELECT CONVERT_TZ('2004-01-01 12:00:00','GMT','MET');
+---------------------------------------------------------+
| CONVERT_TZ('2004-01-01 12:00:00','GMT','MET')           |
+---------------------------------------------------------+
| 2004-01-01 13:00:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT CONVERT_TZ('2004-01-01 12:00:00','+00:00','+10:00');
+---------------------------------------------------------+
| CONVERT_TZ('2004-01-01 12:00:00','+00:00','+10:00')     |
+---------------------------------------------------------+
| 2004-01-01 22:00:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name = "CURDATE">CURDATE()</a>

返回当前日期的函数。根据函数究竟用于字符串还是数字上下文，选择使用 'YYYY-MM-DD'（'年-月-日'） 或 YYYYMMDD（年月日） 格式返回当前日期。   

```
mysql> SELECT CURDATE();
+---------------------------------------------------------+
| CURDATE()                                               |
+---------------------------------------------------------+
| 1997-12-15                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT CURDATE() + 0;
+---------------------------------------------------------+
| CURDATE() + 0                                           |
+---------------------------------------------------------+
| 19971215                                                |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "CURRENT_DATE">`CURRENT_DATE` 和 `CURRENT_DATE()`</a>   

`CURRENT_DATE` 和 `CURRENT_DATE()` 实际上等于 `CURDATE()`。


## <a name = "CURTIME">CURTIME()</a>  

根据函数究竟用于字符串或数字上下文，选择以 'HH:MM:SS' 还是 HHMMSS 格式返回当前时间值（以当前时区来定）。  

```
mysql> SELECT CURTIME();
+---------------------------------------------------------+
| CURTIME()                                               |
+---------------------------------------------------------+
| 23:50:26                                                |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT CURTIME() + 0;
+---------------------------------------------------------+
| CURTIME() + 0                                           |
+---------------------------------------------------------+
| 235026                                                  |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "CURRENT_TIME2">CURRENT_TIME 和 CURRENT_TIME()</a>
 
 
`CURRENT_TIME` 和 `CURRENT_TIME()` 都相当于 `CURTIME()`。  


## <a name = "CURRENT_TIMESTAMP">CURRENT_TIMESTAMP 和 CURRENT_TIMESTAMP()</a>

 
`CURRENT_TIMESTAMP` 和 `CURRENT_TIMESTAMP()` 实际上相当于 `NOW()`。   


## <a name = "DATE">DATE(expr)</a>  

提取日期或日期时间表达式 `expr` 中的日期部分。

```
mysql> SELECT DATE('2003-12-31 01:02:03');
+---------------------------------------------------------+
| DATE('2003-12-31 01:02:03')                             |
+---------------------------------------------------------+
|  2003-12-31                                             |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "DATEDIFF">DATEDIFF(expr1,expr2)</a>


`DATEDIFF()`将返回`expr1 - expr2 `的值，用来表示两个日期相差的天数。`expr1` 和 `expr2` 都是日期或日期时间表达式。运算中只用到了这些值的日期部分。  

```
mysql> SELECT DATEDIFF('1997-12-31 23:59:59','1997-12-30');
+---------------------------------------------------------+
| DATEDIFF('1997-12-31 23:59:59','1997-12-30')            |
+---------------------------------------------------------+
| 1                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "DATE_ADD">DATE_ADD(date,INTERVAL expr unit) 与 DATE_SUB(date,INTERVAL expr unit)</a>


执行日期计算的两种函数。`date` 是一个用来指定**开始日期**的 DATETIME 或 DATE 值。`expr` 是一种以字符串形式呈现的表达式，用来指定从开始日期增加或减少的间隔值。如果是负的间隔值，则 `expr` 值的第一个字符是`-`号。`unit` 是一个单位关键字，用来指定expr表达式应该采取的单位。

INTERVAL 关键字与单位说明符都不区分大小写。   

下表列出了每个单位数值所对应的 expr 参数的期望格式。   

|单位所能取的值|期望的expr格式|  
|----|----|  
|`MICROSECOND`|毫秒|
|`SECOND`|秒|
|`MINUTE`|分|
|`HOUR`|小时|
|`DAY`|日|
|`WEEK`|周|
|`MONTH`|月|
|`QUARTER`|季度|
|`YEAR`|年|
|`SECOND_MICROSECOND`|'秒.毫秒'|
|`MINUTE_MICROSECOND`|'分.毫秒'|
|`MINUTE_SECOND`|'分:秒'|
|`HOUR_MICROSECOND`|'小时.毫秒'|
|`HOUR_SECOND`|'小时:分:秒'|
|`HOUR_MINUTE`|'小时:分'|
|`DAY_MICROSECOND`|'日.毫秒'|
|`DAY_SECOND`|'日 小时:分:秒'|
|`DAY_MINUTE`|'日 小时:分'|
|`DAY_HOUR`|'日 小时'|
|`YEAR_MONTH`|'年-月'|   

QUARTER 和 WEEK 都是 MySQL 5.0.0 才开始引入的单位值。   


```
mysql> SELECT DATE_ADD('1997-12-31 23:59:59', 
    -> INTERVAL '1:1' MINUTE_SECOND);
+---------------------------------------------------------+
| DATE_ADD('1997-12-31 23:59:59', INTERVAL...             |
+---------------------------------------------------------+
| 1998-01-01 00:01:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_ADD('1999-01-01', INTERVAL 1 HOUR);
+---------------------------------------------------------+
| DATE_ADD('1999-01-01', INTERVAL 1 HOUR)                 |
+---------------------------------------------------------+
| 1999-01-01 01:00:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```  


## <a name = "DATE_FORMAT">DATE_FORMAT(date,format)</a>


该函数会根据 format 字符串来格式化 date 值。   

下表中列出了一些可用于 format 字符串的标识符。格式标识符第一个字符必须是`%`字符。  

|格式标识符|说明|
|----|----|   
|`%a`|一星期中每天名称的缩写（Sun...Sat）|
|`%b`|月份的缩写（Jan...Dec）|  
|`%c`|月份的数字表现形式（0...12）|
|`%D`|带有英语后缀的一个月中的每一天的名称（0th、1st、2nd、3rd）|  
|`%d`|用数字形式表现的每月中的每一天（00...31）|  
|`%e`|用数字形式表现的每月中的每一天（0...31）|  
|`%f`|毫秒（000000...999999）|
|`%H`|24时制显示的小时（00...23）|
|`%h`|12时制显示的小时（01...12）|
|`%I`|12时制显示的小时（01...12）|
|`%i`|以数字形式表现的分钟数（00...59）|
|`%j`|一年中的每一天（001...366）|
|`%k`|24时制小时的另一种表现格式（0...23）|
|`%l`|12时制小时的另一种表现格式（1...12）|
|`%M`|用完整英文名称表示的月份（January...December）|
|`%m`|用数字表现的月份（00...12）|
|`%p`|上午（AM）或下午（PM）|
|`%r`|12时制的时间值（hh:mm:ss，后跟 AM 或 PM）|
|`%S`|秒（00...59）|
|`%s`|秒（00...59）|
|`%T`|24时制的小时（hh:mm:ss）|
|`%U`|星期（00...53），其中星期天是每星期的开始日|
|`%u`|星期（00...53），其中星期一是每星期的开始日|
|`%V`|星期（01...53），其中星期天是每星期的开始日，和 `%X` 一起使用|
|`%v`|星期（01...53），其中星期一是每星期的开始日，和 `%x` 一起使用|
|`%W`|一星期中各日名称（Sunday...Saturday）
|`%w`|一星期中各日名称（0代表星期日，6代表星期六，以此类推）|
|`%X`|某星期所处年份。其中，星期天是每星期的开始日，采用4位数字形式表现，和 `%V`一起使用|
|`%x`|某星期所处年份。其中，星期一是每星期的开始日，采用4位数字形式表现，和 `%V` 一起使用|
|`%Y`|4位数字表示的年份|
|`%y`|2位数字表示的年份|
|`%%`|符号`%`的字面值|
|%x（x为斜体）|字符x的字面值，x指以上未列出的任何字符|    


```
mysql> SELECT DATE_FORMAT('1997-10-04 22:23:00', '%W %M %Y');
+---------------------------------------------------------+
| DATE_FORMAT('1997-10-04 22:23:00', '%W %M %Y')          |
+---------------------------------------------------------+
| Saturday October 1997                                   |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT('1997-10-04 22:23:00'
    -> '%H %k %I %r %T %S %w');
+---------------------------------------------------------+
| DATE_FORMAT('1997-10-04 22:23:00.......                 |
+---------------------------------------------------------+
|  22 22 10 10:23:00 PM 22:23:00 00 6                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "DATE_SUB">DATE_SUB(date,INTERVAL expr unit)</a>

类似 `DATE_ADD()` 函数。


## <a name = "DAY">DAY(date)</a>

`DAY()` 等同于 `DAYOFMONTH()`。   

## <a name = "DAYNAME">DAYNAME(date)</a>  

返回 `date` 参数所对应的星期几。  

```
mysql> SELECT DAYNAME('1998-02-05');
+---------------------------------------------------------+
| DAYNAME('1998-02-05')                                   |
+---------------------------------------------------------+
| Thursday                                                |
+---------------------------------------------------------+
1 row in set (0.00 sec)
  
```



## <a name = "DAYOFMONTH">DAYOFMONTH(date)</a>

返回 `date` 参数所对应的一月中的第几天，取值范围从0到31。   

```
mysql> SELECT DAYOFMONTH('1998-02-03');
+---------------------------------------------------------+
| DAYOFMONTH('1998-02-03')                                |
+---------------------------------------------------------+
| 3                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```  

## <a name = "DAYOFWEEK">DAYOFWEEK(date)</a>


返回 `date` 参数所对应的每周中的某一天的索引值（1 = Sunday，2 = Monday……7 = Saturday）。这些索引值对应着 ODBC 标准。


```
mysql> SELECT DAYOFWEEK('1998-02-03');
+---------------------------------------------------------+
|DAYOFWEEK('1998-02-03')                                  |
+---------------------------------------------------------+
| 3                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "DAYOFYEAR">DAYOFYEAR(date)</a>

返回 `date` 参数所对应的一年中的某一天，取值范围从1到366。   

```
mysql> SELECT DAYOFYEAR('1998-02-03');
+---------------------------------------------------------+
| DAYOFYEAR('1998-02-03')                                 |
+---------------------------------------------------------+
| 34                                                      |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name ="EXTRACT">EXTRACT(unit FROM date)</a>


`EXTRACT()` 函数 使用同样的单位标识符 `DATE_ADD()` 或 `DATE_SUB()`，但是只从 `date`  中提取相应部分，而不执行日期运算。   




```
mysql> SELECT EXTRACT(YEAR FROM '1999-07-02');
+---------------------------------------------------------+
| EXTRACT(YEAR FROM '1999-07-02')                         |
+---------------------------------------------------------+
| 1999                                                    |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT EXTRACT(YEAR_MONTH FROM '1999-07-02 01:02:03');
+---------------------------------------------------------+
| EXTRACT(YEAR_MONTH FROM '1999-07-02 01:02:03')          |
+---------------------------------------------------------+
| 199907                                                  |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name ="FROM_DAYS">FROM_DAYS(N)</a>

给定某日 `N`，返回一个 DATE 值。   


```
mysql> SELECT FROM_DAYS(729669);
+---------------------------------------------------------+
| FROM_DAYS(729669)                                       |
+---------------------------------------------------------+
| 1997-10-07                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```  


使用 `FROM_DAYS()` 时，要特别注意古代的日期。该函数不适用于格里高里历（即公历）颁布（公元1582年）之前的日期。


## <a name= "FROM_UNIXTIME">FROM_UNIXTIME(unix_timestamp) FROM_UNIXTIME(unix_timestamp,format)</a>  


```
mysql> SELECT FROM_UNIXTIME(875996580);
+---------------------------------------------------------+
| FROM_UNIXTIME(875996580)                                |
+---------------------------------------------------------+
| 1997-10-04 22:23:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name = "HOUR">HOUR(time)</a>





```
mysql> SELECT HOUR('10:05:03');
+---------------------------------------------------------+
| HOUR('10:05:03')                                        |
+---------------------------------------------------------+
| 10                                                      |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name= "LAST_DAY">LAST_DAY(date)</a>
 
 
 
```
mysql> SELECT LAST_DAY('2003-02-05');
+---------------------------------------------------------+
| LAST_DAY('2003-02-05')                                  |
+---------------------------------------------------------+
| 2003-02-28                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name= "LOCALTIME">LOCALTIME 和 LOCALTIME()  </a>

`LOCALTIME` 和 `LOCALTIME()` 与 `NOW()` 具有相同意义。     


## <a name="LOCALTIMESTAMP">LOCALTIMESTAMP 和 LOCALTIMESTAMP()   </a>

`LOCALTIMESTAMP` 和 `LOCALTIMESTAMP()` 与 `NOW()`具有相同意义。   


## <a name="MAKEDATE">MAKEDATE(year,dayofyear)    </a>

基于给定参数年份（`year`）和一年中的某一天（`dayofyear`）<sup></sup>，返回一个日期值。`dayofyear`必须大于0，否则结果为空。

<sup>`dayofyear`与<a href = "#DAYOFYEAR">`DAYOFYEAR()`</a>函数取值类似，取值范围为1-366。</sup>   


```
mysql> SELECT MAKEDATE(2001,31), MAKEDATE(2001,32);
+---------------------------------------------------------+
| MAKEDATE(2001,31), MAKEDATE(2001,32)                    |
+---------------------------------------------------------+
| '2001-01-31', '2001-02-01'                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

``` 


## <a name="MAKETIME">MAKETIME(hour,minute,second)</a>

基于给定的 `hour`、`minute`以及 `second` 这3个参数，计算出一个时间值。   

```
mysql> SELECT MAKETIME(12,15,30);
+---------------------------------------------------------+
| MAKETIME(12,15,30)                                      |
+---------------------------------------------------------+
| '12:15:30'                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```




## <a name="MICROSECOND">MICROSECOND(expr)</a>


基于时间或“日期+时间”的表达式 expr，返回一个以毫秒计的时间值，取值范围为0-99999。  

```
mysql> SELECT MICROSECOND('12:00:00.123456');
+---------------------------------------------------------+
| MICROSECOND('12:00:00.123456')                          |
+---------------------------------------------------------+
| 123456                                                  |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="MINUTE">MINUTE(time)  </a>

基于 `time` 参数，返回分钟数，取值范围为0-59。   

```
mysql> SELECT MINUTE('98-02-03 10:05:03');
+---------------------------------------------------------+
| MINUTE('98-02-03 10:05:03')                             |
+---------------------------------------------------------+
| 5                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="MONTH">MONTH(date)</a>

基于 `date` 参数，返回月份值，取值范围为0-12。   

```
mysql> SELECT MONTH('1998-02-03')
+---------------------------------------------------------+
| MONTH('1998-02-03')                                     |
+---------------------------------------------------------+
| 2                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="MONTHNAME">MONTHNAME(date)</a>


基于 `date` 参数，返回月份的完整英文名称。   


```
mysql> SELECT MONTHNAME('1998-02-05');
+---------------------------------------------------------+
| MONTHNAME('1998-02-05')                                 |
+---------------------------------------------------------+
| February                                                |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="NOW">NOW()</a>

返回一定格式的日期+时间值。根据函数是否用于字符串或数字内容，格式为 'YYYY-MM-DD HH:MM:SS' 或 YYYYMMDDHHMMSS。
 
 
```
mysql> SELECT NOW();
+---------------------------------------------------------+
| NOW()                                                   |
+---------------------------------------------------------+
| 1997-12-15 23:50:26                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="PERIOD_ADD">PERIOD_ADD(P,N)</a>

将 N 个月添加到时段 P （格式为 YYMM 或 YYYYMM）上，返回值格式为 YYYYMM。注意：时段参数 P 不是一个日期值。  

```
mysql> SELECT PERIOD_ADD(9801,2);
+---------------------------------------------------------+
| PERIOD_ADD(9801,2)                                      |
+---------------------------------------------------------+
| 199803                                                  |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="PERIOD_DIFF">PERIOD_DIFF(P1,P2)</a>

时段 `P1` 和 `P2` 之间的月份差值。`P1` 与 `P2` 的格式应为 YYMM 或 YYYYMM。注意，时段参数 `P1` 和 `P2` 都不是日期值。   


```
mysql> SELECT PERIOD_DIFF(9802,199703);
+---------------------------------------------------------+
| PERIOD_DIFF(9802,199703)                                |
+---------------------------------------------------------+
| 11                                                      |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="QUARTER">QUARTER(date)</a>

返回参数 `date` 所对应的年中某季度，取值范围为1-4。   

```
mysql> SELECT QUARTER('98-04-01');
+---------------------------------------------------------+
| QUARTER('98-04-01')                                     |
+---------------------------------------------------------+
| 2                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="SECOND">SECOND(time)</a>

返回参数 `time` 所对应的秒数，取值范围为0-59。  

```
mysql> SELECT SECOND('10:05:03');
+---------------------------------------------------------+
| SECOND('10:05:03')                                      |
+---------------------------------------------------------+
| 3                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="SEC_TO_TIME">SEC_TO_TIME(seconds)  </a>

将参数 `seconds` 转换成以'HH:MM:SS' 或 HHMMSS 格式（根据函数应用上下文是字符串还是数字）输出的时间值。   

```
mysql> SELECT SEC_TO_TIME(2378);
+---------------------------------------------------------+
| SEC_TO_TIME(2378)                                       |
+---------------------------------------------------------+
| 00:39:38                                                |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="STR_TO_DATE">STR_TO_DATE(str,format)</a>


`DATE_FORMAT()`函数的逆向函数。包含2个参数，字符串类型参数 `str` 和格式字符串参数 `format`。返回值有2种可能性：如果格式字符串既包含日期又包含时间，则返回一个 DATETIME 值；如果格式字符串只包含日期或时间部分，则函数也相应返回 DATE 或 TIME 类型的值。   


```
mysql> SELECT STR_TO_DATE('04/31/2004', '%m/%d/%Y');
+---------------------------------------------------------+
| STR_TO_DATE('04/31/2004', '%m/%d/%Y')                   |
+---------------------------------------------------------+
| 2004-04-31                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="SUBDATE">SUBDATE(date,INTERVAL expr unit) 与 SUBDATE(expr,days)</a>


当第二个参数采用 INTERVAL 格式时，`SUBDATE()` 等同于 `DATE_SUB()`。要想详细了解 INTERVAL 单元参数，请参考 `DATE_ADD()`。   


```
mysql> SELECT DATE_SUB('1998-01-02', INTERVAL 31 DAY);
+---------------------------------------------------------+
| DATE_SUB('1998-01-02', INTERVAL 31 DAY)                 |
+---------------------------------------------------------+
| 1997-12-02                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT SUBDATE('1998-01-02', INTERVAL 31 DAY);
+---------------------------------------------------------+
| SUBDATE('1998-01-02', INTERVAL 31 DAY)                  |
+---------------------------------------------------------+
| 1997-12-02                                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="SUBTIME">SUBTIME(expr1,expr2)</a>
 
 
返回值为 `expr1 - expr2`，格式与 `expr1` 相同。`expr1` 是一个时间或日期时间表达式，而 `expr2` 是一个时间表达式。  


```
mysql> SELECT SUBTIME('1997-12-31 23:59:59.999999',
    -> '1 1:1:1.000002');
+---------------------------------------------------------+
| SUBTIME('1997-12-31 23:59:59.999999'...                 |
+---------------------------------------------------------+
| 1997-12-30 22:58:58.999997                              |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="SYSDATE">SYSDATE()</a>

根据函数所应用的上下文究竟是字符串还是数字，以 'YYYY-MM-DD HH:MM:SS' 或 YYYYMMDDHHMMSS 格式返回当前日期与时间值。   

```
mysql> SELECT SYSDATE();
+---------------------------------------------------------+
| SYSDATE()                                               |
+---------------------------------------------------------+
| 2006-04-12 13:47:44                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="TIME">TIME(expr)</a>


提取时间或日期时间表达式 `expr` 的时间部分，将其作为字符串返回。   

```
mysql> SELECT TIME('2003-12-31 01:02:03');
+---------------------------------------------------------+
| TIME('2003-12-31 01:02:03')                             |
+---------------------------------------------------------+
| 01:02:03                                                |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="TIMEDIFF">TIMEDIFF(expr1,expr2)</a>

返回表示为时间值的 `expr1 - expr2`，`expr1` 和 `expr2` 都是时间或日期与时间表达式，但两者必须类型相同。   

 

```
mysql> SELECT TIMEDIFF('1997-12-31 23:59:59.000001',
    -> '1997-12-30 01:01:01.000002');
+---------------------------------------------------------+
| TIMEDIFF('1997-12-31 23:59:59.000001'.....              |
+---------------------------------------------------------+
|  46:58:57.999999                                        |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="TIMESTAMP">TIMESTAMP(expr), TIMESTAMP(expr1,expr2)</a>


当只接受一个参数 `expr`（日期或日期时间类型）时，函数将这个参数以日期时间的形式返回；若接受两个参数，函数则会将时间参数 `expr2` 添加到日期或日期时间参数 `expr1` 上，以日期时间形式返回这个组合值。



```
mysql> SELECT TIMESTAMP('2003-12-31');
+---------------------------------------------------------+
| TIMESTAMP('2003-12-31')                                 |
+---------------------------------------------------------+
| 2003-12-31 00:00:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```




## <a name="TIMESTAMPADD">TIMESTAMPADD(unit,interval,datetime_expr)</a>

函数将表示间隔值的整形参数 `interval` 添加到日期或日期时间参数 `datetime_expr` 上。`interval` 所采用的单位由 `unit` 参数指定。`unit` 参数的取值范围是：FRAC_SECOND、SECOND、MINUTE、HOUR、DAY、WEEK、MONTH、QUARTER 或 YEAR。   


`unit` 值也可以通过一个前面介绍过的关键字来标识，或者说需要加上前缀 `SQL_TSI_`。例如：DAY 和 SQL_TSI_DAY。这两种形式都是合法的。


```
mysql> SELECT TIMESTAMPADD(MINUTE,1,'2003-01-02');
+---------------------------------------------------------+
| TIMESTAMPADD(MINUTE,1,'2003-01-02')                     |
+---------------------------------------------------------+
| 2003-01-02 00:01:00                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="TIMESTAMPDIFF">TIMESTAMPDIFF(unit,datetime_expr1,datetime_expr2)</a>


返回两个日期或日期时间类型参数 `datetime_expr1` 与 `datetime_epr2` 之间的整数差值。返回值所采用的单位由 `unit` 参数指定。有关`unit` 的合法值，可参看 `TIMESTAMPADD()` 函数介绍。    


```
mysql> SELECT TIMESTAMPDIFF(MONTH,'2003-02-01','2003-05-01');
+---------------------------------------------------------+
| TIMESTAMPDIFF(MONTH,'2003-02-01','2003-05-01')          |
+---------------------------------------------------------+
| 3                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="TIME_FORMAT">TIME_FORMAT(time,format)</a>


该函数和 `DATE_FORMAT()` 函数用法类似，但 `format` 字符串中只含有与小时、分钟、秒相关的格式标识符。   

如果 `time` 值包含一个大于23的小时数，%H 与 %k 小时格式标识符就会生成一个超出平时所用范围（0-23）的值。其他与小时相关的格式标识符会生成以12取模的值。  

```
mysql> SELECT TIME_FORMAT('100:00:00', '%H %k %h %I %l');
+---------------------------------------------------------+
| TIME_FORMAT('100:00:00', '%H %k %h %I %l')              |
+---------------------------------------------------------+
| 100 100 04 04 4                                         |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```	

## <a name="TIME_TO_SEC">TIME_TO_SEC(time)</a>


将 `time` 参数转换成秒数返回。     

```
mysql> SELECT TIME_TO_SEC('22:23:00');
+---------------------------------------------------------+
| TIME_TO_SEC('22:23:00')                                 |
+---------------------------------------------------------+
| 80580                                                   |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name ="TO_DAYS">TO_DAYS(date)</a>


基于日期参数 `date`，返回一个天数（自年份0开始的天数）。   

```
mysql> SELECT TO_DAYS(950501);
+---------------------------------------------------------+
| TO_DAYS(950501)                                         |
+---------------------------------------------------------+
| 728779                                                  |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```

## <a name="UNIX_TIMESTAMP">UNIX_TIMESTAMP(), UNIX_TIMESTAMP(date)</a>



如果不传入参数调用该函数，返回一个 UNIX 时间戳，它是一个自 '1970-01-01 00:00:00'   UTC（世界统一时间） 起计算的秒数，无符号整形值。如果传入 `date` 参数调用该函数，则返回一个自'1970-01-01 00:00:00' UTC 到该参数所示时间所经历的秒数。`date` 参数可能是 DATE 字符串、DATETIME 字符串、TIMESTAMP，或者也有可能是以 YYMMDD 或 YYYYMMDD 格式表示的数值。  


```
mysql> SELECT UNIX_TIMESTAMP();
+---------------------------------------------------------+
| UNIX_TIMESTAMP()                                        |
+---------------------------------------------------------+
| 882226357                                               |
+---------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT UNIX_TIMESTAMP('1997-10-04 22:23:00');
+---------------------------------------------------------+
| UNIX_TIMESTAMP('1997-10-04 22:23:00')                   |
+---------------------------------------------------------+
| 875996580                                               |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="UTC_DATE">UTC_DATE, UTC_DATE()</a>


根据函数应用的上下文究竟是字符串还是数字，相应地以 'YYYY-MM-DD' 或 YYYYMMDD 格式返回当前的 UTC 日期值。    


```
mysql> SELECT UTC_DATE(), UTC_DATE() + 0;
+---------------------------------------------------------+
| UTC_DATE(), UTC_DATE() + 0                              |
+---------------------------------------------------------+
| 2003-08-14, 20030814                                    |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name = "UTC_TIME">UTC_TIME, UTC_TIME()  </a>


根据函数应用的上下文究竟是字符串还是数字，相应地以 'HH:MM:SS' 或 HHMMSS 格式返回当前的 UTC 时间值。   

```
mysql> SELECT UTC_TIME(), UTC_TIME() + 0;
+---------------------------------------------------------+
| UTC_TIME(), UTC_TIME() + 0                              |
+---------------------------------------------------------+
| 18:07:53, 180753                                        |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="UTC_TIMESTAMP">UTC_TIMESTAMP, UTC_TIMESTAMP()</a>
 
 
 
根据函数应用的上下文究竟是字符串还是数字，相应地以 'YYYY-MM-DD HH:MM:SS' 或 YYYYMMDDHHMMSS 格式返回当前的 UTC 日期与时间值。    



```
mysql> SELECT UTC_TIMESTAMP(), UTC_TIMESTAMP() + 0;
+---------------------------------------------------------+
| UTC_TIMESTAMP(), UTC_TIMESTAMP() + 0                    |
+---------------------------------------------------------+
| 2003-08-14 18:08:04, 20030814180804                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="WEEK">WEEK(date[,mode])  </a>


该函数返回日期参数 `date` 所对应的星期序号。如果传入两个参数，则可以指定每星期起始日究竟是星期天还是星期一，以及返回值范围究竟是0-53，还是从1-53。如果忽略 `mode` 参数，就采用 `default_week_format` 系统变量值。 


|模式|每星期的起始天|范围|当 Week 1 是第一个星期时|
|----|----|----|----|  
|0|星期日|0-53|本年有一个周日|  
|1|星期一|0-53|本年有3天以上|  
|2|星期日|1-53|本年有一个周日| 
|3|星期一|1-53|本年有3天以上|
|4|星期日|0-53|本年有3天以上|
|5|星期一|0-53|本年有一个周一|
|6|星期日|1-53|本年有3天以上|
|7|星期一|1-53|本年有一个周日|




```
mysql> SELECT WEEK('1998-02-20');
+---------------------------------------------------------+
| WEEK('1998-02-20')                                      |
+---------------------------------------------------------+
| 7                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```


## <a name="WEEKDAY">WEEKDAY(date)</a>



返回日期参数 `date` 所对应的星期中每天的索引值（例如，0=星期一，1=星期二，6=星期天）。   

```
mysql> SELECT WEEKDAY('1998-02-03 22:23:00');
+---------------------------------------------------------+
| WEEKDAY('1998-02-03 22:23:00')                          |
+---------------------------------------------------------+
| 1                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="WEEKOFYEAR">WEEKOFYEAR(date)</a>


返回日期参数 `date` 所对应的一年中的星期序号（范围1-53）。`WEEKOFYEAR()` 是一个兼容函数，与 WEEK(date,3)等同。


```
mysql> SELECT WEEKOFYEAR('1998-02-20');
+---------------------------------------------------------+
| WEEKOFYEAR('1998-02-20')                                |
+---------------------------------------------------------+
| 8                                                       |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```



## <a name="YEAR">YEAR(date)</a>

返回 `date` 的年份，范围为1000-9999。当 `date` 为0时，返回0。


```
mysql> SELECT YEAR('98-02-03');
+---------------------------------------------------------+
| YEAR('98-02-03')                                        |
+---------------------------------------------------------+
| 1998                                                    |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```  


## <a name="YEARWEEK">YEARWEEK(date) 与 YEARWEEK(date,mode)</a>


返回 `date` 的年份及星期序号。`mode` 参数等同于 `WEEK()` 中的 `mode` 参数。结果中的年份可能会和 `date` 参数中的年份有所不同，差异体现在年份中的第一个与最后一个星期上。

```

mysql> SELECT YEARWEEK('1987-01-01');
+---------------------------------------------------------+
| YEAR('98-02-03')YEARWEEK('1987-01-01')                  |
+---------------------------------------------------------+
| 198653                                                  |
+---------------------------------------------------------+
1 row in set (0.00 sec)

```  

注意，当可选参数为0或1时，`WEEK()` 函数返回的是0，和这里返回的有所不同，因为 `WEEK()` 返回的是指定年份的星期序号。



要想更深入了解有关 MySQL 日期与时间函数的相关信息，请参看[MySQL官方网站——日期与时间函数](http://dev.mysql.com/doc/refman/5.1/en/date-and-time-functions.html)  