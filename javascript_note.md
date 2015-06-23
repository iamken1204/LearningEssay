# Javascript 學習筆記

## 語法

### `includes()` `test()` 尋找某字串是否內含字串
[ref](http://stackoverflow.com/questions/1789945/how-can-i-check-if-one-string-contains-another-substring)
```javascript
var str = 'foo';
console.log(str.includes('oo'));
// output true
```
__OR__ use regular expression to search
```javascript
var ur1 = 'http://hello.com',
    ur2 = 'shttp://hello.co';
/^http.*/.test(ur1);  // true    '^' means there are no words before target word
/^http.*/.test(ur2);  // false   '.*' means can be any words
/.*http.*/.test(ur2); // true
```

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

### object pattern
```javascript
$(function() {
	var youtubeList = function(o) {
		var self = o;
		var init = function() {
			self.$el = $(self.el);
			self.$el.find('.btn').each(function(idx, obj) {
				conosle.log($(this));
			});
			return self;
		}
		o.hello = function() {
			alert('a');
		}
		return init();
	}({el:'#test', target: 'aaaaa'});
	youtubeList.hello();
});
```

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

### add DOM by jQuery
[ref](http://stackoverflow.com/questions/2202269/best-way-to-add-dom-elements-with-jquery)
```javascript
$('<input/>', {
	id: 'user_id',
	name: 'user_id',
	value: $('input[name=ui]').attr('data-xx')
}).appendTo('form');
```

### 傳送PHP字串(含有'或"的變數)給javascript變數接
[參考](http://stackoverflow.com/questions/168214/pass-a-php-string-to-a-javascript-variable-and-escape-newlines)   
```javascript
var myvar = <?php echo json_encode($myVarValue); ?>;
```

### set default select option by jQuery
[ref](http://stackoverflow.com/questions/13343566/set-select-option-selected-by-value)
```html
<div class="group">
  <select>
    <option>A</option>
    <optin>B</option>
  </select>
</div
```
```javascript
$('div.group select').val('B');
```
