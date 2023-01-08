<https://stackoverflow.com/questions/13792254/removing-packages-installed-with-go-get>

# 问题

我在了解到需要设置 `GOPATH` 来避免弄乱 Go 安装根目录之前就运行 `go get package` 下载了包（我想保持 Go 安装目录干净且与自定义文件分开），如何删除以前安装的包？

# 回答

直接删除源文件和包编译文件是安全的。源文件目录在 `$GOPATH/src`，包文件在 `$GOPATH/pkg/<architecture>`，比如：`$GOPATH/pkg/windows_amd64`。
