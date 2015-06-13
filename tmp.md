# ADMIN.alert.show()

## How to use
The state of `ADMIN.alert.show()` separates to __2__ condition:

#### __redirect by controller__
>
Add `#action/status` followed by the redirect url.   
Parameters:   
* __action__   
    * `create` // will print out '新增'   
    * `update` // will print out '修改'   
    * `delete` // will print out '刪除'   
* __status__   
    * `success` // background-color: green    
    * `error`   // background-color: red   
```php
return $this->redirect(['mail/index#create/success']);
```

#### __alert by js__
>
Replace `alert()` by `ADMIN.alert.show(message, status, duration)` in js.   
Parameters:   
* __message__   
  The message you want to show.   
* __status__   
    Color of alert box   
    * `success` // green   
    * `warning` // yellow   
    * `danger`  // red   
* __duration__   
    Determine alert box's remain time, Unit: second, default is 5 seconds.   
    If duration is set to '0', it means the alert box will not close automatically.   
*
```javascript
ADMIN.alert.show('新增成功', 'warning', 0);
```
