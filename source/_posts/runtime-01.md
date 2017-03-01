---
title: runtime
date: 2017-01-11 15:48:34
tags: [runtime,iOS]
---


## runtime 是什么
我们写的代码在程序运行过程中都会被转化成runtime的C代码执行

# 定义一个类Person

```
Person.h

#import <Foundation/Foundation.h>

@interface Person : NSObject
{
NSString * birthday;
}
@property (nonatomic,copy)NSString * name;
@property (nonatomic,assign) NSInteger age;

-(void)eat;
-(void)sayHello;
@end

person.m

#import "Person.h"

@interface Person()
{
NSInteger weight;
}
@property(nonatomic,assign)NSInteger height;

@end

@implementation Person
-(void)eat
{

}

-(void)sayHello
{

}
-(void)sleep
{

}


```


1. runtime 获得数据成员方法 class_copyIvarList（Class cls, unsigned int *outCount）

```
unsigned int count = 0;
Ivar * ivars = class_copyIvarList([Person class], &count);

for (int i = 0; i < count; i++) {
Ivar var = ivars[i];
const char * name = ivar_getName(var);
const char * type = ivar_getTypeEncoding(var);


NSLog(@"name:%s type:%s",name,type);

}


```
结果  : 

name:birthday type:@"NSString"  
name:weight type:q  
name:_name type:@"NSString"  
name:_age type:q  
name:_height type:q  

2. runtime 获得property class_copyPropertyList(Class cls, unsigned int *outCount)

```
unsigned propertyCount = 0;
objc_property_t * pro =   class_copyPropertyList([Person class], &propertyCount);
for (int i = 0;  i < propertyCount; i++) {

const char * name =  property_getName(pro[i]);
NSLog(@"name-->%s",name);

}

```
结果  
name-->height  
name-->name  
name-->age

3. 获取方法列表  class_copyMethodList(Class cls, unsigned int *outCount)

```
unsigned methodCount = 0;
Method * methods =  class_copyMethodList([Person class], &methodCount);
for (int  i = 0; i < methodCount; i++) {
Method  method = methods[i];
SEL sel = method_getName(method);
const char * name = sel_getName(sel);
NSLog(@"%s",name);
}
```
结果：  
eat  
sayHello  
sleep  
age  
setAge:  
.cxx_destruct  
name  
setName:  
height  
setHeight:  
4. 获得协议列表

```
unsigned protocolCount = 0;
__unsafe_unretained Protocol ** protocolList = class_copyProtocolList([Person class], &protocolCount);
for (int  i = 0; i < protocolCount; i++) {
Protocol * myPrototcl = protocolList[i];
NSLog(@"%s",protocol_getName(myPrototcl));
}
```

[DEMO:Runtime_01](https://github.com/wpfcool/runtime)
