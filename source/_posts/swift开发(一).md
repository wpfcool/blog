---
title: swift开发(一) 基础
date: 2016-04-20 10:54:50
tags: [swift,IOS]
---

# 常量和变量 
## 声明常量和变量
```
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
//你可以在一行中声明多个常量或者多个变量，用逗号隔开
var x = 0.0, y = 0.0, z = 0.0
//类型标注  当你声明常量或者变量的时候可以加上类型标注 说明常量或者变量中要存储的值的类型
//注意：一般来说你很少需要写类型标注。如果你在声明常量或者变量的时候赋了一个初始值，Swift可以推断出这个常量或者变量的类型
var welcomeMessage: String
welcomeMessage = "hello"
```
## 常量变量的命名规则

常量和变量的命名  你可以用任何你喜欢的字符作为常量和变量名，包括 Unicode 字符,常量与变量名不能包含数学符号，箭头，保留的（或者非法的）Unicode 码位，连线与制表符。也不能以数字开头，但是可以在常量与变量名的其他地方包含数字。

```
let π = 3.141592654
let 你好 = "你好世界"
let abc = 2
```

用 \\() 可以更简单的实现在字符串中包含一些值

```
let apples = 3
let oranges = 5

let appleSummary = "I have \(apples) apples"
let fruitSummary = "I have \(apples+oranges) pieces of fruit"
```

# 数组 字典

```
ar shoppingList = ["catfish","water","tulips","blue paint"]
shoppingList[1] = "bottle of water"

var occupations = ["Malcolm" : "Captain","Kaylee":"Mechanic"]

occupations["jayne"] = "pub"

print(occupations)


```
## 创建空数组 和 字典

```
var emptyArray = [String]()
var emptyDictionary = [String:Float]()
emptyDictionary["dd"] = 1.0
print(emptyDictionary)

emptyArray.append("dd")
print(emptyArray)

//空
shoppingList = []
occupations = [:]

```

# Optional
## 声明Optional

声明为Optional只需要在类型后面紧跟一个?

```
var optionalString: String? = "hell0"

print(optionalString == nil)
```

对于Optional值，不能直接进行操作，否则会报错：
例如  

```
var optionalString: String? = "hell0"
let value = optionalString.hashValue //报错
```

## Optional的 使用

然后怎么使用Optional值呢？文档中也有提到说，在使用Optional值的时候需要在具体的操作，比如调用方法、属性、下标索引等前面需要加上一个?，“Optional Chaining的问号的意思是询问是否响应后面这个方法，和原来的isResponseToSelector有些类似”，如果是nil值，也就是Optional.None，固然不能响应后面的方法，所以就会跳过，如果有值，就是Optional.Some，可能就会拆包(unwrap)，然后对拆包后的值执行后面的操作，比如：

```
let hashValue = strValue?.hashValue  
```

另外，对于Optional值，不能直接进行操作，否则会报错：
上面提到Optional值需要拆包(unwrap)后才能得到原来值，然后才能对其操作，那怎么来拆包呢？拆包提到了几种方法，一种是Optional Binding， 比如：

```

if let str = strValue { 
    let hashValue = str.hashValue 
} 

```
还有一种是在具体的操作前添加!符号，好吧，这又是什么诡异的语法?!
 
直接上例子，strValue是Optional的String：

```
let hashValue = strValue!.hashValue 
```
这里的!表示“我确定这里的的strValue一定是非nil的

## ?? 提供默认值

```
let nichName: String? = "xx"
let fullNmae: String = "john"
let info = "Hi \(nichName ?? fullNmae)"
```

# 条件语句及循环
## if 及 for-in 
if 后必须是Boolean if socre {} 是错误的

```
let individualScores = [75,43,103,87,12]
var teamScore = 0

for score in individualScores{
    if score > 50{
        teamScore += 3
    }
    else
    {
        teamScore += 1
    }
}
print(teamScore)

```

## switch
```
let vegetable = "x red pepper"
switch vegetable {
    case "celery":
    print("add some raisins and make ants on a log")
    case "cucumber","watercress":
    print("That would make a good tea sandwich")
    case let x where x.hasPrefix("pepper"):
    print("is it a soicy \(x)")
case let x where x.hasSuffix("pepper"):
    print(x)
default:
    print("everythingt tastes good in soup")

}
```
## 循环

```
var m = 101
repeat{
    m = m * 2
}while m < 100
print(m)


```
... 包含最右侧值
..< 不包含最右侧值

```

var firstForLoop = 0
for i in 0...4{
    firstForLoop += i
}
print(firstForLoop)
```
# 函数

## 函数定义

fun name(参数了列表) -> 返回值类型{}

例

```
func greet(name: String,day: String)->String
{
    return "hello \(name) ,today is \(day)"
}

print(greet("wpf", day: "2"))
```
## 可变参数

```
func sumOf(numbers: Int...)->Int{
    var sum = 0
    for number in numbers{
        sum += number
    }
    return sum
}

print(sumOf(1,2,3,4))
```

## 函数作为返回值

```
func makeIncremementer() -> ((Int) -> Int)
{
    func addOne(number: Int) -> Int{
        return number + 1
    }
    
    return addOne
}

var increment = makeIncremementer()
print(increment(7))
```

## 函数最为参数

```
func hasAnyMatches(list: [Int],condition:(Int)->Bool) -> Bool
{
    for item in list{
        
        if(condition(item)){
            return true
        }
    
    }
    return false
}


func lessThanTen(number:Int) -> Bool
{
    return number < 10
}

var numbers = [20,19,22,12]

hasAnyMatches(numbers, condition: lessThanTen)
```

## 元组最为返回值 

```
func calculateStatistics(scores:[Int]) ->(min:Int ,max:Int,sum:Int)
{
    var min = scores[0]
    var max = scores[0]
    var sum = 0
    
    for score in scores{
        if score > max
        {
            max = score
        }else if score < min
        {
            min = score
        }
        sum += score
    }
    
    return (min,max,sum)
}

let statistics = calculateStatistics([1,2,3,4,5,6,7,8,9,10])

print(statistics.sum)
print(statistics.2)
```
