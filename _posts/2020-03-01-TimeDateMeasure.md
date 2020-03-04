---
date:   2020-03-01
layout: post
title:  "测量运行时间"
tag: Time and date
categories: Go语言学习 
---

测量的代码片段

```go
		start := time.Now()
		// Code to measure
		duration := time.Since(start)
		
		// Formatted string, such as "2h3m0.5s" or "4.503μs"
		fmt.Println(duration)
		
		// Nanoseconds as int64
		fmt.Println(duration.Nanoseconds())
```

您可以使用这一行程序跟踪完整函数调用的执行时间，它将结果记录到标准错误流。

```go
func foo() {
    defer duration(track("foo"))
    // Code to measure
}
```

```go
	func track(msg string) (string, time.Time) {
	    return msg, time.Now()
	}
	
	func duration(msg string, start time.Time) {
	    log.Printf("%v: %v\n", msg, time.Since(start))
	}
```

[testing](https://golang.org/pkg/testing/)包支持基准测试，可用于检查代码的性能。
