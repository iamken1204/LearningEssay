#PHP Note

## 語法

### parent
If you override parent class' function and want to run with old function, use `parent::yourFunctionName();`   
```php
class A
{
	public function printing()
	{
		echo "a.printing() ";
	}
}

class B extends A
{
	public function printing()
	{
		parent::printing();
		echo "b.printing()";
	}
}

$b = new B;
$b->printing();
// a.printing() b.printing()
```

### getcwd()
取得目前執行之檔案的絕對路徑
```php
echo getcwd();
```

### curl
example of issuing a post request
```php
$cu = curl_init();
$url = 'http://kettan.dev.com/admin/post/category/test';
$data = [
    'name' => 'Kettan',
    // ...
];
$options = [
    CURLOPT_URL => $url,
    CURLOPT_POST => true,
    CURLOPT_POSTFIELDS => $data,
];
curl_setopt_array($cu, $options);
curl_exec($cu);
curl_close($cu);
```

### CLI(Command Line) Colors (bash)
[Color code is here](http://www.if-not-true-then-false.com/2010/php-class-for-coloring-php-command-line-cli-scripts-output-php-output-colorizing-using-bash-shell-colors/)   
```php
echo "\033[0;31m Your messages\033[0m \n";
// Use "\033" to tell php it's a color code.
// "[0;31m" defines which color to show, in this case, the color is light red.
// "[0m" tells php color code is stoped here, or you'll see all words be changed under your message.
```

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

### `array_values()`
把陣列的index重新訂為0~   
```php
$array = [
  'c' => 1,
  'b' => 2,
  'z' => 3
];
$rearrange = array_values($array);
// $rearrange = [
//   0 => 1,
//   1 => 2,
//   2 => 3
// ]
```

### `json_decode()` 取回(陣列|物件)的方法   
```php
json_decode($jString);         #回傳物件
json_decode($jString, true);   #回傳陣列
```

### 刪除一個已存在的cookie
[參考](http://stackoverflow.com/questions/686155/remove-a-cookie)
```php
if(isset($_COOKIE['login']))
    setcookie('login', null, -1);
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
$add_mon = 3;
$pre_time = $time;
$next_time = strtotime("+$add_mon month", strtotime($pre_time));
$time = date("Y-m-d", $next_time);
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

### 判斷一個變數是否為數字   
```php
$a = '123';
$b = 123;
$c = 'yam23';
echo is_numeric($a); // 1
echo is_numeric($b); // 1
echo is_numeric($c); // 0
```

======
## some common questions

### 移除空白
```php
$str = " This line contains\tliberal \r\n use of whitespace.\n\n";

// 移除前後空白字
$str = trim($str);

// 移除重覆的空白
$str = preg_replace('/\s(?=\s)/', '', $str);

// 移除非空白的間距變成一般的空白
$str = preg_replace('/[\n\r\t]/', ' ', $str);
```

### minutes convert to hours and minutes
[ref](http://stackoverflow.com/questions/8563535/convert-number-of-minutes-into-hours-minutes-using-php)   
[`mktime()`](http://php.net/manual/en/function.mktime.php)   
```php
date("H:i", mktime(0, $yourMinuteInteger));
```

### 關於PHP
* 電腦中PHP的位置
```shell
$ which php
```
* php.ini的路徑可以在`phpinfo();`內看到

### PHP session id
安裝PHP後，PHP compiler會根據該電腦的CPU內核(內核ID每個CPU獨一無二)與其他數據做出__session id__   
php session id是可以重設的，php compiler預設的php session id就叫php session id

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

### 將array_unique過的陣列轉成json
```php
$a = array(1,2,2,3,3);
$b = array_unique($a);                   // $b = [1,2,3]
echo json_encode($b);                    // 輸出 {"0":1,"1":2,"3":3}
echo json_encode(array_values($b));      // 輸出 [1,2,3]
```

=====
## Skills

### 傳送變數至Closure(anonymous funciton)裡
[參考](http://laravel.io/forum/03-10-2014-laravel-mailsend-does-not-appear-to-accept-variables)
```php
// 在function(...)後面加上use($parameter_you_want)
$name = 'Name';
Mail::send('email.view', [...], function($message) use($name) {...});
```

### php://input
[參考](http://stackoverflow.com/ques…/8893574/php-php-input-vs-post)   
`php://input` returns all the raw data after the HTTP-headers of the request.   
If you have a __ajax__ request with __JSON__ data, you may use 
```php
file_get_contents("php://input");
```
to get data.

### 使用php重新整理(或跳轉)頁面
[參考](http://stackoverflow.com/questions/12383371/refresh-a-page-using-php)   
```php
echo "<meta http-equiv='refresh' content='0; url='http://www.google.com'>";
```
這裡的0代表0秒跳轉   
還有另一個是`header()`，使用`header()`前頁面不能有任何輸出如`echo()`, `print_f()`等等   
```php
header("Location: http://www.google.com");
```
不過最方便的還是用js...   
```php
$url = 'www.google.com';
echo "<script>window.location.replace('$url');</script>";
```
   
### 在遞迴函式裡面使用靜態變數加快function的速度
[參考](https://speakerdeck.com/jaceju/how-to-be-a-better-php-developer)
```php
function fib($n)
{



	if($n < 2)
		return $n;
	$f[$n] = fib($n-2) + fib($n-1);
	return $f[$n];
}

echo fib(30), "\n";
```
上面這段`$f`為普通變數，執行時間__5.59556889534__秒   
下面這段把`$f`宣告為為靜態變數，執行時間__0.002144813537__秒
```php
function fib($n)
{
	static $f = array();
	if(isset($f[$n]))
		return $f[$n];
	if($n < 2)
		return $n;
	$f[$n] = fib($n-2) + fib($n-1);
	return $f[$n];
}

echo fib(30), "\n";
```

### 在雙引號字串內印出變數
```php
$juice = 'orange';

echo "I drank some juice made of $juices";    // 無法輸出$juice變數
echo "I drank some juice made of {$juice}s";  // 輸出$juice變數

// 也可以輸出陣列內容
$juice = ['orange', 'apple', 'watermelon'];
echo "I drank some juice made of {$juice[1]}s";
```

## 命名慣例

### Class
首字大寫   
```php
ConsoleController
```

### class' attribute
開頭加個`m`，其他首字大寫
```php
class HelloController
{
    var $mStrAbc;
    var $mHelloAttribute;
}
```

### function
首字小寫，其後駝峰式   
```php
function doSomeThing(){}
```

### variable
全小寫，使用`_`隔開   
```php
$first_string;
$second_string;
```

## Coding Style

### PSR-2
[參考](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)

* 純php檔案的結尾__一定__不要有`?>`
* 檔案結束後最下方__一定__要有一行空白
* 縮排__一定__要用空白，__一定不能__用tab
* class名稱宣告完成後左大括號__一定__要在其下一行，右大括號__一定__要在程式本體結束的下一行
* class的屬性與方法__一定__要宣告可視屬性`public, private, protected...`
* function名稱與params__一定__要連在一起，其後左大括號__一定__要在其下一行，右大括號__一定__要在方法本體結束的下一行
```php
<?php

class SomeClass
{
    public $ParamA = null;
    
    public $ParamB = false;
    
    public function __construct($p1, $p2, $p3 = [])
    {
        // do something
    }
}

```



