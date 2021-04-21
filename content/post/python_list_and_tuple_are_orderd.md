---
author: "AJTL"
title: 为什么python中的list和tuple是有序的
linktitle: "为什么python中的list和tuple是有序的"
weight: 10
date: 2019-10-10T19:08:15+08:00
draft: true
tags: [Python,List,Tuple,Dictionary]
topics: [Python]
description: ""
---

[What does it mean in Python that tuples and lists are ordered, but dictionaries are not ordered? - Qura](https://www.quora.com/What-does-it-mean-in-Python-that-tuples-and-lists-are-ordered-but-dictionaries-are-not-ordered )

Suppose, we have initialised a list L. And it consists of numbers in it. List looks something like
**照例，我们来初始化一个list L并赋一些值在里面。**

```python
L=[1, 2, 3, 4, 5]
```

Now, Try doing the following and see the result.
**现在 执行下面一些操作并查看结果。将list元素按照索引print到console。**

```python
print(L)
print(L[0], L[1], L[2], L[3], L[4])
```

Similarly, let’s initialise a dictionary D
**同样的，初始化一个字典 D**

```python
D={'Maharashtra': 'Mumbai', 'Rajasthan': 'Jaipur', 'Karnataka': 'Bengaluru'}
```

Likewise, do
**执行和list一样的操作，将字典print到console**

```python
print(D)
```

Let’s try this as well. Initialise a Tuple T.
**这次新建一个tuple对象**

```python
T=(1, 2, 3, 4, 5)
```

Checkout the result
**查看print结果**

```python
print(T)
print(T[0], T[1], T[2], T[3], T[4])
```

Conclusion based on the above exercise.
In Lists and Tuples you will be able to access the elements based on there position. That is element at position 0 will always be at position 0 hence, can be accessed using integers like L[0] or T[0] and result will be 1.
**通过上述的操作可以发现，在列表List和元组Tuple中，我们可以通过元素的位置来获取元素的值。计数从0开始**

While, when you print the Dictionary it may give an output like
**然而，当你print字典的时候，结果可能如下：**

```python
{'Maharashtra': 'Mumbai', 'Rajasthan': 'Jaipur', 'Karnataka': 'Bengaluru'}
```

or
**或者是**

```python
{'Rajasthan': 'Jaipur', 'Karnataka': 'Bengaluru', 'Maharashtra': 'Mumbai'}
```

or some other way.
**或者一些其他的结果**

 What remains fixed is the mapping of values with keys. But, positioning might vary. So, when you access elements present in dictionary. We don’t do it based on position. We do it based on keys.
**可以发现，key 与 value始终保持一致，但是元素索引位置会有不同的情况，所以当从字典中取值时，不通过元素索引，需要通过key值去取值。**

```python
print(D['Rajasthan'], D['Karnataka'], D['Maharashtra'])
```

So, on and so fourth.

Coming back to Question.

So, Tuples and Lists are ordered. Dictionaries are unordered.

**回到最初的问题本身， List和Tuple时有序的，字典是无序的。**

Can dictionary be ordered?
**字典是可以有序的吗**

Yes, checkout collections library. And a method named as OrderedDict(). As, the name suggests it remembers the order in which contents are added.
**当然，Collections 库有一个OrderedDict的类型，是一个有序字典**

## Conclusion

+ 有序是指序号一致，即索引值符合插入值的序号。
+ 对比C++，List和Tuple好比vector，字典对比map。
