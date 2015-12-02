# **PHP example of big mount query**

* Laravel [ref](http://laravel.io/forum/12-03-2014-fetching-large-numbers-of-rows)

``` php
$sql = Dog::select('name')->whereAge(0)->toSql();
// 0 is just "empty" value, it doesn't matter here yet

$db = DB::connection()->getPdo();

$query = $db->prepare($sql);
$query->execute(array(10)); // here's our puppies' real age

while ($name = $query->fetchColumn()) {
    // process data
}
```

* Yii

``` php
$query = Model::find()
			  ->where(['id' => $id])
              ->createCommand()
              ->query();
while ($r = $query->read()) {
  // process data
}
```

