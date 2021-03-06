# MySQL 数据类型

对于数据库的整体优化来说，正确定义表中的字段是非常关键的。应该只采用字段》。如果事先知道只会用到2个字符的宽度，就不要把字段定义为10个字符宽。字段（或者说列）的类型也被称为数据类型。   

MySQL使用的多种数据类型可分为三类：数字、日期与时间，以及字符串类型。   

## 数字类型  

MySQL使用标准的 ANSI SQL 数字类型，所以如果你在学习MySQL之前，接触过其他数据库系统，那么肯定对这些定义不会感到陌生。下面就列举出常见的一些数字类型及其说明：   

- **INT** 正常大小的整数，可以有符号，也可以没有符号。如果是有符号整数，其允许的取值范围是-2147483648~2147483647；无符号整数的取值范围是从0至4294967295。最高可指定11位数字。   
- **TINYINT** 非常小的整数，分为有无符号两种。前有符号时，其允许取值范围是-128~127；无符号时的取值范围为0~255。所以，最高可指定4位数字。  
- **SMALLINT** 较小的整数，分为有无符号两种。前有符号时，其允许取值范围是-32768~32767；无符号时的取值范围为0~65535。所以最高可指定5位数字。  
- **MEDIUMINT** 中型大小的整数，分为有无符号两种。前有符号时，其允许取值范围是-8388608~8388607；无符号时的取值范围为0~16777215。所以，最高可指定9位数字。  
- **BIGINT** 较大型的整数，分为有无符号两种。前有符号时，其允许取值范围为-9223372036854775808~9223372036854775807；无符号时的取值范围为0~18446744073709551615。最高可指定20位数字。  
- **FLOAT(M,D)**  不带符号的浮点数。M 代表显示长度，D 代表小数位数。这两个参数都不是必需参数，它们默认为10, 2，表示小数点后有2位数字，而整个数字的位数为10（包含小数位数）。FLOAT 类型的小数精度可以达到24位。  
- **DOUBLE(M,D)**  不带符号的双精度浮点数。M 代表显示长度，D 代表小数位数。这两个参数都不是必需参数，它们默认为16, 4，表示小数点后有4位数字，而整个数字的位数为 16（包含小数位数）。DOUBLE 类型的小数精度可以达到53位。DOUBLE 与 REAL 同义。  
- **DECIMAL(M,D)** 非压缩的无符号浮点数。 在未压缩十进制中，每一位十进制数都对应一个字节。需要定义显示长度（M）和小数位数（D）。DECIMAL 与 NUMERIC 同义。


## 日期与时间类型    

MySQL 包含以下几种日期与时间类型：  

- **DATE** YYYY-MM-DD （年-月-日）格式显示的日期，取值范围从1000-01-01 到 9999-12-31。比如1973年的12月30日就存为 1973-12-30。    
- **DATETIME** 按照 YYYY-MM-DD HH:MM:SS 格式组合显示的日期与时间，取值范围从1000-01-01 00:00:00 到 9999-12-31 23:59:59。比如说1973年的12月30日下午3 : 30就存为1973-12-30 15 : 30 : 00。
- **TIMESTAMP** 介于1970年1月1日凌晨与2037年某个时间点之间的一种时间戳。这种格式与之前的 DATETIME 格式相仿，只不过少了数字间的连字符。1973年12月30日下午3 : 30被存为19731230153000（YYYYMMDDHHMMSS）。
- **TIME** 按照 HH:MM:SS 格式存储的时间。
- **YEAR(M)** 用2位或4位格式存储的时间。如果把长度定为2，比如说YEAR(2)，那么可以表示从1970年到2069年的这些年份（70-69）。如果把长度定为4，YEAR(4)，则可以表示从1901年到2155年。默认长度为4。   


## 字符串类型  

虽然数字与日期类型都很有趣，但通常我们存储最多的就是字符串了。下面列出了 MySQL 中常见的字符串类型。  

- **CHAR(M)** 长度固定的字符串，长度范围从1~255个字符，比如CHAR(5)。在存储时，会向右用空格补齐指定长度。长度并非必须参数，默认长度为1。
- **VARCHAR(M)**  长度不定的字符串，长度范围从1~255个字符。比如：CHAR(25)。在创建VARCHAR字段时，必须定义长度。
- **BLOB or TEXT**   最大长度为65535个字符的字段。BLOB是Binary Large Objects（二进制大型对象）的缩写，专用于保存大量的二进制数据，比如图片或其他类型的文件。TEXT 类型的文件也能保存大型数据。这两者的区别在于存储数据的排序和对比方面，BLOB类型数据是大小写敏感的，而TEXT类型数据则不是。另外，不能指定它们的长度。   
- **TINYBLOB or TINYTEXT**   最大长度为255个字符的 BLOB 或 TEXT 字段。同样也不能指定它们的长度。
- **MEDIUMBLOB or MEDIUMTEXT**  最大长度为16777215个字符的 BLOB 或 TEXT 字段。同样也不能指定它们的长度。
- **LONGBLOB or LONGTEXT** 最大长度为4294967295个字符的 BLOB 或 TEXT 字段。同样也不能指定它们的长度。  
- **ENUM**  枚举类型，是一种很独特的列表类型。ENUM 类型的数据实际是一个包含多个固定值的列表，只能选择这些值（包括 NULL 值）。例如，如果希望某个字段包含 "A"、"B" 和 "C"，必须这样定义：`ENUM ('A', 'B', 'C')`，只有这些值（或 NULL 值）能够填充到该字段中。





