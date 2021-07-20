---
layout: post
title:  OjectModel(对象模型)
date:   2021-7-20
categories: C++
tags: C++ 语法
author: Karl Harris
mathjax: true
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ObjectModel](#objectmodel)
  - [vptr(虚指针)&&vtable(虚表)「虚机制」](#vptr%E8%99%9A%E6%8C%87%E9%92%88vtable%E8%99%9A%E8%A1%A8%E8%99%9A%E6%9C%BA%E5%88%B6)
    - [对象模型在底层内存的分析](#%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B%E5%9C%A8%E5%BA%95%E5%B1%82%E5%86%85%E5%AD%98%E7%9A%84%E5%88%86%E6%9E%90)
    - [总结](#%E6%80%BB%E7%BB%93)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ObjectModel
## vptr(虚指针)&&vtable(虚表)「虚机制」
### 对象模型在底层内存的分析

**先上代码:**
    
    class a{
    public: 
        virtual void virtual_func1(); //虚函数
        virtual void virtual_func2(); //虚函数
        void func1();
        void func2(); 
    private:
        int m-data1,m-data2;
    }

    class b:public a{
    public:
        virtual void virtual-func1(); //子类b重写了父类a的虚函数
        void func3(); 
    private:
        int m-data3;
    }

    class c:public b{
    public:
        virtual void virtual-func1(); //子类c重写了父类b的虚函数
        void func4();
    private:
        int m-data1,m-data2;
    }

![内存图示]({{"https://www.karlharris.cn/img/objectmodel.png"|absolute_url}})

图表达的类对象在内存中的分布是真实存在的，从图中可以看出类中含有一个以上的**虚函数**并且类和类之间有继承关系时(**函数的继承不是指继承函数所占内存大小，而是指继承函数调用权**)，类内会有多出一个**指针(虚指针)** 指向 **虚表**，子类**没有重写(OverRide)**的**虚函数**都会指向同一个虚函数(相同地址),而子类**重写**的虚函数会被**重新分配**一个地址.编译器看到有指针指向的类使用虚函数时就进行图示调用(动态绑定),即指向对象的**p指针**通过指向**虚表的vptr**找到**指向虚函数的vtable**最后找到想要调用函数地址，虚函数的调用解释称成C形式的代码如下所示:

    *(ptr->vptr)[n](p);
    (*ptr->vptr[n])(p);

### 总结
- C++编译器看到函数就会判断进行的是静态绑定还是动态绑定，而动态绑定(虚机制)的条件为：1.必须通过指针调用 2.指针是向上转型(up-cast) 3.调用的是虚函数
- 虚机制的作用：面向对象的多态性(同一个父类的不同子类有不同的行为**通过重写虚函数实现**)
