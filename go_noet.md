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

### about `struct`

###### declare a struct(like php's key-value array)
```go
type Post struct {
    id      int
    title   string
    context string
}
p1 := Post{1, "hello", "world!"}
p2 := Post{2, "I am", "golang!"}
posts := []Post{p1, p2}
fmt.Println(posts[0].title)
// out put I am
```

###### struct pointer
```go
type Vertex struct {
    X int
    Y int
}

func main() {
    p := Vertex{1, 2}
    q := &p
    q.X = 1e9
    fmt.Println(p)
}
// output:
// {1000000000 2}
```

===

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

### go version php's `var_dump()`
```go
import fmt

var (
    ten    int  = 10
    DoWork bool = true
)

func main() {
    const pattern = "%T(%v)\n"
    fmt.Printf(pattern, 10, 10)
    fmt.Printf(pattern, DoWork, DoWork)
    // output:
    // int(10)
    // bool(true)
    // %T will output paremeter's type
    // %v will output paremeter's value
}
```

### about `for`
* basic `for`
```go
func main() {
    sum := 0
    for i := 0; i < 10; i++ {
        sum += i
    }
    fmt.Println(sum)
}
// output:
// 45
```
* `for` can omit the __first__ and the __final__ parameters
```go
func main() {
    sum := 1
    for ; sum < 10; {
        fmt.Println(sum)
        sum += sum
    }
    fmt.Println(sum)
}
// output:
// 1
// 2
// 4
// 8
// 16
```
* `for` is golang's `while`, either
```go
func main() {
    sum := 1
    for sum < 1000 {
        sum += sum
    }
    fmt.Println(sum)
}
// output:
// 1024
```

### about `if` `else`
There can place a single-line operation before judgement in golang's `if`
```go
func test(x, y int) string {
    ref := ""
    // the v parameter can use in if operation only
    if v := x - y; v > 0 {
        ref = "x>y"
    } else if v == 0 {
        ref = "x=y"
    } else {
        ref = "x<y"
    }
    return ref
}

func main() {
    fmt.Println(test(10, 10))
    // output:
    // x=y
}
```
