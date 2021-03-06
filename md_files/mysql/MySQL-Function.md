# MySQL 常用函数
## 1. 字符串函数

|         函数          |                             功能                             |
| :-------------------: | :----------------------------------------------------------: |
| concat(s1,s2,...,sn)  |                 连接s1,s2,...,sn为一个字符串                 |
| insert(str,x,y,instr) | 将字符串str从第x位置开始，y个字符长的子串替换为字符串instr（位置从1开始） |
|      lower(str)       |                将字符串str中的字符转换成小写                 |
|      upper(str)       |                将字符串str中的字符转换成大写                 |
|      left(str,x)      |                    返回str最左边的x个字符                    |
|     right(str,x)      |                    返回str最右边的x个字符                    |
|    lpad(str,n,pad)    |    用字符串pad对str最左边进行填充，直到长度为n个字符长度     |
|    rpad(str,n,pad)    |    用字符串pad对str最右边进行填充，直到长度为n个字符长度     |
|      ltrim(str)       |                        去掉左侧的空格                        |
|      rtrim(str)       |                        去掉右侧的空格                        |
|       trim(str)       |                        去掉两侧的空格                        |
|     repeat(str,n)     |                  返回字符串str重复n次的结果                  |
|   replace(str,a,b)    |                   用b替换str中所有出现的a                    |
|     strcmp(s1,s2)     |              比较两个字符串s1,s2。返回1，0，-1               |
|  substring(str,x,y)   |  返回从字符串str的x位置起的y个字符长度的子串（位置从1开始）  |



## 2. 数值函数

|     函数      |                功能                |
| :-----------: | :--------------------------------: |
|    abs(x)     |               绝对值               |
|    ceil(x)    | 返回大于x的最小整数值，即向上取整  |
|   floor(x)    | 返回小于x的最大整数值，即向下取整  |
|   mod(x,y)    |              x对y取余              |
|    rand()     |         返回0~1内的随机值          |
|  round(x,y)   | 返回参数x的四舍五入的有y位小数的值 |
| truncate(x,y) |    返回数字x截断为y位小数的结果    |

eg.

```mysql
mysql> select ceil(1.2), floor(1.2);
+-----------+------------+
| ceil(1.2) | floor(1.2) |
+-----------+------------+
|         2 |          1 |
+-----------+------------+
1 row in set (0.00 sec)

mysql> select ceil(-1.2), floor(-1.2);
+------------+-------------+
| ceil(-1.2) | floor(-1.2) |
+------------+-------------+
|         -1 |          -2 |
+------------+-------------+
1 row in set (0.00 sec)

mysql> select rand(), ceil(100*rand());
+--------------------+------------------+
| rand()             | ceil(100*rand()) |
+--------------------+------------------+
| 0.6494681040285789 |               24 |
+--------------------+------------------+
1 row in set (0.00 sec)

mysql> select round(1.2345,2), round(1.456, 2);
+-----------------+-----------------+
| round(1.2345,2) | round(1.456, 2) |
+-----------------+-----------------+
|            1.23 |            1.46 |
+-----------------+-----------------+
1 row in set (0.00 sec)

mysql> select round(1.2345,6), round(1.456, 6);
+-----------------+-----------------+
| round(1.2345,6) | round(1.456, 6) |
+-----------------+-----------------+
|        1.234500 |        1.456000 |
+-----------------+-----------------+
1 row in set (0.00 sec)

mysql> select strcmp('bb', 'aa'), strcmp('bb', 'bb'), strcmp('bb', 'cc');
+--------------------+--------------------+--------------------+
| strcmp('bb', 'aa') | strcmp('bb', 'bb') | strcmp('bb', 'cc') |
+--------------------+--------------------+--------------------+
|                  1 |                  0 |                 -1 |
+--------------------+--------------------+--------------------+
1 row in set (0.00 sec)

mysql> select truncate(1.2345, 3), truncate(1.2345, 6);
+---------------------+---------------------+
| truncate(1.2345, 3) | truncate(1.2345, 6) |
+---------------------+---------------------+
|               1.234 |            1.234500 |
+---------------------+---------------------+
1 row in set (0.00 sec)
```



## 3. 日期和时间函数



