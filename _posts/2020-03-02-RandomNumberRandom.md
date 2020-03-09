---
date:   2020-03-02
layout: post
title:  "生成随机数、字符和切片元素"
tag: Random numbers
categories: Go语言学习 
---

# Go伪随机数
可以使用 [math/rand](https://golang.org/pkg/math/rand/) 包内的 [rand.Seed](https://golang.org/pkg/math/rand/#Seed) 和 [rand.Int63](rand.Int63) 方法来生成一个非负的int64型的伪随机数。

```go
	rand.Seed(time.Now().UnixNano())
	n := rand.Int63() // for example 4601851300195147788
```
同样的，可以调用 rand.Float64 来生成一个浮点数 a , 0 ≤ a < 1

```go
	x := rand.Float64() // for example 0.49893371771268225
```
### 随机源
[math/rand](https://golang.org/pkg/math/rand/) 包内的方法都使用同一个随机源。

如果需要，您可以自己设置一个随机种子并创建一个新的[Rand](https://golang.org/pkg/math/rand/#Rand)类型的随机生成器，并用它的方法来生成随机数。

```go
		generator := rand.New(rand.NewSource(time.Now().UnixNano()))
		n := generator.Int63()
		x := generator.Float64()

```


# 给定范围内生成随机数或字符

### a 到 b 之间的数字

调用函数 [rand.Intn(m)](rand.Intn(m)) 将会返回随机数 n ，并且 0 ≤ n < m.

```go
		n := a + rand.Intn(b-a+1) // a ≤ n ≤ b
```

### a 到 z 之间的字符

```go
		c := 'a' + rune(rand.Intn('z'-'a'+1)) // 'a' ≤ c ≤ 'z'
```


# 随机切片元素
可以通过选定一个随机的索引来从任意一个切片中生成一个字符。

```go
		chars := []rune("AB⌘")
		c := chars[rand.Intn(len(chars))] // for example '⌘'
```






