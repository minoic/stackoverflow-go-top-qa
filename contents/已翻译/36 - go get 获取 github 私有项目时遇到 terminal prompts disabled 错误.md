<https://stackoverflow.com/questions/32232655/go-get-results-in-terminal-prompts-disabled-error-for-github-private-repo>

# 问题

我通过浏览器中的 GitHub 界面创建了一个私有仓库 examplesite/myprivaterepo。

然后在桌面端目录中 clone 它：

```shell
$ cd $GOPATH
$ go get github.com/examplesite/myprivaterepo
```

到目前为止都很好，创建 scheduler.go，添加 repo，并 push。

```shell
$ vim scheduler.go
$ git add scheduler.go
$ git commit
$ git push
```

所有都正常，但当我用另一台干净的笔记本试着 clone 这个仓库时，出现了报错：

```shell
# 现在是笔记本，它并未接触过这个 repo
$ cd $GOPATH
$ go get github.com/examplesite/myprivaterepo
# 现在应该向我询问用户名和密码了对吧？但它并没有这么做
# 而是出现了如下报错：
cd .; git clone https://github.com/examplesite/myprivaterepo /Users/tom/go/src/github.com/examplesite/myprivaterepo
Cloning into '/Users/tom/go/src/github.com/examplesite/myprivaterepo'...
fatal: could not read Username for 'https://github.com': terminal prompts disabled
package github.com/examplesite/myprivaterepo: exit status 128
```

我的笔记本为何对我的私人仓库如此反感？怎么样才能让它接受这样的命运？谢谢。

# 回答

我发现了一个非常有用的方法，解决了我的问题。这个指令可以让你用两步验证来解决（避免了输入用户名密码的问题）：

GitHub：

```shell
git config --global --add url."git@github.com:".insteadOf "https://github.com/"
```

GitLab：

```shell
git config --global --add url."git@gitlab.com:".insteadOf "https://gitlab.com/"
```

来源：[http://albertech.blogspot.com/2016/11/fix-git-error-could-not-read-username.html](http://albertech.blogspot.com/2016/11/fix-git-error-could-not-read-username.html)

如果你不用两步验证，也可以用 SSH 正常工作。

之后 `.gitconfig` 会变成类似下面的样子：

```
[url "git@github.com:"]
    insteadOf = https://github.com
```