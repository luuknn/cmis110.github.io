---
date:   2020-03-02
layout: post
title:  "Runes and character encoding"
tag: Strings
categories: Go语言学习 
---

ASCII码定义128个字符，由代码点0-127标识。它包括英文字母、拉丁数字和其他一些字符。

Unicode是ASCII的一个超集，它定义了一个包含1,114,112个码点的codespace。Unicode版本10.0包含139个现代和历史脚本(包括runic字母表，但不包括Klingon)，以及多个符号集。


# Strings and UTF-8 encoding

字符串是字节序列 并不是 rune 序列。

但是，字符串通常包含用UTF-8编码的Unicode文本，它使用1到4个字节对所有Unicode码点进行编码。(ASCII字符用一个字节编码，而其他代码点用得更多。)

由于Go源代码本身被编码为UTF-8，字符串文本将自动获得这种编码。

例如，在字符串“cafe”中，字符e(代码点233)使用两个字节进行编码，而ASCII字符c、a和f(代码点99、97和102)只使用一个字节

```go
		fmt.Println([]byte("café")) // [99 97 102 195 169]
		fmt.Println([]rune("café")) // [99 97 102 233]
```


# []byte 与 []rune
```go
		// byte is an alias for uint8 and is equivalent to uint8 in all ways. It is
		// used, by convention, to distinguish byte values from 8-bit unsigned
		// integer values.
		type byte = uint8
		
		// rune is an alias for int32 and is equivalent to int32 in all ways. It is
		// used, by convention, to distinguish character values from integer values.
		type rune = int32
```
原来是 byte 表示一个字节，rune 表示四个字节，那么就可以得出了结论了，来看一段代码，使用中文字符串.

```go
		bj := "北京欢迎你"
		fmt.Println([]rune(bj))//[21271 20140 27426 36814 20320]
		fmt.Println([]byte(bj))//[229 140 151 228 186 172 230 172 162 232 191 142 228 189 160]
```
这里可以看出中文字符串每个占3个字节。

```go
		res := []rune("北京欢迎你")
		fmt.Println(string(res[:2]))//北京
```