|                函数                |                     功能                      |
| :--------------------------------: | :-------------------------------------------: |
|             curdate()              |                 返回当前日期                  |
|             curtime()              |                 返回当前时间                  |
|               now()                |              返回当前日期和时间               |
|        unix_timestamp(date)        |           返回日期date的unix时间戳            |
|        from_unixtime(stamp)        |            返回时间戳stamp的日期值            |
|             week(date)             |         返回日期date为一年中的第几周          |
|             year(date)             |                返回date的年份                 |
|             hour(time)             |               返回time的小时值                |
|            minute(time)            |               返回time的分钟值                |
|          monthname(date)           |               显示date的月份名                |
|       date_format(date,fmt)        |                格式化日期时间                 |
| date_add(date,INTERVAL expr type)  |  返回与所给日期date加上INTERVAL 时间段的日期  |
| date_sub(date, INTERVAL expr type) |  返回与所给日期date减去INTERVAL 时间段的日期  |
|       datediff(date1,date2)        | 计算两个日期之间相差的天数。date1-date2的天数 |

eg.

```mysql
mysql> select curdate();
+------------+
| curdate()  |
+------------+
| 2018-10-27 |
+------------+
1 row in set (0.00 sec)

mysql> select curtime();
+-----------+
| curtime() |
+-----------+
| 21:45:00  |
+-----------+
1 row in set (0.00 sec)

mysql> select now();
+---------------------+
| now()               |
+---------------------+
| 2018-10-27 21:45:22 |
+---------------------+
1 row in set (0.00 sec)

mysql> select unix_timestamp(now());
+-----------------------+
| unix_timestamp(now()) |
+-----------------------+
|            1540648073 |
+-----------------------+
1 row in set (0.00 sec)

mysql> select from_unixtime(1540648073);
+---------------------------+
| from_unixtime(1540648073) |
+---------------------------+
| 2018-10-27 21:47:53       |
+---------------------------+
1 row in set (0.00 sec)

mysql> select week(now());
+-------------+
| week(now()) |
+-------------+
|          42 |
+-------------+
1 row in set (0.00 sec)

mysql> select year(now());
+-------------+
| year(now()) |
+-------------+
|        2018 |
+-------------+
1 row in set (0.00 sec)

mysql> select hour(now());
+-------------+
| hour(now()) |
+-------------+
|          22 |
+-------------+
1 row in set (0.00 sec)

mysql> select minute(now());
+---------------+
| minute(now()) |
+---------------+
|             4 |
+---------------+
1 row in set (0.00 sec)

mysql> select monthname(now());
+------------------+
| monthname(now()) |
+------------------+
| October          |
+------------------+
1 row in set (0.00 sec)
```

**date_format(date, fmt):**

按照字符串fmt 格式化日期 date 值，此函数能够按指定的格式显示日期，可以用到的格式符如下表显示：

|    格式符     |                           格式说明                           |
| :-----------: | :----------------------------------------------------------: |
|    %S和%s     |                两位数字形式的秒(00,01,...,59)                |
|      %i       |                两位数字形式的分(00,01,...,59)                |
|      %H       |           两位数字形式的小时，24小时(00,01,...,23)           |
| %h和%I(大写i) |           两位数字形式的小时，12小时(01,02,...,12)           |
|      %k       |              数字形式的小时，24小时(0,1,...,23)              |
|   %l(小写L)   |              数字形式的小时，12小时(1,2,...,12)              |
|      %T       |                  24小时的时间形式(hh:mm:ss)                  |
|      %r       |           12小时的时间格式(hh:mm:ssAM或hh:mm:ssPM)           |
|      %p       |                           AM 或 PM                           |
|      %W       |        一周中每一天的名称(Sunday,Monday,...,Saturday)        |
|      %a       |           一周中每一天名称的缩写(Sun,Mon,...,Sat)            |
|      %w       |  以数字形式表示周中的天数(0=Sunday,1=Monday,...,6=Saturday)  |
|      %d       |              两位数字表示月中的天数(01,...,31)               |
|      %e       |              数字形式表示月中的天数(1,2,...,31)              |
|      %D       |           英文后缀表示月中的天数(1st,2nd,3rd,...)            |
|      %j       |           以3位数字表示年中的天数(001,002,...,366)           |
|      %U       | 一年中的第几周(00,01,...,52)，其中Sunday为周中的第一天。（从00开始） |
|      %u       | 一年中的第几周(01,02,...,53)，其中Monday为周中的第一天。（从01开始） |
|      %M       |             月名(January,February,...,December)              |
|      %b       |                 缩写的月名(Jan,Feb,...,Dec)                  |
|      %m       |               两位数字表示的月份(01,02,...,12)               |
|      %c       |                  数字表示的月份(1,2,...,12)                  |
|      %Y       |                   4位数字表示的年份(2018)                    |
|      %y       |                    两位数字表示的年份(18)                    |

eg.



