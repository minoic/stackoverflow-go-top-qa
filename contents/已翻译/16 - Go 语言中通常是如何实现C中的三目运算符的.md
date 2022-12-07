<https://stackoverflow.com/questions/19979178/what-is-the-idiomatic-go-equivalent-of-cs-ternary-operator>

# 问题

在 C/C++ （或其它 C 系语言）中，通常用三木运算符来有条件地声明并初始化一个变量。

```c
int index = val > 0 ? val : -val
```

Go 中没有相应的运算符。通常如何实现和上面相似的功能？

我只能想到一个很繁琐的办法：

```go
var index int

if val > 0 {
    index = val
} else {
    index = -val
}
```

有没有更好的方式？

# 回答

正如你所说的（是不是很惊讶），使用 `if+else` 确实就是 Go 中实现三目运算符的惯用方法。

但除了完整的 `var+if+else` 代码块之外，下面的方式也很常用：

```go
index := val
if val <= 0 {
    index = -val
}
```

而如果你的代码块重复性比较高，比如它等价于 `int value = a <= b ? a : b`，你可以创建函数来复用它：

```go
func min(a, b int) int {
    if a <= b {
        return a
    }
    return b
}

...

value := min(a, b)
```

编译器会内联这些简单的函数，所以这种方式快速、清晰且简便。