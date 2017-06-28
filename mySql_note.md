# MySQL note

### You can't specify target table for INSERT/UPDATE/DELETE in FROM clause
[ref](https://stackoverflow.com/questions/4429319/you-cant-specify-target-table-for-update-in-from-clause)   
You cannot manipulate a table by reference the same table in subquery.   
Instead of:
```sql
UPDATE my_table
SET my_table.aaa = (
	SELECT bbb
	FROM my_table
	...
)
```
use:
```sql
UPDATE my_table
SET my_table.aaa = (
	SELECT bbb
	FROM (SELECT * FROM my_table) AS something
	...
)
```


### Show partition information
```sql
SELECT *
FROM information_schema.partitions
WHERE table_name = table_name;
```

### Show all indexes within a specific table
```sql
SHOW INDEXES
FROM table_name;
```

### Difference between `WHERE` and `HAVING`
[ref](http://www.mysql.tw/2014/06/sqlwherehaving.html)
* Quries with no `GROUP BY`, use `WHERE` only
* Quries with `GROUP BY`, use `WHERE` before `GROUP BY`, then follow `HAVING`
* `HAVING` only accetp the target that related with `GROUP BY`

An example from [leetcode](https://leetcode.com/problems/duplicate-emails/),   
query from a table that:
```
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```
the result should be:
```
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
```
```sql
SELECT Email
FROM Person
GROUP BY Email
HAVING count(Email) > 1;
```

### `mysqldump` specific tables or excepted tables [ref](http://dba.stackexchange.com/questions/9306/how-do-you-mysqldump-specific-tables)
* Dump specific tables
```shell
mysqldump -u -p yourdb table1 table2 table3 > table_1_2_3.sql
```
* Dump tables without the excepted
```shell
DBTODUMP=mydb
SQL="SET group_concat_max_len = 10240;"
SQL="${SQL} SELECT GROUP_CONCAT(table_name separator ' ')"
SQL="${SQL} FROM information_schema.tables WHERE table_schema='${DBTODUMP}'"
SQL="${SQL} AND table_name NOT IN ('t1','t2','t3')"
TBLIST=`mysql -u... -p... -AN -e"${SQL}"`
mysqldump -u... -p... ${DBTODUMP} ${TBLIST} > mydb_tables.sql
```

### 特定情境處理方法
* 想要根據不重複 `account` __並且__找出最新 (`id` 最大) 的資料   
`group by` 預設並不會找最新一筆，所以要用 `max()` 強迫 DB query 出符合需要的資料
```mysql
select id, account, data
from consumer_data
where id in (
    select MAX(id)
    from consumer_data
    group by account
)
and id < %d
ORDER BY `id` DESC
limit %d
```

### 子查詢
在where條件裡面可以再下其他查詢   
```mysql
select *
from  `ARTICLE_CLICKS`
where `ARTICLE_ID` in (
	select article_id
	from article
	where datetime > '2015-01-01 00:00:00'
)
order by  `ARTICLE_CLICKS`.`ARTICLE_ID` desc
```

### Another subquery
```mysql
select *
from (
    select * from participants_kettan
    group by awarded_title_id
) as tmp
group by zip_code
```
__Note__ that subquery in `()` must be assigned a alias.   

### 減少更新資料時的query次數

```mysql
-- transaction start --
SELECT `example` FROM `test` WHERE ID = :ID;
UPDATE `test` SET `example` = n WHERE ID = :ID;
-- commit transaction --

-- 可以變成↓ --

-- transaction start --
UPDATE `test` SET `example` = `example` - '1' WHERE `example` > 0;
-- commit transaction 
```
