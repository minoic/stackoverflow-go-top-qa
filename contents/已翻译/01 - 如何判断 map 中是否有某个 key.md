<https://stackoverflow.com/questions/2050391/how-to-check-if-a-map-contains-a-key-in-go>

# 问题

我知道以下方式可以遍历 map `m`

```go
for k, v := range m { ... }
```

并查找一个 key，但有没有更高效的方法来判断 map 中是否有某个 key？

# 回答

简单来说：

```go
if val, ok := dict["foo"]; ok {
    //do something here
}
```

## 解释

Go 中的 `if` 语句可以同时包含初始化和判断表达式，就像上面的例子：

- 初始化两个变量：`val` 会接收 map 中关于键“foo”的值或者一个“零值”（在这里应为空字符串）而 `ok` 会接收一个 bool 类型变量，它代表“foo”是否存在于这个 map。
- 判断 `ok`，它会在“foo”存在于这个 map 时为 `true`

如果“foo”存在，`if` 语句的主体会被执行，并且 `val` 会在这个作用域可用。