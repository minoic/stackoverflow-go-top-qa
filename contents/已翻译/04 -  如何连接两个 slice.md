<https://stackoverflow.com/questions/16248241/concatenate-two-slices-in-go>

# 问题

我想试着合并切片 `[1, 2]` 和切片 `[3, 4]`，在 Go 中应该怎么做？

我尝试使用：

```go
append([]int{1,2}, []int{3,4})
```

但只得到：

```go
cannot use []int literal (type []int) as type int in append
```

但 [文档](https://pkg.go.dev/builtin#append) 中貌似说这是可行的，我错在哪里？

```go
slice = append(slice, anotherSlice...)
```

# 回答

在第二个切片中添加三个点

```go
//                           vvv
append([]int{1,2}, []int{3,4}...)
```

这就像其它可 [可变参数函数](https://go.dev/doc/go1.17_spec#Passing_arguments_to_..._parameters) 那样：

```go
func foo(is ...int) {
    for i := 0; i < len(is); i++ {
        fmt.Println(is[i])
    }
}

func main() {
    foo([]int{9,8,7,6,5}...)
}
```