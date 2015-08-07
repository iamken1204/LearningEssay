# PHP Example of big mount of db insert

```php
<?php

namespace app\commands;

use Yii,
    yii\console\Controller,
    Exception,
    app\models\iptv\IptvUsers,
    app\models\user\Users,
    app\models\user\UserIsch;

Class IptvMemberController extends Controller
{
    private $error = [];

    public function actionImport() {
        $fromDb = Yii::$app->db2;
        $toDb = Yii::$app->db;
        $auth = Yii::$app->authManager;
        $role = $auth->getRole('member');


        $sqlFormat = 'select * from user_users where id > %d order by id asc limit %d';

        $max = 3301957;
        $limit = 1000;
        $bool = true;
        $total = 0;
        while($bool) {
            $sql = sprintf($sqlFormat, $max, $limit);
            $count = 0;
            $fromDb->close();
            $dr = $fromDb->createCommand($sql)->query();
            try {
                $transaction = $toDb->beginTransaction();
                $ischs = [];
                $users = [];
                while($r=$dr->read()) {
                    $data = $this->parseMember($r);

                    $toDb->createCommand()->insert('user_users', $data)
                                          ->execute();

                    $ischs[] = [
                        'user_id' => $r['id'],
                        'account' => $r['yam_id'],
                        'password' => sha1($r['password']),
                        'status' => 1
                    ];


                    // $auth->assign($role, $data['id']);
                    $count++;
                    $max = (int) $data['id'];
                    echo '.';
                }

                echo "\n";
                while($r=array_shift($ischs)) {
                    $toDb->createCommand()->insert('user_isch', $r)
                                          ->execute();
                    $users[] = $r['user_id'];
                    echo '#';
                }

                echo "\n";
                while($r=array_shift($users)) {
                    $auth->assign($role, $r);
                    echo '*';
                }


                $total += $count;
                echo sprintf("\n==========\nfinished total: %d, max: %d\n==========\n", $total, $max);
                $transaction->commit();


            } catch (Exception $e) {
                echo $e->getMessage();
                echo sprintf("\n==========\nError total: %d, max: %d\n==========\n", $total, $max);
                $transaction->rollback();
            }


            if ($count<$limit)
                $bool = false;
            else
                usleep(100000*rand(2, 8));
        }
    }

    private function parseMember($row) {
        $uDatas = [];

        //pro birthday, add date
        if ( !empty($row['birthday']) )
            $bitCmd = explode(' ', $row['birthday']);

        if ( !empty($row['add_date']) )
            $addDCmd = explode(' ', $row['add_date']);
        //pro education
        $education = null;
        switch ($row['education']) {
            case '國中以下（含國中）':
                $education = 1;
                break;
            case '大學':
                $education = 4;
                break;
            case '大專、學院或大學':
                $education = 4;
                break;
            case '專科':
                $education = 3;
                break;
            case '研究所及以上':
                $education = 5;
                break;
            case '高中(職)':
                $education = 2;
                break;
            case '高中(職)以下':
                $education = 1;
                break;
            case '高中或高職':
                $education = 2;
                break;
        };
        //pro income
        $income = null;
        $incomeCmd = (int) str_replace(',', '', $row['income']);

        if ( $incomeCmd != 0 ){
            $income = ( $incomeCmd < 19000 ) ? 1 : null;
            $income = ( $incomeCmd > 19000 && $incomeCmd < 29000 ) ? 2 : $income;
            $income = ( $incomeCmd > 29000 && $incomeCmd < 49000 ) ? 3 : $income;
            $income = ( $incomeCmd > 49000 && $incomeCmd < 69000 ) ? 4 : $income;
            $income = ( $incomeCmd > 70000 ) ? 5 : $income;
        }
        //pro marriage
        $marriage = null;
        switch ($row['marriage']) {
            case '已婚':
                $marriage = 1;
                break;
            case '未婚':
                $marriage = 0;
                break;
        }
        //pro children
        $children = null;
        switch ($row['children']) {
            case '有':
                $children = 1;
                break;
            case '無':
                $children = 0;
                break;
        }
        // $um = new Users;
        $uDatas = [
            'id' => $row['id'],
            'name' => $row['name'],
            'nick_name' => $row['nick_name'],
            'email' => $row['email'],
            'phone' => !empty($row['phone']) ? $row['phone'] : null,
            'postal_code' => !empty($row['postal_code']) ? $row['postal_code'] : null,
            'address' => !empty($row['address']) ? $row['address'] : null,
            'country' => !empty($row['country']) ? $row['country'] : null,
            'area' => !empty($row['area']) ? $row['area'] : null,
            'birthday' => (!empty($row['birthday'])) ? date('Y-m-d', strtotime($bitCmd[0])) : null,
            'gender' => ($row['gender'] = '女' ) ? 0 : 1,
            'education' => $education,
            'income' => $income,
            'marriage' => $marriage,
            'children' => $children,
            'status' => 1,
            'member_status' => 1,
            'created_at' => (!empty($row['add_date'])) ? date('Y-m-d H:i:s', strtotime($addDCmd[0] . ' ' . $addDCmd[2])) : date('Y-m-d H:i:s'),
            'updated_at' => (!empty($row['add_date'])) ? date('Y-m-d H:i:s', strtotime($addDCmd[0] . ' ' . $addDCmd[2])) : date('Y-m-d H:i:s')
        ];

        unset($row);
        return $uDatas;
    }


    private function saveMember($offset, $limit) {
        $iptvMembers = IptvUsers::find()->orderBy(['id'=>SORT_ASC])->offset($offset)->limit($limit)->all();

        $uDatas = [];
        $uiDatas = [];
        foreach ($iptvMembers as $key => $row) {
            //pro birthday, add date
            $bitCmd = explode(' ', $row['birthday']);
            $addDCmd = explode(' ', $row['add_date']);
            //pro education
            $education = null;
            switch ($row['education']) {
                case '國中以下（含國中）':
                    $education = 1;
                    break;
                case '大學':
                    $education = 4;
                    break;
                case '大專、學院或大學':
                    $education = 4;
                    break;
                case '專科':
                    $education = 3;
                    break;
                case '研究所及以上':
                    $education = 5;
                    break;
                case '高中(職)':
                    $education = 2;
                    break;
                case '高中(職)以下':
                    $education = 1;
                    break;
                case '高中或高職':
                    $education = 2;
                    break;
            };
            //pro income
            $income = null;
            $incomeCmd = (int) str_replace(',', '', $row['income']);

            if ( $incomeCmd != 0 ){
                $income = ( $incomeCmd < 19000 ) ? 1 : null;
                $income = ( $incomeCmd > 19000 && $incomeCmd < 29000 ) ? 2 : $income;
                $income = ( $incomeCmd > 29000 && $incomeCmd < 49000 ) ? 3 : $income;
                $income = ( $incomeCmd > 49000 && $incomeCmd < 69000 ) ? 4 : $income;
                $income = ( $incomeCmd > 70000 ) ? 5 : $income;
            }
            //pro marriage
            $marriage = null;
            switch ($row['marriage']) {
                case '已婚':
                    $marriage = 1;
                    break;
                case '未婚':
                    $marriage = 0;
                    break;
            }
            //pro children
            $children = null;
            switch ($row['children']) {
                case '有':
                    $children = 1;
                    break;
                case '無':
                    $children = 0;
                    break;
            }
            // $um = new Users;
            $uDatas[] = [
                'id' => $row['id'],
                'name' => $row['name'],
                'nick_name' => $row['nick_name'],
                'email' => $row['email'],
                'phone' => !empty($row['phone']) ? $row['phone'] : null,
                'postal_code' => !empty($row['postal_code']) ? $row['postal_code'] : null,
                'address' => !empty($row['address']) ? $row['address'] : null,
                'country' => !empty($row['country']) ? $row['country'] : null,
                'area' => !empty($row['area']) ? $row['area'] : null,
                'birthday' => date('Y-m-d', strtotime($bitCmd[0])),
                'gender' => ($row['gender'] = '女' ) ? 0 : 1,
                'education' => $education,
                'income' => $income,
                'marriage' => $marriage,
                'children' => $children,
                'status' => 1,
                'member_status' => 1,
                'created_at' => date('Y-m-d H:i:s', strtotime($addDCmd[0] . ' ' . $addDCmd[2])),
                'updated_at' => date('Y-m-d H:i:s', strtotime($addDCmd[0] . ' ' . $addDCmd[2])),
            ];

            $uiDatas[] = [
                'user_id' => $row['id'],
                'account' => $row['yam_id'],
                'password' => UserIsch::generatePassword($row['password']),
                'status' => 1
            ];

            //assign role
            $auth = Yii::$app->authManager;
            $role = $auth->getRole('member');
            $auth->assign($role, $row['id']);

            echo ".";
        }
        $uField = ['id','name','nick_name','email','phone','postal_code','address','country','area','birthday','gender','education','income','marriage','children','status','member_status','created_at','updated_at'];
        $uSql = Yii::$app->db->createCommand()->batchInsert('user_users', $uField, $uDatas)->execute();

        $uiField = ['user_id','account','password','status'];
        $uiSql = Yii::$app->db->createCommand()->batchInsert('user_isch', $uiField, $uiDatas)->execute();

        echo $offset . '-' . ( $offset + $limit ) . ' Success!!' . "\n";
    }
}
```
