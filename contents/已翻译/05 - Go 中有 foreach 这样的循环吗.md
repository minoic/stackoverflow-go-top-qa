<https://stackoverflow.com/questions/7782411/is-there-a-foreach-loop-in-go>

# 问题

Go 语言中有 `foreach` 的设计吗？如何遍历一个切片或数组？

# 回答

根据 [带有 range 的 for 语句](https://go.dev/ref/spec#For_range)

> A "for" statement with a "range" clause iterates through all entries of an array, slice, string or map, or values received on a channel. For each entry it assigns iteration values to corresponding iteration variables and then executes the block.
>
> 译：带有“range”的“for”语句可以遍历数组、切片、字符串或 map，以及从 channel 中接收到的值。对于每个元素，它将所有迭代值赋值到迭代变量，然后执行语句块。

一个例子：
```go
for index, element := range someSlice {
    // index 是数组下标或其它入口，代表当前位置
    // element 是在 someSlice 中，在当前位置上的元素值
}
```

如果你不关心下标是什么，可以使用 `_`：

```go
for _, element := range someSlice {
    // element 即 someSlice 中的某个元素
}
```

下划线 `_` 即 [空标识符](https://go.dev/ref/spec#Blank_identifier)，它作为匿名占位符使用。

