# MySQL note

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
