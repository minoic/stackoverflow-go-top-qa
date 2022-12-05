<https://stackoverflow.com/questions/14230145/how-can-i-convert-a-zero-terminated-byte-array-to-string>

# 问题

我需要读取 `[100]byte` 来传输一堆 `string` 数据。

由于并不是所有 `string` 的长度都是 100 个字符，`byte` 数组中的剩余部分是 `0`。

如果我用 `string(byteArray[:])` 将 `[100]byte` 转换为 `string`，尾部的 `0` 将会显示为一些 `^@^@`。

在 C 语言中，`string` 会以 `0` 结尾，所以 Go 语言中将 `byte` 字符串转换为 `string` 的最好的方式是什么？

# 回答

将数据读取到 byte 数组的函数都会返回一个数字表示读取到多少个字节，你需要将这个数字保存下来以便创建字符串。假设 `n` 代表读取的字节数，你的代码应该是下面这样：

```go
s := string(byteArray[:n])
```

若要整个转换为字符串，可以使用：

```go
s := string(byteArray[:len(byteArray)])
```

它等价于：

```go
s := string(byteArray[:])
```

如果你确实不知道 `n` 是多少，可以使用 `bytes` 包来获取，假设你的输入中没有空字符：

```go
n := bytes.Index(byteArray[:], []byte{0})
```

或：

```go
n := bytes.IndexByte(byteArray[:], 0)
```