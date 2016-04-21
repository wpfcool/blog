---
title: swift开发（二） 闭包
date: 2016-04-20 14:53:50
tags: swift
---

***

## 闭包表达式

> { (parameters) -> returnType in statements} 


***
代码列子

```
import UIKit

var list = [1,5,2,6,2,8,6,4,9,25,2]

let a = list.map({(number:Int)->Int in
    let result = 3 * number
    return result
})

print(a)


var b = list.sort{$0 < $1}
print(b)


func order(number1:Int,number2:Int) -> Bool{


    return number2 < number1
}
var bc = list.sort(order)

print(bc)

// 完整
var aa = list.sort({(number1:Int,number2:Int)->Bool in return number1 > number2})

print(aa)

//简写1 根据上下文推断类型
aa = list.sort({(number1,number2) in return number1 > number2})

print(aa)

//简写2 单行表达式闭包可以省略 return
aa = list.sort({(number1,number2) in number1 > number2})

print(aa)

//简写2 参数名简写  $0 代表第一个参数
aa = list.sort({ $0 > $1})

print(aa)

```


