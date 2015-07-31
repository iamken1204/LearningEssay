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

### about `fmt.Print*`
```go
s := "sss"
d := 199
v := []int{1, 2}
fmt.Printf("string: %s, int: %d, value:%v\n", s, d, v)
// output:
// string: sss, int: 199, value:[1 2]
fmt.Println("string: %s, int: %d, value:%v\n", s, d, v)
// output:
// string: %s, int: %d, value:%v
//  sss 199 [1 2]
arr := []string{"i", "am", "ken"}
fmt.Printf("arr = %q", arr)
// output:
// arr = ["i" "am" "ken"]
```

===

### about `array`

###### declare an array
```go
func main() {
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1])
	fmt.Println(a)
}

```

###### declare a two-dimensional array
```go
func main() {
	a := make([][]int, 10)
	fmt.Printlnl(a)
	// output:
	// [[] [] [] [] [] [] [] [] [] []]
	// as above, the array a's default value is nil and cannot be used
	a[0] = make([]int, 10))
	fmt.Printlnl(a)
	// output:
	// [[0 0 0 0 0 0 0 0 0 0] [] [] [] [] [] [] [] [] []]
}
```

###### add items into array dynamically
```go
// declare an empty array
var arr []int
// add new items into array dynamically
arr = append(arr, 55)
arr = append(arr, 99, 777)
fmt.Println(arr)
// output:
// [55 99 777]
```

###### new a slice
```go
func main {
	a := make([]int, 5, 10) 
	// len(a) = 5, cap(a) = 10
	// len must not be bigger than cap
	fmt.Printf("%v", a)
	// output:
	// [0 0 0 0 0]
	
	var z []int
	fmt.Println(z, len(z), cap(z))
	if z == nil {
		fmt.Println("z is nil!")
	}
	// output:
	// [] 0 0
	// nil!
}
```

###### slicing slices
The expression `s[low:high]` evaluates to a slice of the elements from low through high-1, inclusive.
```go
func main() {
	s := []int{1, 2, 3, 4, 5, 6}
	fmt.Println("s ==", s)
	// output:
	// s == [1 2 3 4 5 6]
	fmt.Println("s[1:4] ==", s[1:4])
	// output:
	// s[1:4] == [2, 3, 4]

	// missing low index implies 0
	fmt.Println("s[:3] ==", s[:3])
	// output:
	// s[:3] == [1 2 3]

	// missing high index implies len(s)
	fmt.Println("s[4:] ==", s[4:])
	// output:
	// ss[4:] == [5 6]
}
```

===

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

###### attach fun() to a struct
```go
type Fib struct {
	prev, next, sum int
}
func (f Fib) Operation() Fib {
	f.sum = f.prev + f.next
	f.prev, f.next = f.next, f.sum
	return f
}
func main() {
	f := Fib{0, 1, 0}
	for i := 0; i < 10; i++ {
		f = f.Operation()
		fmt.Println(f.sum)
	}
}
// output:
// 1
// 2
// 3
// 5
// 8
// 13
// 21
// 34
// 55
// 89
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

###### `new()`
`v := new(Vertex)` eaquls to `var v *T = new(Vertex)`
```go
type Vertex struct {
    X, Y int
}

func main() {
    v := new(Vertex)
    fmt.Println(v)
    v.X, v.Y = 11, 9
    fmt.Println(v)
}
// output:
// &{0, 0}
// &{11, 9}
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

### golang's foreach `range `
```go
var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

func main() {
	for idx, val := range pow {
		fmt.Printf("index = %d, value = %d\n", idx, val)
	}
}
// output:
// index = 0, value = 1
// index = 1, value = 2
// index = 2, value = 4
// index = 3, value = 8
// index = 4, value = 16
// index = 5, value = 32
```
* ignore index, declare as `for _, val := range pow {}`
* ignore value, declare as `for idx := range pow {}`

