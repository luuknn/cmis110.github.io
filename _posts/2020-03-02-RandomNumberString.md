---
date:   2020-03-02
layout: post
title:  "生成随机字符串（密码）"
tag: Random numbers
categories: Go语言学习 
---

# 随机字符串
从瑞典字母(包括非ascii字符å, ä 和 ö))中生成随机的数字和字符字符串。

```go
		rand.Seed(time.Now().UnixNano())
		chars := []rune("ABCDEFGHIJKLMNOPQRSTUVWXYZÅÄÖ" +
			"abcdefghijklmnopqrstuvwxyzåäö" +
			"0123456789")
		length := 8
		var b strings.Builder
		for i := 0; i < length; i++ {
			b.WriteRune(chars[rand.Intn(len(chars))])
		}
		str := b.String() // E.g. "PsVwäDFU"
```

# 带约束的随机字符串
以下代码演示生成一个随机ASCII字符串，该字符串至少包含一个数字和一个特殊字符。

```go
		rand.Seed(time.Now().UnixNano())
		digits := "0123456789"
		specials := "~=+%^*/()[]{}/!@#$?|"
		all := "ABCDEFGHIJKLMNOPQRSTUVWXYZ" +
			"abcdefghijklmnopqrstuvwxyz" +
			digits + specials
		length := 8
		buf := make([]byte, length)
		buf[0] = digits[rand.Intn(len(digits))]
		buf[1] = specials[rand.Intn(len(specials))]
		for i := 2; i < length; i++ {
			buf[i] = all[rand.Intn(len(all))]
		}
		rand.Shuffle(len(buf), func(i, j int) {
			buf[i], buf[j] = buf[j], buf[i]
		})
		str := string(buf) // E.g. "$Lu2y/6+"
```





