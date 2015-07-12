# GO language

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
