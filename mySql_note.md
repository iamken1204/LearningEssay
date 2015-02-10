# MySQL note

### 子查詢
在where條件裡面可以再下其他查詢   
```mysql
select *
from  `NEWS_ARTICLE_CLICKS`
where `NEWS_ID` in (
	select news_id
	from news_article
	where rdatetime > '2015-01-01 00:00:00'
)
order by  `NEWS_ARTICLE_CLICKS`.`NEWS_ID` desc
```
