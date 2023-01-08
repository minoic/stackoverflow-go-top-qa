<https://stackoverflow.com/questions/4278430/convert-string-to-integer-type-in-go>

# 问题

我正在尝试在 Go 中将 `flag.Arg(n)` 返回的字符串转换为 `int`，通常应该用什么方法？

# 回答

使用 [`strconv.Atoi`](http://golang.org/pkg/strconv/#Atoi)。

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    s := "123"

    // string to int
    i, err := strconv.Atoi(s)
    if err != nil {
        // ... handle error
        panic(err)
    }

    fmt.Println(s, i)
}
```