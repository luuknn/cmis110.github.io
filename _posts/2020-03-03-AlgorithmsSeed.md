---
date:   2020-03-03
layout: post
title:  "什么是随机种子（seed）"
tag: "Algorithms"
categories: "Algorithms"
---

实际上，伪随机数根本就不是随机的，它们是用一种固定的判定算法计算出来的。

种子是伪随机数序列的起点。如果你从相同的种子开始，你会得到相同的序列。这对于调试非常有用。

如果你希望每次都有不同的数字序列，你可以使用当前时间作为种子。


## 举例
下面的生成器会产生97个不同数字的序列，然后重新开始。种子决定了从哪个数字开始序列。

```go
// New returns a pseudorandom number generator Rand with a given seed.
// Every time you call Rand, you get a new "random" number.
func New(seed int) (Rand func() int) {
    current := seed
    return func() int {
        next := (17 * current) % 97
        current = next
        return next
    }
}

func main() {
    rand1 := New(1)
    fmt.Println(rand1(), rand1(), rand1())

    rand2 := New(2)
    fmt.Println(rand2(), rand2(), rand2())
}
```

```go
			17 95 63
			34 93 29
```


在大多数编程语言中，随机数生成器通常就是这样工作的，当然它们使用了更智能的函数。理想情况下，你希望通过采用一种廉价算术运算来得到一个长序列且具有良好的随机属性。例如，通常希望避免使用取模运算符。







