<https://stackoverflow.com/questions/24790175/when-is-the-init-function-run>

# 问题

我试着寻找一个关于 Go 中 `init()` 函数的精确描述。我读了 [Effective Go](https://golang.org/doc/effective_go.html#init) 中的部分但我不知道理解的是否正确，就是下面这句话：

> And finally means finally: init is called after all the variable declarations in the package have evaluated their initializers, and those are evaluated only after all the imported packages have been initialized.
>
> 译：而它的结束就意味着初始化结束： 只有该包中的所有变量声明都通过它们的初始化求值后 init 才会被调用，而且该初始化求值只会在所有导入的包都被初始化之后才会执行。

句中的 `all the variable declarations in the package have evaluated their initializers`（`所有变量声明都通过它们的初始化器求值`）是什么意思？是不是说当你在软件包中声明了全局变量时，直到它被初始化求值之后才会运行所有的 init 函数，然后紧接着运行主文件中的主函数？

我也读了 Mark Summerfield 的 Go 语言书，书中写道：

> If a package has one or more init() functions they are automatically executed before the main package's main() function is called.
>
> 译：如果一个包有一个或多个 init() 函数，它们都会在主软件包的 main() 函数之前被自动调用。

我的理解是，`init()` 只于 `main()` 的运行时机相关，对吗？大家可以在 `init()` 的认识上纠正我的观点。

# 回答

是的，假设你有[这段代码](https://go.dev/play/p/dvHymTy73F)：

```go
var WhatIsThe = AnswerToLife()

func AnswerToLife() int { // 1
    return 42
}

func init() { // 2
    WhatIsThe = 0
}

func main() { // 3
    if WhatIsThe == 0 {
        fmt.Println("It's all a lie.")
    }
}
```

`AnswerToLife()` 保证会在 `init()` 执行前运行，同时 `init()` 也保证在 `main()` 之前被执行。

记住 `init()` 无论有没有 main 函数都会被调用，因此如果你导入的包中也有 `init()` 函数，那它同样会被执行。

不仅如此，你可以在一个软件包中有很多个 `init()`；它们会以在文件中出现的顺序被执行（当然在变量被初始化求值之后）。如果它们分布在多个文件中，会按文件名字典序执行（据 [@benc](https://stackoverflow.com/users/2039413/benc) 指出）：

> It seems that `init()` functions are executed in lexical file name order. The Go spec says "build systems are encouraged to present multiple files belonging to the same package in lexical file name order to a compiler". It seems that `go build` works this way.
>
> 译：看起来 `init()` 函会以文件名字典序执行。Go 语言规范指出“推荐构建系统以字典序向编译器传递同一个软件包中的多个源文件”。看来 `go build` 就是这样工作的。

# 回答

看这个图片:)

![](../images/2.3.init.png)

1. 如果一个包导入了另一个包，那么被导入的包首先被初始化。
2. 紧接着初始化当前包的常量。
3. 然后初始化当前包的变量。
4. 最后，当前包的 `init()` 被执行。

> A package can have multiple init functions (either in a single file or distributed across multiple files) and they are called in the order in which they are presented to the compiler.
>
> 译：一个包可以有多个 init 函数（无论是在一个文件还是分布在多个文件中），它们会以被传递给编译器的顺序执行。

> A package will be initialised only once even if it is imported from multiple packages.
>
> 译：一个包即使被多个包导入，也只会被初始化一次。
