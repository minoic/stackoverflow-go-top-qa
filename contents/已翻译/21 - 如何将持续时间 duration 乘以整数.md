<https://stackoverflow.com/questions/17573190/how-to-multiply-duration-by-integer>

# 问题

为测试并发 goroutines，我在函数中添加了一行来让函数在随机延迟（最大一秒）后返回。

```go
time.Sleep(rand.Int31n(1000) * time.Millisecond)
```

但是当我编译时会报错：

> .\crawler.go:49: invalid operation: rand.Int31n(1000) * time.Millisecond (mismatched types int32 and time.Duration)

这是怎么回事？怎么样才能将持续时间乘以整数？

# 回答

`int32` 和 `time.Duration` 是不同的类型。你需要将 `int32` 强制转换为 `time.Duration`：

```go
time.Sleep(time.Duration(rand.Int31n(1000)) * time.Millisecond)
```