```mysql
mysql> select date_format(now(), '%M, %D, %Y');
+----------------------------------+
| date_format(now(), '%M, %D, %Y') |
+----------------------------------+
| October, 27th, 2018              |
+----------------------------------+
1 row in set (0.00 sec)
```

**时间：**

```mysql
mysql> select date_format(now(), '%H:%i:%S, %H:%i:%s');
+------------------------------------------+
| date_format(now(), '%H:%i:%S, %H:%i:%s') |
+------------------------------------------+
| 23:27:02, 23:27:02                       |
+------------------------------------------+
1 row in set (0.00 sec)

mysql> select date_format(now(), '%h:%i:%S %p, %I:%i:%S %p');
+------------------------------------------------+
| date_format(now(), '%h:%i:%S %p, %I:%i:%S %p') |
+------------------------------------------------+
| 11:27:54 PM, 11:27:54 PM                       |
+------------------------------------------------+
1 row in set (0.00 sec)

mysql> select date_format(now(), '%k:%i:%S, %l:%i:%S %p');
+---------------------------------------------+
| date_format(now(), '%k:%i:%S, %l:%i:%S %p') |
+---------------------------------------------+
| 23:28:57, 11:28:57 PM                       |
+---------------------------------------------+
1 row in set (0.00 sec)

mysql> select date_format(now(), '%T, %r');
+------------------------------+
| date_format(now(), '%T, %r') |
+------------------------------+
| 23:29:32, 11:29:32 PM        |
+------------------------------+
1 row in set (0.00 sec)
```



**星期几：**

```mysql
mysql> select date_format(now(), '%W %a %w');
+--------------------------------+
| date_format(now(), '%W %a %w') |
+--------------------------------+
| Saturday Sat 6                 |
+--------------------------------+
1 row in set (0.00 sec)
```

**日期天数：**

```mysql
mysql> select date_format(now(), '%d, %e, %D');
+----------------------------------+
| date_format(now(), '%d, %e, %D') |
+----------------------------------+
| 27, 27, 27th                     |
+----------------------------------+
1 row in set (0.00 sec)
```

**第几天和第几周：**

```mysql
mysql> select date_format('2018-01-01', '%j, %U, %u, %W');
+---------------------------------------------+
| date_format('2018-01-01', '%j, %U, %u, %W') |
+---------------------------------------------+
| 001, 00, 01, Monday                         |
+---------------------------------------------+
1 row in set (0.00 sec)

mysql> select date_format('2018-12-31', '%j, %U, %u, %W');
+---------------------------------------------+
| date_format('2018-12-31', '%j, %U, %u, %W') |
+---------------------------------------------+
| 365, 52, 53, Monday                         |
+---------------------------------------------+
1 row in set (0.00 sec)
```

**月份名：**

```mysql
mysql> select date_format('2018-01-01', '%M, %b, %m, %c');
+---------------------------------------------+
| date_format('2018-01-01', '%M, %b, %m, %c') |
+---------------------------------------------+
| January, Jan, 01, 1                         |
+---------------------------------------------+
1 row in set (0.00 sec)
```

**年份：**

```mysql
mysql> select date_format('2018-01-01', '%Y, %y');
+-------------------------------------+
| date_format('2018-01-01', '%Y, %y') |
+-------------------------------------+
| 2018, 18                            |
+-------------------------------------+
1 row in set (0.00 sec)
```

**date_add(date, interval expr type) 函数：** 返回与所给日期 date 相差 INTERVAL 的时间段的日期。

其中 INTERVAL 是间隔类型的关键字，expr 是一个表达式，正数表示向后加这个间隔，负数则表示向前减去这个间隔。这个表达式对应后面的类型，type 是间隔类型，MySQL 提供了 13 种间隔类型，如下表：



|  表达式类型   |    描述    |
| :-----------: | :--------: |
|     hour      |    小时    |
|    minute     |    分钟    |
|    second     |     秒     |
|     year      |     年     |
|     month     |     月     |
|      day      |     日     |
|  year_month   |   年和月   |
|   day_hour    |  日和小时  |
|  day_minute   |  日和分钟  |
|  day_second   |   日和秒   |
|  hour_minute  | 小时和分钟 |
|  hour_second  |  小时和秒  |
| minute_second |  分钟和秒  |

eg.

