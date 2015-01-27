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

### 創造時間變數
```php
$dateTime = date("Y-m-d H:i:s", mktime(date('H'), date('i'), date('s'), date('m'), date('d'), date('Y')));
// 順序為: h時 i分 s秒 m月 d日 Y年   時可為 h->十二小時制度 H->二十四小時制
$time = date("ah:i:s");
// "ah"的a用來顯示"am"或"pm"
```   
   
### 修改已存在的時間
如果要幫 `$time = "2014-12-24"` 加3個月的話
[參考](http://stackoverflow.com/questions/10724305/how-to-add-1-month-on-a-date-without-skipping-i-e-february)
```php
$time = "2014-12-24";
$addMon = 3;
$preTime = $time;
$nextTime = strtotime("+$addMon month", strtotime($preTime));
$time = date("Y-m-d", $nextTime);
echo $time;
// 輸出2015-06-24
```

### 時間戳記加減運算
```php
$a = '2015-01-20 07:00:00';
$b = '2015-01-20 20:00:00';
$c = strtotime($b)-strtotime($a);
echo gmdate("H:i:s", $c);
// 輸出13:00:00
```

======
## some common questions

### 傳送PHP字串(含有'或"的變數)給javascript變數接
[參考](http://stackoverflow.com/questions/168214/pass-a-php-string-to-a-javascript-variable-and-escape-newlines)   
```javascript
var myvar = <?php echo json_encode($myVarValue); ?>;   
```   

### 操作 `cookie`、`session` 之前不能輸出網頁內容   
如:   
不能   
```php
echo 'aaa';
setcookie(...);
```   
不能
```php
<p>Hello</p>
<?php
setcookie(...);
?>
```   
[參考](http://blog.xuite.net/vexed/tech/26406775-PHP+%E9%8C%AF%E8%AA%A4+-+headers+already+sent)
