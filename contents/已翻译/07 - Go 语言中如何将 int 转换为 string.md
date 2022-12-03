<https://stackoverflow.com/questions/10105935/how-to-convert-an-int-value-to-string-in-go>

# 问题

```go
i := 123
s := string(i) 
```

s 值为'E'，但我想得到"123"

请告诉我如何得到“123”。

并且我在 Java 中可以这样做：

```go
String s = "ab" + "c"  // s is "abc"
```

我在 Go 中应如何 `连接` 两个字符串？

# 回答

使用 [`strconv`](http://golang.org/pkg/strconv/#Itoa) 包中的 `Itoa` 函数。

比如：

```go
package main

import (
    "strconv"
    "fmt"
)

func main() {
    t := strconv.Itoa(123)
    fmt.Println(t)
}
```

你可以很简单的用 `+` 运算符连接字符串，或用 [`strings`](http://golang.org/pkg/strings/#Join) 包中的 `Join` 函数。