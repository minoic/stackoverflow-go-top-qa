<https://stackoverflow.com/questions/1841443/iterating-over-all-the-keys-of-a-map>

# 问题

在 Go 语言中有没有获取 map 中所有 key 的方法？元素个数可以通过 `len()` 获得，当我有一个这样的 map 时：

```go
m := map[string]string{ "key1":"val1", "key2":"val2" }
```

我该如何遍历所有的 key？

# 回答

[https://play.golang.org/p/JGZ7mN0-U-](https://play.golang.org/p/JGZ7mN0-U-)

```go
for k, v := range m { 
    fmt.Printf("key[%s] value[%s]\n", k, v)
}
```

或者

```go
for k := range m {
    fmt.Printf("key[%s] value[%s]\n", k, m[k])
}
```

[Go 语言规范中的 `for` 语句](http://golang.org/ref/spec#For_statements) 指出，第一个变量为键，第二个变量为值且可以忽略。

