---
date:   2020-03-02
layout: post
title:  "生成一个唯一的字符串"
tag: Random numbers
categories: Go语言学习 
---

全球唯一标识符([UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier))或全球唯一标识符(GUID)是一个用于标识信息的128位数字。

* uuid实际的目的是唯一的:它被复制的可能性几乎趋于0。
* uuid 不依赖于中央权威，也不依赖于生成 uuid 的那些机构之间的协调。

UUID 字符串表现是由32个十六制数字组成，分为5组，用连接符分割。例如：

```go
	123e4567-e89b-12d3-a456-426655440000
```

# UUID生成器 举例
可以通过使用 [crypto/rand](https://golang.org/pkg/crypto/rand/) 包的 [rand.Read](https://golang.org/pkg/crypto/rand/#Read)方法来创建一个 uuid。

```go
		b := make([]byte, 16)
		_, err := rand.Read(b)
		if err != nil {
			log.Fatal(err)
		}
		uuid := fmt.Sprintf("%x-%x-%x-%x-%x",
			b[0:4], b[4:6], b[6:8], b[8:10], b[10:])
		fmt.Println(uuid) //d37a5f14-ee89-241a-43e6-ba84d527a095
```
#### 限制
这个UUID不符合[RFC 4122](https://tools.ietf.org/html/rfc4122)。特别地，它不包含任何版本号或变体号。