```mysql
mysql> select now() current, date_add(now(), interval 1 hour) after1hour;
+---------------------+---------------------+
| current             | after1hour          |
+---------------------+---------------------+
| 2018-10-28 11:22:24 | 2018-10-28 12:22:24 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval 1 minute) after1minute;
+---------------------+---------------------+
| current             | after1minute        |
+---------------------+---------------------+
| 2018-10-28 11:22:43 | 2018-10-28 11:23:43 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval 1 second) after1second;
+---------------------+---------------------+
| current             | after1second        |
+---------------------+---------------------+
| 2018-10-28 11:23:13 | 2018-10-28 11:23:14 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval 1 year) after1year;
+---------------------+---------------------+
| current             | after1year          |
+---------------------+---------------------+
| 2018-10-28 11:23:43 | 2019-10-28 11:23:43 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval 1 month) after1month;
+---------------------+---------------------+
| current             | after1month         |
+---------------------+---------------------+
| 2018-10-29 21:39:03 | 2018-11-29 21:39:03 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval 1 day) after1day;
+---------------------+---------------------+
| current             | after1day           |
+---------------------+---------------------+
| 2018-10-29 21:39:14 | 2018-10-30 21:39:14 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' year_month) after1year1month;
+---------------------+---------------------+
| current             | after1year1month    |
+---------------------+---------------------+
| 2018-10-28 11:26:11 | 2019-11-28 11:26:11 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '-1_-1' year_month) before1year1month;
+---------------------+---------------------+
| current             | before1year1month   |
+---------------------+---------------------+
| 2018-10-28 11:30:42 | 2017-09-28 11:30:42 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' day_hour) after1day1hour;
+---------------------+---------------------+
| current             | after1day1hour      |
+---------------------+---------------------+
| 2018-10-28 11:31:15 | 2018-10-29 12:31:15 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' day_minute) after1day1minute;
+---------------------+---------------------+
| current             | after1day1minute    |
+---------------------+---------------------+
| 2018-10-28 11:31:29 | 2018-10-28 12:32:29 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' day_second) after1day1second;
+---------------------+---------------------+
| current             | after1day1second    |
+---------------------+---------------------+
| 2018-10-28 11:31:42 | 2018-10-28 11:32:43 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' hour_minute) after1hour1minute;
+---------------------+---------------------+
| current             | after1hour1minute   |
+---------------------+---------------------+
| 2018-10-28 11:32:04 | 2018-10-28 12:33:04 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' hour_second) after1hour1second;
+---------------------+---------------------+
| current             | after1hour1second   |
+---------------------+---------------------+
| 2018-10-28 11:32:29 | 2018-10-28 11:33:30 |
+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> select now() current, date_add(now(), interval '1_1' minute_second) after1minute1second;
+---------------------+---------------------+
| current             | after1minute1second |
+---------------------+---------------------+
| 2018-10-28 11:32:44 | 2018-10-28 11:33:45 |
+---------------------+---------------------+
1 row in set (0.00 sec)
```

**date_sub(date, INTERVAL expr type)**：返回与所给日期date减去INTERVAL 时间段的日期。

eg.

```mysql
mysql> select now() current, date_sub(now(), interval 1 day) before1day;
+---------------------+---------------------+
| current             | before1day          |
+---------------------+---------------------+
| 2018-10-29 21:40:09 | 2018-10-28 21:40:09 |
+---------------------+---------------------+
1 row in set (0.00 sec)
```

**datediff(date1, date2):** 计算两个日期之间相差的天数。date1-date2

eg. 表示当前距离2010-09-14已经过去了2966天。

```mysql
mysql> select now() current, datediff(now(), '2010-09-14');
+---------------------+-------------------------------+
| current             | datediff(now(), '2010-09-14') |
+---------------------+-------------------------------+
| 2018-10-28 11:35:02 |                          2966 |
+---------------------+-------------------------------+
1 row in set (0.00 sec)
```



## 4. 流程函数

流程函数也是很常用的一类函数，用户可以使用这类函数在一个SQL语句中实现条件选择，这样做能够提高语句的效率。



MySQL 中的流程函数

|                            函数                            |                          功能                           |
| :--------------------------------------------------------: | :-----------------------------------------------------: |
|                      if(value, t, f)                       |            如果 value 是真，返回t；否则返回f            |
|                   ifnull(value1, value2)                   |     如果 value1 不为空，返回value1，否则返回 value2     |
|    case when [value1] then [result]...else[default] end    | 多条件判断，见eg.相当于if...else if... else if ... else |
| case [expr] when [value] then [result]...else[default] end |     多值判断，见eg. case A..;case B...;... default      |

eg.

创建职员薪水表：

```mysql
mysql> create table salary(userid int, salary decimal(9,2));
Query OK, 0 rows affected (0.08 sec)

mysql> insert into salary values(1,1000),(2,2000),(3,3000),(4,4000),(5,5000),(1,null);
Query OK, 6 rows affected (0.03 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> select * from salary;
+--------+---------+
| userid | salary  |
+--------+---------+
|      1 | 1000.00 |
|      2 | 2000.00 |
|      3 | 3000.00 |
|      4 | 4000.00 |
|      5 | 5000.00 |
|      1 |    NULL |
+--------+---------+
6 rows in set (0.00 sec)
```

