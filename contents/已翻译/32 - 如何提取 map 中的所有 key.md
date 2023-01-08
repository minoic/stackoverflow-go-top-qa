<https://stackoverflow.com/questions/21362950/getting-a-slice-of-keys-from-a-map>

# 问题

Go 中有没有什么更简单优雅的方式获取 map 中所有的 key 为一个切片？

目前我只能遍历 map 并且将 key 挨个复制进切片：

```go
i := 0
keys := make([]int, len(mymap))
for k := range mymap {
    keys[i] = k
    i++
}
```

# 回答

这是个老问题了，但我想说一下我的观点。PeterSO 的回答稍微简单但少了点性能，你已经知道数据规模所以并不需要用 append 了：

```go
keys := make([]int, len(mymap))

i := 0
for k := range mymap {
    keys[i] = k
    i++
}
```

在大部分情况下这也没什么区别，但也不麻烦，而且在我的测试中（用一个包含 100w 个 `int64` 键的 map 生成键序列，两个方法各十次），直接声明切片长度要比插入药快大约 20%。

虽然设置容量避免了内存重新分配，但插入仍然会导致一些额外的操作来检查每次插入时是否打到了容量上限。
