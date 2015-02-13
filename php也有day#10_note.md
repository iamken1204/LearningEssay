# PHP也有day#10

### 開發小型專案經驗分享
* Win Wu 吳怡穎 
* github winwu

Laravel Requirement
MCrypt PHP Extension ($php -m)

`composer create-project laravel/laravel YOUR_PROJECT_NAME --prefer-dist`

`your-project-folder artisan list`

`your-project-folder artisan serve` (預設por:8000)

CSS/JS管理工具   
__Grunt__ __Gulp__

前端工具   
__Bower__

Amazon, Linode, windows Azure

Laravel hosting requirement
ssl
git
php 5.4up
php.ini複寫
.htaccess
修改your-project-name/bootstrap/paths.php路徑

前端framework
Flat UI, Bootstrap, Semantic UI

package: 
torann/geoip - 紀錄user IP的功能
laravel-debugbar(Barryvdh/Debugbar)

CSRF

catch(redis)
 -寫入catch

cheats.jesse-obrien.ca/

builtwithlaravel.com

__FTPLOY__   
接github或bitbucket

===================

### 快快樂樂用Homestead
* 陳正瑋 得寬科技   

#### Homestead 2.0
Laravel Homestead __VAGRUNT__
a command line tool
Manage virtual machine(VM)

Box + Vagrantfile-Setting Config   
 |   
VM Base Image

laravel/homestead Ubuntu 14.04
									PHP 5.6
									HHVM
									NGINX
homestead COMMAND
~/.composer/vendor/bin
~/.homestead   
`homestead up`-->create VM-->VM provision-->Run ~/.homestead/after.sh


#### Installation & Setup

|								 
|:-----------------------------:|
| Virtual Box 64bit  			 |
| Vagrant   					 |
| Add Box(larabel/homestead)   	 |
| Composer   					 |
| Homestead   					 |

`vagrant box add laravel/homestead`   

##### setup homestead.yaml
`homestead init`   
`homestead edit`   
改完設定後   
`homestead up --provision`   

##### Vagrant Cloud
有別人寫好的box   
打包vagrant   
`vagrant package --base my-virtual-machine`   
每個box都是映像檔   

##### Customized Vagrantfile
http://github.com/mcuyar/station
