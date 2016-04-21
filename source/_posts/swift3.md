---
title: swift开发（三） 对象与类
date: 2016-04-20 16:48:00
tags: swift
---

***
## 类
用class后面紧跟类名创建类
init() 初始化

```
class NameShap {
    var numberOfSides:Int = 0
    var name: String
    init(name:String){
        self.name = name
    }
    func simpleDescription()->String{
        return "A shape with \(numberOfSides) sides."
    }
}


```
## 继承
override 重写方法

```
class Square: NameShap {
    var sideLength:Double
    
    init(sideLength:Double,name:String)
    {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }
    
    func area() -> Double{
        return sideLength * sideLength
    }
    
    override func simpleDescription() -> String {
        return "a square with sides of length \(sideLength)"
    }
}

```
## getter setter 方法

```
class EquilateralTriangle: NameShap {
    var sideLength: Double = 0.0
    init(sidelength:Double,name:String){
        self.sideLength = sidelength
        super.init(name: name)
        numberOfSides = 3
    }
    
    //get set
    var perimetter: Double{
        
        get{
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0  //newValue 隐型的新值
        
        }
    
    }
    
    override func simpleDescription() -> String {
        return "an equilateral triangle with sides of length \(sideLength)"
    }
    
}

```
## willSet didSet

```
class TriangleAndSquare {
 
    var triangle:EquilateralTriangle{
        willSet{
            squate.sideLength = newValue.sideLength
            
        
        }
    }

    var squate:Square{
        willSet{
            triangle.sideLength = newValue.sideLength;
        
        }
    
    }
    
    init(size:Double,name:String){
    
        squate = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sidelength: size, name: name)
        
    }
}
```