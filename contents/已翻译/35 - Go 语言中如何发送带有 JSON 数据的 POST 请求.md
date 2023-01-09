<https://stackoverflow.com/questions/24455147/how-do-i-send-a-json-string-in-a-post-request-in-go>

# 问题

我尝试通过以下代码用 Apiary 制作了一个通用模板来将 JSON 发送到模拟服务器：

```go
package main

import (
    "encoding/json"
    "fmt"
    "github.com/jmcvetta/napping"
    "log"
    "net/http"
)

func main() {
    url := "http://restapi3.apiary.io/notes"
    fmt.Println("URL:>", url)

    s := napping.Session{}
    h := &http.Header{}
    h.Set("X-Custom-Header", "myvalue")
    s.Header = h

    var jsonStr = []byte(`
{
    "title": "Buy cheese and bread for breakfast."
}`)

    var data map[string]json.RawMessage
    err := json.Unmarshal(jsonStr, &data)
    if err != nil {
        fmt.Println(err)
    }

    resp, err := s.Post(url, &data, nil, nil)
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println("response Status:", resp.Status())
    fmt.Println("response Headers:", resp.HttpResponse().Header)
    fmt.Println("response Body:", resp.RawText())

}
```

这段代码并不能正确的发送 JSON 数据，但我不知道为什么。JSON 字符串每一次都不一样所以我没法使用 `struct`。

# 回答

我不太熟悉 napping，但使用 Golang 的 `net/http` 包是正常的（[playground](http://play.golang.org/p/Qpob4Yu3wG)）：

```go
func main() {
    url := "http://restapi3.apiary.io/notes"
    fmt.Println("URL:>", url)

    var jsonStr = []byte(`{"title":"Buy cheese and bread for breakfast."}`)
    req, err := http.NewRequest("POST", url, bytes.NewBuffer(jsonStr))
    req.Header.Set("X-Custom-Header", "myvalue")
    req.Header.Set("Content-Type", "application/json")

    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    fmt.Println("response Status:", resp.Status)
    fmt.Println("response Headers:", resp.Header)
    body, _ := ioutil.ReadAll(resp.Body)
    fmt.Println("response Body:", string(body))
}
```