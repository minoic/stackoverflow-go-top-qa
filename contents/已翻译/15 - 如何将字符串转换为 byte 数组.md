<https://stackoverflow.com/questions/8032170/how-to-assign-string-to-bytes-array>

# 问题

我希望将字符串转换为 byte 数组：

```go
var arr [20]byte
str := "abc"
for k, v := range []byte(str) {
  arr[k] = byte(v)
}
```

有其他的办法吗？

# 回答

安全又简单：

```go
[]byte("Here is a string....")
```

## 补充

Go 代码中的最佳实践是在将字符串转换为 bytes 时使用 `[]byte` 切片，而不是 `[20]byte` 数组。不相信我？可以看看 Rob Pike 的 [回答](https://groups.google.com/forum/#!topic/golang-nuts/84GCvDBhpbg) 
