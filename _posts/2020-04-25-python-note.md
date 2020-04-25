---
layout: post
title: 'python学习笔记 1'
date: 2020-04-25
tags: python
---

Python的变量不需要声明类型，那么引申出以下思考

1. **已经被赋予整型数值的a变量，可以再被赋值为字符串吗？可以**

   ```python
a = 1
   a = "1"
   ```
   
   因为python中所有的变量都是引用，可以理解为每一个变量都是C语言中的void*，即可以指向任意类型。所以python中变量不需要要声明类型时因为变量本身确实就没有具体类型，它们都是引用。

2. 虽然python变量没有类型，但变量所指的对象是有类型的。python中有六个标准的数据类型：

   1. Number（包括int，float，bool，complex）
   2. String
   3. List
   4. Tuple
   5. Set
   6. Dictionary

3. **不可变类型**：Number，String，Tuple

   **可变类型**：List，Set，Dictionary

   不可变类型即指变量所指的内存中的值是不可变的，因此如果对这种类型的变量重新赋值，实际上是为新值在内存中开辟了一块空间，并将变量重新指向这个新内存空间。

   可变类型则当值被修改时，内存地址不会变化。
   
4. **赋值**

   ```python
   a = 123456
   b = a
   print(id(a) == id(b))
   # 输出结果 True
   ```

   可以看出将a赋值给b时，实际发生的是引用的复制。

   ```python
   a = "first"
   b = a
   a = "second"
   print(a, b)
   c = [a, b]
   d = c
   a = "third"
   c[1] = "fourth"
   print(c, d)
   # 输出结果为
   # second first
   # ['second', 'fourth'] ['second', 'fourth']
   ```

   因为是不可变类型，所以a的修改不会影响到b，a被重新赋值时变量a是引用被替换了，而”first“这个对象依旧还是保持原样。同理，c[0]也不会随a而变化。但是因为列表是可变类型，而c和d其实是同一个引用，所以c[1]的修改是会影响到d的。
   
5. **拷贝**

   显然如果只能使用赋值的话，那如果有需要两份一样的可变类型的数据，但是做不同处理的场景时，显然是不够的。

   ```python
   >>> import copy
   >>> a = [1,2,3,[1234]]
   >>> b = copy.copy(a)
   >>> c = copy.deepcopy(a)
   >>> a[1] = 1234
   >>> a[3][0] =1
   >>> a
   [1, 1234, 3, [1]]
   >>> b
   [1, 2, 3, [1]]
   >>> c
   [1, 2, 3, [1234]]
   ```

   可以看出浅拷贝只会复制列表中第一层的每个元素，即如果有一个元素是可变元素，对这个元素的修改，依旧还是会反应在a和b上。但是如果是深拷贝则是拷贝至每个不可变元素，即拷贝和被拷贝对象再无关联。
