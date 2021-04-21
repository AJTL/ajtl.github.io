---
author: "AJTL"
title: C++ delete this
linktitle: “C++ delete this"
weight: 10
date: 2019-06-01T16:54:49+08:00
draft: true
tags: [c++,delete]
topics: [c++]
description: ""
---

## C++中`delete this`的注意事项

- 你必须100%绝对确保`this`对象是通过`new`分配的（不是通过`new[]`，不是`placement new`，不是栈上的局部对象，不是全局对象，不是另一个对象的数据成员；仅仅只是通过原始的`new`运算符）

- 你必须100%绝对确保调用`delete this`操作的成员函数是最后调用的成员函数

- 你必须100%绝对确保在当前函数中`delete this`后，调用的其他成员函数不会读取`this`对象。

- 你必须100%确保再也不会使用`this`指针。即使你使用`this`指针和其他指针比较，例如`nullptr`，打印`this`指针，转换`this`指针等等。

`delete this`语句其实比较危险，在不同的编译器也会有不同的输出结果。最好私有化该类的构造函数，另外提供create函数。
