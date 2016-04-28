---
title: swift学习（六） 错误处理(Error Handling)
date: 2016-04-22 13:29:12
tags: [swift,IOS]
---

## 错误处理
你可以用符合ErrorType协议的的类型表示错误，枚举类型尤为适合构建一组相关的错误状态

```
enum PrinterError: ErrorType{
    
    case OutOfPaper
    case NoToner
    case OnFire

}
```
用throw 抛出一个错误，用throws标记一个能抛出错误的函数。如果你在函数中抛出一个错误，函数立马返回并且处理错误的代码被调用

```
func sendToPrinter(printName: String) throws -> String{
    if printName == "Never Has Toner"{
    
        throw PrinterError.NoToner
    }
    return "job"
}
```
有几种方式去处理错误。

1、 使用do-catch 在do中使用try 标记一个能抛出错误的代码 在catch中会自动得到错误名称。可以存在多个catch

```
do{
    let printerResponse = try sendToPrinter("Never Has Toner")
    print(printerResponse)

}catch{
    print(error)
}

```
2、使用try? 使结果变成optional类型.如果函数抛出异常，结果为nil

```
let printersuccess = try? sendToPrinter("Never Has Toner")
let printersuccess1 = try? sendToPrinter("122")
```

可以使用defer语句在即将离开当前代码块时执行一系列语句.

```
var teaKettleHeating = false

func morningRoutine() throws {
    teaKettleHeating = false
    
    defer {
        teaKettleHeating = true
    }
    
    let newspaper = try? sendToPrinter("dd")
    
    print(newspaper)
}

```
