# Javascript 學習筆記

## 語法

>
### `isNaN()`
判斷是否"**不是數字**"   

>
		isNaN('hello'); // true   
		isNaN(NaN); // true   
		isNaN(undefined); // true   
		isNaN(42); //false   
		**inNaN('42'); //false   **
		
### 宣告陣列
>
`var list = [1, 32, 44];`   
`var multiArray = [1, true, "Hello", Car={cc:1000}];`
`var twoDimenitonal = [ [2,3,4], ['tt','jj'], [true, false, false] ];`   

### 宣告物件
>
```
var phoneBook = {};
phoneBook.name = 'Annie';
phoneBook.number = "1234-6677";
phoneBook.phone() = funciton() {
	console.log("Calling " + phoneBook.name + " at  " + phoneBook.number + ".");
}
phoneBook.phone();
```   
   
>
```
var me = {
	name: "Kettan",
	age: 25
}
```

>
```
var myName = new Object{}; // new a Object
var myName = {}; // new a empty object
myName["name"] = "Ezreal";     <=>     myName.name = "Ezreal";
```