### about `defer`, golang's `try catch`
[ref](http://polor10101.gitbooks.io/golang_note/content/defer_panic_recover.html)

### about `map`

###### declare a map
```go
m := make(map[string]int)
// or
m := map[string]int{}
```

###### delete a map, check map's value is exist
```go
m := map[string]int{}
m["age"] = 16
delete(m, "age")
value, ok := m["age"]
fmt.Println(value, ok)
// output:
// 0 false
```

###### declare multi maps in one time
```go
type Post struct {
	id    int
	title string
}

func main() {
person := map[string]Post{
       "age" : {16, "h"},
       "ago" : {27, "i"},
       "agi" : {38, "j"},
    }
fmt.Println(person)
fmt.Println(person["age"])
}
// output:
// map[age:{16 h} ago:{27 i} agi:{38 j}]
// {16 h}
```

###### a tour of go's map exercise
[exercise is here](http://tour.golang.org/moretypes/19)   
my answer:
```go
package main

import (
	"golang.org/x/tour/wc"
	"strings"
)

func WordCount(s string) map[string]int {
	ss := strings.Fields(s)
	m := map[string]int{}
	for _, val := range ss {
		m[val] = m[val] + 1
	}
	return m
}

func main() {
	wc.Test(WordCount)
}
```
===

### about golang's `interface`

###### a tour of go's stringer exercise
[exercise is here](http://tour.golang.org/methods/7)   
my answer[(run in playground)](http://play.golang.org/p/K6YkbCL-Ia):
```go
package main

import "fmt"

type IPAddr [4]byte

func (ia IPAddr) String() string {
	var res string
	for i, v := range ia {
		switch {
		case i < len(ia) - 1:
			res += fmt.Sprintf("%v.", v)
		default:
			res += fmt.Sprintf("%v", v)
		}
	}
	return fmt.Sprintf(res)
}

func main() {
	addrs := map[string]IPAddr{
		"loopback":  {127, 0, 0, 1},
		"googleDNS": {8, 8, 8, 8},
	}
	for idx, val := range addrs {
		fmt.Printf("%v: %v\n", idx, val)
	}
	// output:
	// googleDNS: 8.8.8.8
	// loopback: 127.0.0.1
}
```
__NOTE__   
The func `String()` rewrite `fmt`'s `Stringer` _interface_[(reference here)](http://tour.golang.org/methods/6).   
Originally you use `fmt.Printf("%v", val)` only prints the pure value of parameter, however, in this exercise, I implement `Stringer`'s content `String()` so that I can output ip value as `"127.0.0.1"` instead of `[127, 0, 0, 1]`.

===

### about golang's `error`

###### __type: `error`__, __func: `Error()`__
The `error` type is a built-in interface similar to `fmt.Stringer`,   
and the `error` type returns error message as string by it's func `Error()`.
```go
type error interface {
	Error() string
}
```

### An example of custom error implementation
[ref](http://tour.golang.org/methods/8)
```go
package main

import (
	"fmt"
	"time"
)

type MyError struct {
	When time.Time
	What string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v: %s", e.When, e.What)
}

func report() error {
	return &MyError{
		time.Now(),
		"Something went wrong!",
	}
}

func main() {
	if err := report(); err != nil {
		fmt.Println(err)
	}
	// output:
	// at 2009-11-10 23:00:00 +0000 UTC: Something went wrong!
}
```

###### a tour of go's error exercise
[excise is here](http://tour.golang.org/methods/9)
my answer:
```go
package main

import "fmt"

type ErrNegativeSqrt float64

func (e ErrNegativeSqrt) Error() string {
	return fmt.Sprintf("cannot Sqrt negative number: %g", float64(e))
}

func Sqrt(x float64) (float64, error) {
	if x < 0 {
		return 0, ErrNegativeSqrt(x)
	}
	return 0, nil
}

func main() {
	fmt.Println(Sqrt(2))
	fmt.Println(Sqrt(-2))
}
```

===
