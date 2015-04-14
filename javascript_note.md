# Javascript 學習筆記

## 語法

### `on()`
[參考](http://www.ladesign.tw/paper/info/jquery_bind_delegate)

### 取得cookie
[參考](http://stackoverflow.com/questions/10730362/get-cookie-by-name)   
原生js取得cookie的方式是`document.cookie`，但是這樣會取回字串，很不方便   
如果不想用lib，想用原生方式以key取值的話：
```javascript
function getCookie(name) {
	var value = "; " + document.cookie;
	var parts = value.split("; " + name + "=");
	if (parts.length == 2)
		return parts.pop().split(";").shift();
}
```


### `isNaN()`
判斷是否"**不是數字**"   


		isNaN('hello'); // true   
		isNaN(NaN); // true   
		isNaN(undefined); // true   
		isNaN(42); //false   
		**inNaN('42'); //false   **
		
### 宣告陣列

`var list = [1, 32, 44];`   
`var multiArray = [1, true, "Hello", Car={cc:1000}];`
`var twoDimenitonal = [ [2,3,4], ['tt','jj'], [true, false, false] ];`   
   
### 找出陣列中是否包含某字串   
```javascript
var array = [2, 5, 9];
var index = array.indexOf(2);
// index is 0
index = array.indexOf(7);
// index is -1
index = array.indexOf(9, 2);
// index is 2
index = array.indexOf(2, -1);
// index is -1
index = array.indexOf(2, -3);
// index is 0
```   
   
### 宣告物件

```javascript
var phoneBook = {};
phoneBook.name = 'Annie';
phoneBook.number = "1234-6677";
phoneBook.phone() = funciton() {
	console.log("Calling " + phoneBook.name + " at  " + phoneBook.number + ".");
}
phoneBook.phone();
```   
   

```javascript
var me = {
	name: "Kettan",
	age: 25
}
```


```javascript
var myName = new Object{}; // new a Object
var myName = {}; // new a empty object
myName["name"] = "Ezreal";     <=>     myName.name = "Ezreal";
```

### js的迴圈continue與break
```javascript
//在loop裡面
return ;      // continue
return false; // break
```   
   
### 取得時間
```javascript
var d = new Date(),
    year = d.getFullYear(),
    mon = d.getMonth(),
    day = d.getDate(),
    h = d.getHours(),
    i = d.getMinutes(),
    s = d.getSeconds();
```
[參考](http://www.w3schools.com/jsref/jsref_obj_date.asp)

=======
## Design Pattern

### Cache -1
在物件裡面,cache的方式   
先用`$panel`記住`$('.panel-body')`這個區塊,之後用`$panel.find`找裡面的dom   
如果沒有cache的話,每次宣告`$('.panel-body')`都會從文件最上方開始找   
```javascript
var _videoControl = function(o) {
	o.init = function() {
		$panel = $('.panel-body');
		# ...
		$panel.find('.video-play').click(function(e) {
			# ...
		});
	}

	o.on_loadstart = function() {
		$panel.find('.video-controls').hide();
	}
}
```    

======
## some common questions

### 傳送PHP字串(含有'或"的變數)給javascript變數接
[參考](http://stackoverflow.com/questions/168214/pass-a-php-string-to-a-javascript-variable-and-escape-newlines)   
```javascript
var myvar = <?php echo json_encode($myVarValue); ?>;
```
