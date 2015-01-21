#### An essay for my learning.
   
   
   

YMoney Project
================================

YMoney website rebuild with Yii2.0.


CONFIGURATION
-------------

* __NOTE__ The folders are under app/web/money_admin/images and theirs files should be set as property:0777.   
* Check /www/money_admin/images has a folder named __newsBighead__, if not, create one.   
* Database   

>
server: __Pro-money__ dbname: __money__   
|       url       |       ac       |       pw       |     remark     |
|:---------------:|:--------------:|:--------------:|:--------------:|
|    10.1.2.10    |       rd2      |     rd2rd2     | For creating app's db account|
|                 |      money     |     money      |   Dev account  |


DIRECTORY STRUCTURE
-------------------

      assets/             contains assets definition
      commands/           contains console commands (controllers)
      config/             contains application configurations
      controllers/        contains Web controller classes
      models/             contains model classes
      modules/admin       money backend
      vendor/             contains dependent 3rd-party packages
      views/              contains view files for the Web application
      web/                contains the entry script and Web resources


REQUIREMENTS
------------

The minimum requirement by this application template that your Web server supports PHP 5.4.0.


Developers
----------

_Eric Huang_

_Kettan Wu_

_Leo Wang_

_Rex Chen_
