---
date:   2020-03-01
layout: post
title:  "日期格式化"
tag: Time and date
categories: Go语言学习 
---

# 基本示例

Go 没有采用 yyyy-mm-dd 的展现来格式化时间，而是采用了一个特殊的时间格式  
　　　<font color=#008000> Mon Jan 2 15:04:05 MST 2006 </font>   
同样格式的时间可以被解析。这个特使的时间格式可以按下面这种方式方便记忆 　<font color=#008000>　2006-01-02 15:04  </font> 

```go
	const (
		layoutISO = "2006-01-02"
		layoutUS  = "January 2, 2006"
	)
	date := "2020-02-29"
	t, _ := time.Parse(layoutISO, date)
	fmt.Println(t)                  // 2020-02-29 00:00:00 +0000 UTC
	fmt.Println(t.Format(layoutUS)) // February 29, 2020
```  

函数     

*  [time.Parse](https://golang.org/pkg/time/#Parse)可以用来解析一个日期字符串。
*  [Format](https://golang.org/pkg/time/#Time.Format)可以对一个 [time.Time](https://golang.org/pkg/time/#Time)的值进行格式化。

```go
      func Parse(layout, value string) (Time, error)
      func (t Time) Format(layout string) string
```
		
# 格式化可选项		
Type | Options
:----:  | :----: 
Year	 | 06   2006
Month	| 01   1   Jan   January
Day	| 02   2   _2   (width two, right justified)
Weekday| 	Mon   Monday
Hours| 	03   3   15
Minutes| 	04   4
Seconds	| 05   5
ms μs ns	| .000   .000000   .000000000
ms μs ns	| .999   .999999   .999999999   (trailing zeros removed)
am/pm| 	PM   pm
Timezone	| MST
Offset| 	-0700   -07   -07:00   Z0700   Z07:00


# 获取当前时间戳
可以使用[time.Now](https://golang.org/pkg/time/#Now)和方法
 [time.Unix](https://golang.org/pkg/time/#Time.Unix) 或则 [time.UnixNano](https://golang.org/pkg/time/#Time.UnixNano) 获取时间戳。
 
 ```go
 	now := time.Now()      // current local time
	sec := now.Unix()      // number of seconds since January 1, 1970 UTC
	nsec := now.UnixNano() // number of nanoseconds since January 1, 1970 UTC

	fmt.Println(now)  // time.Time
	fmt.Println(sec)  // int64
	fmt.Println(nsec) // int64
 ```


