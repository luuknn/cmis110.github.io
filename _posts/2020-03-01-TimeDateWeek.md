---
date:   2020-03-01
layout: post
title:  "如何找到星期几"
tag: Time and date
categories: Go语言学习 
---

函数[Weekday](https://golang.org/pkg/time/#Time.Weekday)用于返回一周中的星期几。

```go
		func (t Time) Weekday() Weekday
```

使用:

```go
		weekday := time.Now().Weekday()
		fmt.Println(weekday)      // "Tuesday"
		fmt.Println(int(weekday)) // "2"	
		
```

## Type Weekday

[time.Weekday](https://golang.org/pkg/time/#Weekday)用来描述星期 比如礼拜天 Sunday=0...

```go
type Weekday int

		const (
			Sunday Weekday = iota
			Monday
			Tuesday
			Wednesday
			Thursday
			Friday
			Saturday
		)
```


