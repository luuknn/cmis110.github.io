---
date:   2020-02-29
layout: post
title:  "切片或数组的3种比较方式"
tag: Slices and arrays
categories: Go语言学习 
---

# 通用案例

在大多数情况下，你将会自己编写代码来比较两个切片中的元素

```go
// Equal tells whether a and b contain the same elements.
// A nil argument is equivalent to an empty slice.
func Equal(a, b []int) bool {
	if len(a) != len(b) {
		return false
	}
	for i, v := range a {
		if v != b[i] {
			return false
		}
	}
	return true
}

```
对于数组来说，可以直接使用比较运算符 == 和 !=

```go 
	a := [2]int{1, 2}  
	b := [2]int{1, 3}  
	fmt.Println(a == b) // false
```
当数组的元素是可比较的时候，数组也是可比较的 。  
如果两个数组对应的元素是相等的那么这两个数组也是相等的，返回 true。   
[-go 语言说明：比较运算符] (https://golang.org/ref/spec#Comparison_operators)

# byte slice
我们可以使用[bytes.Equal](https://golang.org/pkg/bytes/#Equal)来比较 byte 型的切片。

# 递归比较
出于测试目的，你会选择使用[reflect.DeepEqual](https://golang.org/pkg/reflect/#DeepEqual)。它用来循环地比较两个任意类型的元素。

```go
	var a []int = nil
	var b []int = make([]int, 0)
	fmt.Println(reflect.DeepEqual(a, b)) // false
```
这个函数的性能相比上面的要差很多，但是在简单性和准确性非常严格的情况下是非常有用的。
