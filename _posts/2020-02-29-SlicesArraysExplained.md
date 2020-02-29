---
date:   2020-02-29
layout: post
title:  "数组（arrays）与切片（slice）的定义"
tag: Slices and arrays
categories: Go语言学习 
---

# 基础

一个切片不会存储数据,它只是描述了底层数组的一部分

* 当更改切片的某个元素时，将修改它底层数组的相应元素，共享同一块底层数组的其他切片也会感受到变化。
* 切片可以在底层数组的范围内增长和收缩。
* 切片通常按以下方式进行索引 s[i] 访问第 i 个元素，从0开始。    

# 创建
```go
	var s []int // a nil slice
	s1 := []string{"foo", "bar"}
	s2 := make([]int, 2)          // same as []int{0, 0}
	s3 := make([]int, 2, 4)       // same as new([4]int)[:2]
	fmt.Println(len(s3), cap(s3)) // 2 4
```

* 切片的零值为 nil. 方法 len cap append 都会将 nil 视为容量为0的空片。
* 你可以通过调用 make 函数来进行切片的创建，可将长度和容量作为参数。
* 内置的方法 [len](https://golang.org/pkg/builtin/#len) 和 [cap](https://golang.org/pkg/builtin/#cap) 获取长度和容量。          

# 切片
```go
    a := [...]int{0, 1, 2, 3} // an array
	s := a[1:3]               // s == []int{1, 2}        cap(s) == 3
	s = a[:2]                 // s == []int{0, 1}        cap(s) == 4
	s = a[2:]                 // s == []int{2, 3}        cap(s) == 2
	s = a[:]                  // s == []int{0, 1, 2, 3}  cap(s) == 4
```
你可以创建一个切片通过一个已经存在的数组或切片。
* 一个切片可以通过指定上下边界s[low:hign] 来创建。这样一个切片将会选择一个包含第一个元素但不包含最后一个元素的半开范围。
* 你可以忽略低或高的界限来使用它们的默认值。默认情况下，低边界为0 高边界为该切片的长度。

```go
	s := []int{0, 1, 2, 3, 4} // a slice
	s = s[1:4]                // s == []int{1, 2, 3}
	s = s[1:2]                // s == []int{2} (index relative to slice)
	s = s[:3]                 // s == []int{2, 3, 4} (extend length)
```
当给一个切片进行切片的时候，索引是相对于切片而言的，而不是底层的数组
* 上限不是由切片的长度决定的，而是由它的容量决定的，这意味着你可以延长切片的长度。
* 尝试上限超越切片的容量，将会引发一次 panic。

# 迭代
```go
	s := []string{"Foo", "Bar"}
	for i, v := range s {
		fmt.Println(i, v)
	}
```
* 迭代值将会分配给变量 i，v 就像在赋值语句中一样。
* 第二个迭代参数是可选的。
* 如果 slice 为 nil，迭代的次数将会为0。开始循环迭代前，内部会进行一次判断。
