---
title: runtime 方法调用及转发
date: 2017-01-11 16:05:19
tags: [iOS ,runtime]
---


# 方法调用

如果用实例对象调用实例方法，会到实例isa指针指向的对象（类对象）操作
如果调用的是类方法，就会到类对象的isa指针指向的对象（元类对象）中操作

## 方法调用过程
1. 首先，在相应操作的对象中的缓存方法列表中找到调用的方法，如果找到，转向相应实现并执行
2. 如果没找到，在相应操作的对象中的方法列表中找到调用方法，如果找到，转向相应实现执行
3. 如果没找到，去父类指针所指向的对象中执行1，2操作
4. 以此类推，如果一直到跟类没有找到，转向拦截调用
5. 如果没有重写拦截调用的方法，程序报错


## 拦截调用  
在找不到调用方法程序崩溃之前，重写一下四个方法
```
+(BOOL)resolveInstanceMethod:(SEL)sel;
+(BOOL)resolveClassMethod:(SEL)sel;
-(void)forwardInvocation:(NSInvocation *)anInvocation;
-(id)forwardingTargetForSelector:(SEL)aSelector;

```

第一个方法，当调用不存在的实例方法时调用  
第二个方法，当调用不存在的类方法时调用  
第三个个方法是将你调用的不存在的方法打包成NSInvocation传给你，做完自己的处理后调用invokeWithTarget:方法让某个target触发这个方法  
第四个个方法当你调用不存在的方法重新定向其他声明这个方法的类，只需返回这个方法的target  

## 动态添加方法

```
class_addMethod(<#__unsafe_unretained Class cls#>, <#SEL name#>, <#IMP imp#>, <#const char *types#>)
```
其中class_addMethod的四个参数分别是：

1. Class cls  
给哪个类添加方法，本例中是self
2. SEL name  
添加的方法，本例中是重写的拦截调用传进来的selector。
3. IMP imp  
方法的实现，C方法的方法实现可以直接获得。如果是OC方法，可以用+ (IMP)instanceMethodForSelector:(SEL)aSelector;获得方法的实现。
4. "v@:*"方法的签名，代表有一个参数的方法。  


[DEMO:runtime_02](https://github.com/wpfcool/runtime)

