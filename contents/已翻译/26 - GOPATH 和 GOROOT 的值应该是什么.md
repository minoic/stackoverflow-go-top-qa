<https://stackoverflow.com/questions/7970390/what-should-be-the-values-of-gopath-and-goroot>

# 问题

我正在尝试这样安装 [doozer](https://github.com/ha/doozer)：

```shell
goinstall github.com/ha/doozer
```

但提示这些报错：

```shell
goinstall: os: go/build: package could not be found locally
goinstall: fmt: go/build: package could not be found locally
goinstall: io: go/build: package could not be found locally
goinstall: reflect: go/build: package could not be found locally
goinstall: math: go/build: package could not be found locally
goinstall: rand: go/build: package could not be found locally
goinstall: url: go/build: package could not be found locally
goinstall: net: go/build: package could not be found locally
goinstall: sync: go/build: package could not be found locally
goinstall: runtime: go/build: package could not be found locally
goinstall: strings: go/build: package could not be found locally
goinstall: sort: go/build: package could not be found locally
goinstall: strconv: go/build: package could not be found locally
goinstall: bytes: go/build: package could not be found locally
goinstall: log: go/build: package could not be found locally
goinstall: encoding/binary: go/build: package could not be found locally
```

# 回答

`GOPATH` 在 [`cmd/go` 文档中](http://golang.org/cmd/go/#hdr-GOPATH_environment_variable) 被提及：

> `GOPATH` 环境变量指出查找 Go 代码的路径。在 Unix 中，它是用冒号分隔的字符串。在 Windows 中，它是用分号分隔的字符串。在 Plan 9 中，它是一个列表。
>
> `GOPATH` 必须被设置以用于获取、构建和安装标准 Go 之外的库。

`GOROOT` 在 [安装引导](http://golang.org/doc/install#tarball_non_standard) 中被提及：

> Go 二进制发行版会假设被安装在 `/usr/local/go` (或 Windows 中的 `C:\Go`)，但也可以在其它地方安装 Go 工具。此时就必须设置 `GOROOT` 环境变量来指出安装位置。
> 
> 例如，如果你将 Go 安装在 home 目录则需要在 `$HOME/.profile` 中添加如下指令：
> 
> ```shell
> export GOROOT=$HOME/go
> export PATH=$PATH:$GOROOT/bin
> ```
> 
> **注意：**`GOROOT` 只有在自定义安装目录时才必须被设置。
