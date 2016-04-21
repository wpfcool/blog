---
title: swift开发(四) 枚举与结构体
date: 2016-04-20 16:59:14
tags: swift
---

## 枚举

用 enum 创建枚举 枚举中可包含 方法

```
// 枚举
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

## 结构体
