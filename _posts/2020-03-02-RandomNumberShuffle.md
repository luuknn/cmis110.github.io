---
date:   2020-03-02
layout: post
title:  "打乱切片或数组的顺序"
tag: Random numbers
categories: Go语言学习 
---
[math/rand](https://golang.org/pkg/math/rand/) 包中方法 [rand.Shuffle](https://golang.org/pkg/math/rand/#Shuffle) 会通过指定的交换函数打乱数组的输入序列即进行洗牌。

```go
		a := []int{1, 2, 3, 4, 5, 6, 7, 8}
		rand.Seed(time.Now().UnixNano())
		rand.Shuffle(len(a), func(i, j int) { a[i], a[j] = a[j], a[i] })
		fmt.Println(a) //[4 7 6 1 3 5 8 2]

```

#### Go 1.10 之前
会使用  [math/rand](https://golang.org/pkg/math/rand/) 包中的 [rand.Seed](https://golang.org/pkg/math/rand/#Seed) 和 [rand.Intn](https://golang.org/pkg/math/rand/#Intn) 函数来打乱切片的顺序。

```go
		a := []int{1, 2, 3, 4, 5, 6, 7, 8}
		rand.Seed(time.Now().UnixNano())
		for i := len(a) - 1; i > 0; i-- { // Fisher–Yates shuffle
		    j := rand.Intn(i + 1)
		    a[i], a[j] = a[j], a[i]
		}
```