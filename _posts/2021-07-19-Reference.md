---
layout: post
title:  Reference
date:   2021-7-19
categories: C++
tags: C++ 语法
author: Karl Harris
mathjax: true
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Reference(引用)特点](#reference%E5%BC%95%E7%94%A8%E7%89%B9%E7%82%B9)
- [从内存分析](#%E4%BB%8E%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90)
- [为什么喜欢用Referencce](#%E4%B8%BA%E4%BB%80%E4%B9%88%E5%96%9C%E6%AC%A2%E7%94%A8referencce)
- [const reference&non—const reference(常量引用与非常量引用的比较)](#const-referencenonconst-reference%E5%B8%B8%E9%87%8F%E5%BC%95%E7%94%A8%E4%B8%8E%E9%9D%9E%E5%B8%B8%E9%87%8F%E5%BC%95%E7%94%A8%E7%9A%84%E6%AF%94%E8%BE%83)
  - [测试代码如下](#%E6%B5%8B%E8%AF%95%E4%BB%A3%E7%A0%81%E5%A6%82%E4%B8%8B)
    - [为了确保r1、r1能够绑定一个整数，编译器会将代码转换成如下](#%E4%B8%BA%E4%BA%86%E7%A1%AE%E4%BF%9Dr1r1%E8%83%BD%E5%A4%9F%E7%BB%91%E5%AE%9A%E4%B8%80%E4%B8%AA%E6%95%B4%E6%95%B0%E7%BC%96%E8%AF%91%E5%99%A8%E4%BC%9A%E5%B0%86%E4%BB%A3%E7%A0%81%E8%BD%AC%E6%8D%A2%E6%88%90%E5%A6%82%E4%B8%8B)
  - [代码运行图示](#%E4%BB%A3%E7%A0%81%E8%BF%90%E8%A1%8C%E5%9B%BE%E7%A4%BA)
  - [总结](#%E6%80%BB%E7%BB%93)
- [注意事项](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# Reference(引用)特点
1. **Reference**一般不用在变量的声明上,通常在参数传递时使用**Reference**(Pass by reference or Return by reference),**原因：传入传出时速度更快~**
    
2. 本质是**pointer**(指针),引用的内部实现是通过指针实现的,编译器将其伪装成值,因此引用(**Reference**)可称为代表一个值

---
# 从内存分析

![内存位置]({{"https://www.karlharris.cn/img/reference1.png"|absolute_url}})

	double x = 0;
	double* p = &x;
	double& r = x;
	
	cout << sizeof(x) << endl;//8字节
	cout << sizeof(p) << endl;//4字节
	cout << sizeof(r) << endl;//8字节 sizeof(r)==sizeof(x)
	cout << *p << endl;//0
	cout << x << endl; //0
	cout << r << endl; //0
    cout << p << endl; //007BFAA8
	cout << &x << endl;//007BFAA8
	cout << &r << endl;//007BFAA8

***可以很清楚的看出指针占4个字节，而值和引用都占8个字节，因此引用与值的大小相同，地址相同，值多大，引用就是多大，这是编译器造成的假象，其实引用就是一个指针，是一种更漂亮的指针**

---

# 为什么喜欢用Referencce
1.因为其本质是指针，所以传入传出时速度快，占用空间小

2.传入传出引用与传入传出值时格式高度一致

	//被调用端
	void func1(Cls* pobj) {pobj->xxx();}//指针传参
	void func2(Cls obj){obj.xxx();}//普通传参
	void func3(Cls& obj){obj.xxx();}//与普通传参数写法相同

	Cls obj；
	//调用端
	func1(&obj)；//指针调用端
	func2(obj);//普通调用
	func3(obj);//与普通调用端相同

---

# const reference&non—const reference(常量引用与非常量引用的比较)
## 测试代码如下

	//常量引用
	double d = 3.14;
	const int &r1 = d;

	//非常量引用
	int &r2 = d;

### 为了确保r1、r1能够绑定一个整数，编译器会将代码转换成如下

	//常量引用
	const int temp = d;
	const int &r1 = temp;//编译通过

	//非常量引用
	int temp = d;
	int &r1 = temp;//编译失败，r1未能实现绑定d的效果(实际绑定的是temp)

## 代码运行图示
![图示]({{"https://www.karlharris.cn/img/reference2.png"|absolute_url}})
## 总结
常量引用只要绑定的对象能够成功转换成引用的类型即可，非常量对象则必须绑定类型一致的对象

---

# 注意事项
	//以下被视为same signature(相同签名)
	double imag(const double& im){....}
	double imag(const double im){....} //Ambiguity

* 这种情况时函数是不可以重载的，因为参数列表在编译器看来是同一个东西

* 这种情况下可以重载const函数，因为编译器视const为不同签名




    