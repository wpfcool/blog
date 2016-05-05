---
title: c语言 const修饰常指针
date: 2016-05-04 10:34:49
tags: [c语言]
---

const int * A // const修饰指向的对象，A可变，A指向的对象不可变
int const * A // const修饰指向的对象，A可变，A指向的对象不可变
const int * const A // 指针A和A指向的对象都不可变 
int * const A  // const 修饰指针 ，A不可变 A指向的对象可变