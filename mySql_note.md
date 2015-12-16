# MySQL note

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
