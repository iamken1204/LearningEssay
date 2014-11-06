# How to set an new Yii2.0 project on nginx Linux

## 設置
* 下載一個yii專案壓縮檔.tgz
* `tar zxvf yii-basic-app-2.0.0.tgz`
* 把`assets`, `runtime`, `web/assets`權限設成777
* 把`config/web.php`的`request`改成:
```
'request' => [
            // !!! insert a secret key in the following (if it is empty) - this is required by cookie validation
            'enableCsrfValidation' => false,
            'enableCookieValidation' => false,
            'cookieValidationKey' => '',
        ],
```
* enjoy!
