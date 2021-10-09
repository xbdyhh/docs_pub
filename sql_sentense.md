

# sql语句常用

## myql 安装

`docker pull mysql`

`docker images`

`docker run -d -e MYSQL_ROOT_PASSWORD=<root password> --name mysql -v /data/mysql/data:/var/lib/mysql -p 3306:3306 mysql`

## 数据库

`create database school` 创建一个名为school 的数据库

`drop database <数据库名>`

`use school;`

## 表

### 增加

`CREATE TABLE table_name (column_name column_type);

```
CREATE TABLE IF NOT EXISTS `student`(
   `id` INT UNSIGNED AUTO_INCREMENT,
   `name` VARCHAR(100) NOT NULL,
   `sex` VARCHAR(40) NOT NULL,
   `class` Char(10) NOT NULL,
   `birthday` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

引擎和charset一般使用默认就可以

`INSERT INTO table_name ( field1, field2,...fieldN ) VALUES  ( value1, value2,...valueN );`增加数据

```
ALTER TABLE <table_name> DROP <column_name>;
ALTER TABLE <table_name> ADD <column_name><colum_type>;
ALTER TABLE <table_name> Change <column_name><column_new_name><colum_type>;



```



### 删除：

`DROP TABLE <table_name> ;`

```
DELETE FROM table_name [WHERE Clause]
```

查询数据：

```
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]`
LIMIT限制查询数量，比如limit 50就是只返回前50个
offset表示偏移量，比如offset 50就是从第50个开始返回
limit 和 offset配合排序使用就可以实现分页
select * 表示选择所有列
```

```
SELECT name,id
form school
where sex = male AND(OR) birthday = 2020-01-11
注意：大于于等于,小于等于为>==，<==
```

```
LIKE 子句，用于在where中代替=，实现模糊匹配，%表示任意字符，需注意xxx%效率要高于%xxx
ORDER by + column_name + asc(desc) 实现排序
```

```
GROUP by用法
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;

例如：
SELECT name, SUM(class) as class_count FROM  school GROUP BY name WITH ROLLUP;
coalesce(a,b,c)用于返回一个非空的值
常用函数：AVG count LEAST GREATEST
```

更改数据：

```
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

## 事务

```
begin 		开始一个事务
commit 		提交一个事务
rollback	回滚一个事务
```

## 数据类型：

| 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
| :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
| TINYINT      | 1 Bytes                                  | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 Bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 Bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 Bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 Bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 Bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 Bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

| 类型      | 大小 ( bytes) | 范围                                                         | 格式                | 用途                     |
| :-------- | :------------ | :----------------------------------------------------------- | :------------------ | :----------------------- |
| DATE      | 3             | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3             | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1             | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8             | 1000-01-01 00:00:00/9999-12-31 23:59:59                      | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4             | 1970-01-01 00:00:00/2038结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYYMMDD HHMMSS     | 混合日期和时间值，时间戳 |



| 类型       | 大小                  | 用途                            |
| :--------- | :-------------------- | :------------------------------ |
| CHAR       | 0-255 bytes           | 定长字符串                      |
| VARCHAR    | 0-65535 bytes         | 变长字符串                      |
| TINYBLOB   | 0-255 bytes           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                    |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535 bytes        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                    |
