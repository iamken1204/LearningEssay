#PHP Note

## 語法

### `array_unique()`
同index的重複value只保留一個   
```php
$a = [1,2,2,3];   
$b = [
	['neo'] => [4,5,5,6,7,7]
];
$a1 = array_unique($a);
$b1 = array_unique($b);
// $a1 = [1,2,3]
// $b1 = [
//    ['neo'] => [4,5,6,7]
// ]
```

### `json_decode()` 取回(陣列|物件)的方法   
```php
json_decode($jString);         #回傳物件
json_decode($jString, true);   #回傳陣列
```

### `unset()`
清除陣列
```php
$a = [1,2,3];
unset($a[1]);
// $a = [1,3];
```   
   
### 修改已存在的時間
如果要幫 `$time = "2014-12-24"` 加3個月的話
[參考](http://stackoverflow.com/questions/10724305/how-to-add-1-month-on-a-date-without-skipping-i-e-february)
```php
$time = "2014-12-24;
$addMon = 3;
$preTime = $time;
$nextTime = strtotime("+$addMon month", strtotime($pretime));
$time = date("Y-m-d", $nextTime);
echo $time
// 輸出2015-06-24
```

