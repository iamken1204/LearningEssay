# GO language

### golang's basic types
```
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // uint8 的別名

rune // int32 的別名
     // 代表一個Unicode碼

float32 float64

complex64 complex128
```

### add items into array dynamically
```go
// declare an empty array
arr := []int{}
// add new items into array dynamically
arr = append(arr, 55)
arr = append(arr, 99)
fmt.Println(arr[1])
```

### declare a map(like php's key-value array)
```go
type Post struct {
    id      integer
    title   string
    context string
}
p1 := Post{1, "hello", "world!"}
p2 := Post{2, "I am", "golang!"}
posts := []Post{p1, p2}
fmt.Println(posts[0].title)
// out put I am
```

### `goapp`
> If you want to develop a web app by golang, there is a localhost server called `goapp` which were made by Google.[(for more info, check here)](https://developers.google.com/appengine/downloads?hl=es#Google_App_Engine_SDK_for_Go)   

__How to use__   
1. [Install go app](https://developers.google.com/appengine/downloads?hl=es#Google_App_Engine_SDK_for_Go)   
2. `$ cd $GOPATH/path/to/your/app/`
__example: `$ cd $GOPATH/src/github.com/gin-gonic/gin/examples/`__   
3. `$ goapp serve your_app_folder_name`
__example: `$ goapp serve app-engine/`__   
4. open `localhost:8080`   

* Google App Engine is in `localhost:8000`
* goapp is in `localhost:8080` by default

### multiple insert
[ref(see the most pushed-up answer)](http://stackoverflow.com/questions/12486436/golang-how-do-i-batch-sql-statements-with-package-database-sql)
```go
func BulkInsert(unsavedRows []*ExampleRowStruct) error {
    valueStrings := make([]string, 0, len(unsavedRows))
    valueArgs := make([]interface{}, 0, len(unsavedRows) * 3)
    for _, post := range unsavedRows {
        valueStrings = append(valueStrings, "(?, ?, ?)")
        valueArgs = append(valueArgs, post.Column1)
        valueArgs = append(valueArgs, post.Column2)
        valueArgs = append(valueArgs, post.Column3)
    }
    stmt := fmt.Sprintf("INSERT INTO my_sample_table (column1, column2, column3) VALUES %s", strings.Join(valueStrings, ","))
    _, err := db.Exec(stmt, valueArgs...)
    return err
}
```

### about `_`
All values you had declared __must__ be used in golang. If the return value from a func you will not use at this time, you can declare the value as `_` to tell golang to ignore it.
```go
func test(val int) (int, int) {
    x = val * 99
    y = x - 99
    return
}

func main() {
    x, _ := test(100)
    fmt.Pringf("The value is %d.", x)
    // The value is 9900.
}
```
