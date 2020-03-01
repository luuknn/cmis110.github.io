---
date:   2020-02-29
layout: post
title:  "删除切片元素的2种方法"
tag: "Slices and arrays"
categories: Go语言学习 
---

# 快速版本（改变顺序）

```go
	a := []string{"A", "B", "C", "D", "E"}
	i := 2

	// Remove the element at index i from a.
	a[i] = a[len(a)-1] // Copy last element to index i.
	a[len(a)-1] = ""   // Erase last element (write zero value).
	a = a[:len(a)-1]   // Truncate slice.

	fmt.Println(a) // [A B E D]
```
这段代码拷贝了一个元素，时间复杂度为常数阶。

# 慢速版本（保持顺序）
```go
a := []string{"A", "B", "C", "D", "E"}
i := 2

// Remove the element at index i from a.
copy(a[i:], a[i+1:]) // Shift a[i+1:] left one index.
a[len(a)-1] = ""     // Erase last element (write zero value).
a = a[:len(a)-1]     // Truncate slice.

fmt.Println(a) // [A B D E]
```   
这段代码拷贝了 len(a)-i-1个元素，时间复杂度为线性阶。