**各个函数：**

```mysql
mysql> select if(salary > 2000, 'high','low') from salary;
+---------------------------------+
| if(salary > 2000, 'high','low') |
+---------------------------------+
| low                             |
| low                             |
| high                            |
| high                            |
| high                            |
| low                             |
+---------------------------------+
6 rows in set (0.00 sec)

mysql> select ifnull(salary,0) from salary;
+------------------+
| ifnull(salary,0) |
+------------------+
|          1000.00 |
|          2000.00 |
|          3000.00 |
|          4000.00 |
|          5000.00 |
|             0.00 |
+------------------+
6 rows in set (0.00 sec)

mysql> select case when salary<=2000 then 'low'  when salary<=3000 then 'middle' else 'high' end from salary;
+------------------------------------------------------------------------------------+
| case when salary<=2000 then 'low'  when salary<=3000 then 'middle' else 'high' end |
+------------------------------------------------------------------------------------+
| low                                                                                |
| low                                                                                |
| middle                                                                             |
| high                                                                               |
| high                                                                               |
| high                                                                               |
+------------------------------------------------------------------------------------+
6 rows in set (0.00 sec)

mysql> select case salary when 1000 then 'low'  when 2000 then 'middle' else 'high' end from salary;
+---------------------------------------------------------------------------+
| case salary when 1000 then 'low'  when 2000 then 'middle' else 'high' end |
+---------------------------------------------------------------------------+
| low                                                                       |
| middle                                                                    |
| high                                                                      |
| high                                                                      |
| high                                                                      |
| high                                                                      |
+---------------------------------------------------------------------------+
6 rows in set (0.00 sec)
```

## 5. 其他常用函数

|                   函数                    |          功能           |
| :---------------------------------------: | :---------------------: |
|                datebase()                 |    返回当前数据库名     |
|                 version()                 |   返回当前数据库版本    |
|                  user()                   |   返回当前登录用户名    |
|               inet_aton(ip)               |  返回ip地址的数字表示   |
|              inet_ntoa(num)               |  返回数字代表的ip地址   |
| password(str)（8.0.11版本已经移除该函数） | 返回字符串str的加密版本 |
|                 md5(str)                  |  返回字符串str的md5值   |

eg.

```mysql
mysql> select database();
+------------+
| database() |
+------------+
| db201810   |
+------------+
1 row in set (0.00 sec)

mysql> select version();
+-----------+
| version() |
+-----------+
| 8.0.11    |
+-----------+
1 row in set (0.00 sec)

mysql> select user();
+--------------------+
| user()             |
+--------------------+
| bearyang@localhost |
+--------------------+
1 row in set (0.00 sec)

mysql> select inet_aton('192.168.1.2');
+--------------------------+
| inet_aton('192.168.1.2') |
+--------------------------+
|               3232235778 |
+--------------------------+
1 row in set (0.00 sec)

mysql> select inet_ntoa(3232235778);
+-----------------------+
| inet_ntoa(3232235778) |
+-----------------------+
| 192.168.1.2           |
+-----------------------+
1 row in set (0.01 sec)

# 8.0.11 版本
mysql> select password('123456');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '('123456')' at line 1

# 5.7.22 版本
mysql> select password('123456');
+-------------------------------------------+
| password('123456')                        |
+-------------------------------------------+
| *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
+-------------------------------------------+
1 row in set, 1 warning (0.00 sec)

mysql> select md5('123456');
+----------------------------------+
| md5('123456')                    |
+----------------------------------+
| e10adc3949ba59abbe56e057f20f883e |
+----------------------------------+
1 row in set (0.00 sec)
```



## MySQL 系列：

### [1. MySQL 常用 SQL 命令（1. DDL语句）](https://github.com/YoungBear/MyBlog/blob/master/md_files/mysql/SQL-DDL.md)

### [2. MySQL 常用 SQL 命令（2. DML语句）](https://github.com/YoungBear/MyBlog/blob/master/md_files/mysql/SQL-DML.md)

### [3. MySQL 常用函数](https://github.com/YoungBear/MyBlog/blob/master/md_files/mysql/MySQL-Function.md)

### [4. MySQL 浮点数精度](https://github.com/YoungBear/MyBlog/blob/master/md_files/mysql/MySQLFloatPrecision.md)



### [更多文章](https://github.com/YoungBear/MyBlog/blob/master/README.md)

