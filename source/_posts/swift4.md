---
title: swift开发(四) 枚举与结构体
date: 2016-04-20 16:59:14
tags: [swift,IOS]
---

## 枚举
### 枚举的定义
用 enum 创建枚举 枚举中可包含 方法
swift中的枚举类型更加灵活，实现了支持关联值的枚举，还可以设置原始值得枚举

```
enum Rank:Int{
    case Ace = 1
    case Two,Three,Fore,Five,Six,Seven,Eight,Nine,Ten
    case Jack,Queen,King
    
    func simpleDescription() -> String{
        switch self{
        case .Ace:
            return "ace"
        case .Jack:
            return "jack"
        case .Queen:
            return "queen"
        case .King:
            return "king"
        default:
            return String(self.rawValue)
        
        }
    
    }

}
Rank(rawValue: 1) // 用init?(rawValue)初始化
let ace = Rank.Ace
let aceRawValue = ace.rawValue
ace.simpleDescription()

if let convert = Rank(rawValue: 3)
{
    let three = convert.simpleDescription()
}

```

### 关联值
在siwft中可以定义这样的枚举类型，每一个枚举项都是一个附加信息，来扩充这个枚举项的信息
比如我们有一个枚举类型ServerResponse来表示服务应答结果

```
enum ServerResponse{
    case Result(String,String)
    case Failure(String)
    
    
}

let success = ServerResponse.Result("6:00 am", "8.09pm")
let failure = ServerResponse.Failure("out of cheese")

switch success {

case let .Result(sunrise,sunset):
    print("----\(sunrise)----\(sunset)")
case let .Failure(message):
    print("Failure...\(message)")


}
```
### 原始值
原始值为枚举项提供默认值 如

```
enum WeekDay:String{
    case Monday = "1. Monday"
    case Tuesday = "2. Tuesday"
    case WednesDay = "3. WednesDay"
    case Thursday = "4. Thursday"
    case Firday = "5. Firday"
    case Saturday = "6. Saturday"
    case Sunday = "7. Sunday"
}

```
我们可以用rawValue 输出

```
print(WeekDay.Saturday.rawValue)
```
我们可以通过原始值来初始化
```
let day = WeekDay(rawValue: "7. Sunday")
```

## 结构体
使用struct创建结构体，结构体和类有很多相似之处，包括方法和构造函数。两者不同之处在与结构体传值都是 copy 而类都是引用

```
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDes() -> String
    {
        return "the \(rank.simpleDescription()) of \(suit.sumpeDes())"
    }
}


var card = Card(rank: Rank.Six, suit: Suit.Spades)
print(card.simpleDes())
```