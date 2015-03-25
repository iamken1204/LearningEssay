# 使用Selenium搞定前端測試

* PHP也有Day#13 2015-03-12
* [Selenium官網](http://www.seleniumhq.org)
   


* Selenium IDE不支援輸出php錄製碼...使用[PHP-Formatter-PHPUnit_Selenium2](https://github.com/suzuki/PHP-Formatter-PHPUnit_Selenium2)
  
* 搭配__firefox__使用最方便，不需額外下載driver
   
* Selenium server 127.0.0.1:4444
   
* 可以執行javascript並取得回傳值
   
* [PHPUnit](https://phpunit.de)官方4.5版已內建phpunit-selenium
   
* 測試流程：
  1. 開啟selenium server `$ java -jar selenium-server-standalone-2.45.0.jar`
  2. `$ phpunit your_test.php`
  

