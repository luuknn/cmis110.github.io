---
date:   2020-03-01
layout: post
title:  "时区"
tag: Time and date
categories: Go语言学习 
---

每个 [Time](https://golang.org/pkg/time/#Time)都与一个[Location](https://golang.org/pkg/time/#Location)关联，用于时区的展示。

方法[In](https://golang.org/pkg/time/#Time.In)会返回一个特定位置的时间。在这种方式下改变地理位置只会改变时间的表达方式，并不会真正改变当下描述的时间。

TimeIn 这个函数会方便的改变时间的时区。
 
 ```go
    // TimeIn returns the time in UTC if the name is "" or "UTC".
    // It returns the local time if the name is "Local".
    // Otherwise, the name is taken to be a location name in
    // the IANA Time Zone database, such as "Africa/Lagos".
    func TimeIn(t time.Time, name string) (time.Time, error) {
        loc, err := time.LoadLocation(name)
        if err == nil {
            t = t.In(loc)
        }
        return t, err
    }
 ```
 
 ```go
 	for _, name := range []string{
		"",
		"Local",
		"Asia/Shanghai",
		"America/Metropolis",
	} {
		t, err := TimeIn(time.Now(), name)
		if err == nil {
			fmt.Println(t.Location(), t.Format("15:04"))
		} else {
			fmt.Println(name, "")
		}
	}
 ```
 ```go
		UTC 09:09
		Local 17:09
		Asia/Shanghai 17:09
		America/Metropolis 
 ```
 
 [package time :Date](https://golang.org/pkg/time/#Date)
 


