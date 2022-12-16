<https://stackoverflow.com/questions/15323767/does-go-have-if-x-in-construct-similar-to-python>

# 问题

我该如何在**不**遍历整个数组的情况下，判断 `x` 是否在数组中？Go 语言中有这种设计吗？

就像在 Python 中的：

```python
if "x" in array: 
  # do something
```

# 回答

Go 中没有内建的这种操作。你需要遍历整个数组来实现。也可以像这样编写自定义函数：

```go
func stringInSlice(a string, list []string) bool {
    for _, b := range list {
        if b == a {
            return true
        }
    }
    return false
}
```

或者在 Go 1.18 或更新的版本中，可以使用 [`slice.Contains`](https://pkg.go.dev/golang.org/x/exp/slices#Contains)（golang.org/x/exp/slices）。

如果需要在不遍历整个列表的情况下检查存在性，你需要的是字典而不是数组或切片，像这样：

```go
visitedURL := map[string]bool {
    "http://www.google.com": true,
    "https://paypal.com": true,
}
if visitedURL[thisSite] {
    fmt.Println("Already been here.")
}
```