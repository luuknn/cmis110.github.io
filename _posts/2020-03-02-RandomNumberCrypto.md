---
date:   2020-03-02
layout: post
title:  "容易使用的加密rand包"
tag: Random numbers
categories: Go语言学习 
---
Go 提供了两个生成随机数的包。

* [math/rand](https://golang.org/pkg/math/rand/)实现了伪随机数生成器。
* [crypto/rand](https://golang.org/pkg/crypto/rand/)使用有限的接口实现加密安全的伪随机数生成器。

```go
import (
    crand "crypto/rand"
    rand "math/rand"

    "encoding/binary"
    "fmt"
    "log"
)

func main() {
    var src cryptoSource
    rnd := rand.New(src)
    fmt.Println(rnd.Intn(1000)) // a truly random number 0 to 999
}

type cryptoSource struct{}

func (s cryptoSource) Seed(seed int64) {}

func (s cryptoSource) Int63() int64 {
    return int64(s.Uint64() & ^uint64(1<<63))
}

func (s cryptoSource) Uint64() (v uint64) {
    err := binary.Read(crand.Reader, binary.BigEndian, &v)
    if err != nil {
        log.Fatal(err)
    }
    return v
}
```