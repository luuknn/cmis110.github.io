---
date:   2020-03-01
layout: post
title:  "获取年月日"
tag: Time and date
categories: Go语言学习 
---

函数[Date](https://golang.org/pkg/time/#Time.Date)用于返回 [time.Time](https://golang.org/pkg/time/#Time)的年月日信息。

```go
func (t Time) Date() (year int, month Month, day int)
```

使用:  

```go
	year, month, day := time.Now().Date()
	fmt.Println(year, month, day)      // For example 2020 March 1
	fmt.Println(year, int(month), day) // For example 2009 3 1
```
 
也可以单独调用提取相应的年月日：

```go
	t := time.Now()
	year := t.Year()   // type int
	month := t.Month() // type time.Month
	day := t.Day()     // type int
```
 
 [time.Month]用来表示一年中的月份，比如一月份 January = 1...
 
 ```go
     const (
        January Month = 1 + iota
        February
        March
        April
        May
        June
        July
        August
        September
        October
        November
        December
    )
 ```
 


