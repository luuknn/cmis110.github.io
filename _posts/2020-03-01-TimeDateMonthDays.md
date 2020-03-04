---
date:   2020-03-01
layout: post
title:  "获取月份的天数"
tag: Time and date
categories: Go语言学习 
---

为了计算20年2月份有多少天，我们可以看下3月1号的前一天。

```go
		func main() {
		    t := Date(2020, 3, 0) // the day before 2020-03-01
		    fmt.Println(t)        // 2020-02-29 00:00:00 +0000 UTC
		    fmt.Println(t.Day())  // 29
		}
		
		func Date(year, month, day int) time.Time {
		    return time.Date(year, time.Month(month), day, 0, 0, 0, 0, time.UTC)
		}
```

函数 [AddDate](https://golang.org/pkg/time/#Time.AddDate)可以用于日期的调整。

```go
	t = Date(2019, 10, 31).AddDate(0, 1, 0) // a month after October 31
	fmt.Println(t)                          // 2019-12-01 00:00:00 +0000 UTC
```
