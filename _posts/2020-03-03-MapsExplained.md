---
date:   2020-03-03
layout: post
title:  "map的创建、添加、获取和删除"
tag: Maps
categories: Go语言学习 
---

Go中的map在底层是用哈希表实现的，它具有高效的添加、获取和删除操作。

# 创建一个新的 map

```go
	var m map[string]int                // nil map of string-int pairs
	
	m1 := make(map[string]float64)      // Empty map of string-float64 pairs
	m2 := make(map[string]float64, 100) // Preallocate room for 100 entries
	
	m3 := map[string]float64{           // Map literal
	    "e":  2.71828,
	    "pi": 3.1416,
	}
	fmt.Println(len(m3))                // Size of map: 2
```

* 一个 map一组键值对的无序集合，每个键值都是唯一的。
* 你可以通过 [make](https://golang.org/pkg/builtin/#make) 关键字来创建一个 map。
* map的零值为 nil。一个值为nil的 map除了不能添加元素外和一个空的 map 是等效的。如果你试图往一个尚未初始化的 map 中添加元素，将会引发运行时的 panic。
* [len](https://golang.org/pkg/builtin/#len) 函数可以获取到 map 的大小，即键值对的总数量。


# map的添加、更新、获取和删除
```go
	m := make(map[string]float64)
	
	m["pi"] = 3.14             // Add a new key-value pair
	m["pi"] = 3.1416           // Update value
	fmt.Println(m)             // Print map: "map[pi:3.1416]"
	
	v := m["pi"]               // Get value: v == 3.1416
	v = m["pie"]               // Not found: v == 0 (zero value)
	
	_, found := m["pi"]        // found == true
	_, found = m["pie"]        // found == false
	
	if x, found := m["pi"]; found {
	    fmt.Println(x)
	}                           // Prints "3.1416"
	
	delete(m, "pi")             // Delete a key-value pair
	fmt.Println(m)              // Print map: "map[]"
```

* 当你索引一个map时，你会得到两个返回值;第二个(可选)是一个布尔值，指示键是否存在。
* 如果键不存在的话，第一个返回值将会是默认的[零值](https://yourbasic.org/golang/default-zero-value/)


# 循环遍历map
```go
	m := map[string]float64{
	    "pi": 3.1416,
	    "e":  2.71828,
	}
	fmt.Println(m) // "map[e:2.71828 pi:3.1416]"
	
	for key, value := range m { // Order not specified 
	    fmt.Println(key, value)
	}
```
* 迭代顺序没有指定，并且可能因迭代而异。
* 如果在迭代期间删除了尚未到达的条目，则不会产生相应的迭代值。
* 如果一个条目是在迭代期间创建的，那么这个条目可能在迭代期间产生，也可能不产生。

# map的性能与实现
* map的底层是由hash table实现。
* 添加、获取和删除操作在恒定的预期时间内运行。添加操作的时间复杂度是平摊的。
* 必须为键类型定义运算符 ==和!=。


