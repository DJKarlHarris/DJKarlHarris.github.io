---
layout: post
title:  Beginning with MarkDown
date:   2021-7-11
categories: Git
tags: MarkDown
author: Karl Harris
mathjax: true
---
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [前言](#%E5%89%8D%E8%A8%80)
- [MarkDown Synatx](#markdown-synatx)
  - [标题](#%E6%A0%87%E9%A2%98)
  - [无序标题](#%E6%97%A0%E5%BA%8F%E6%A0%87%E9%A2%98)
  - [有序标题](#%E6%9C%89%E5%BA%8F%E6%A0%87%E9%A2%98)
  - [嵌套列表](#%E5%B5%8C%E5%A5%97%E5%88%97%E8%A1%A8)
  - [图片](#%E5%9B%BE%E7%89%87)
  - [链接](#%E9%93%BE%E6%8E%A5)
  - [链接的另一种表现形式](#%E9%93%BE%E6%8E%A5%E7%9A%84%E5%8F%A6%E4%B8%80%E7%A7%8D%E8%A1%A8%E7%8E%B0%E5%BD%A2%E5%BC%8F)
  - [分割线](#%E5%88%86%E5%89%B2%E7%BA%BF)
  - [表格](#%E8%A1%A8%E6%A0%BC)
  - [代码块](#%E4%BB%A3%E7%A0%81%E5%9D%97)
  - [文章段](#%E6%96%87%E7%AB%A0%E6%AE%B5)
  - [加粗段](#%E5%8A%A0%E7%B2%97%E6%AE%B5)
  - [斜体](#%E6%96%9C%E4%BD%93)
  - [字体、字号、颜色](#%E5%AD%97%E4%BD%93%E5%AD%97%E5%8F%B7%E9%A2%9C%E8%89%B2)
  - [引用](#%E5%BC%95%E7%94%A8)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 前言
学习MarkDown更有利于写笔记，所以写下此笔记，干就完了，奥里给！

# MarkDown Synatx
## 实现TOC目录
1. 安装node.js

    安装node.js网上有很多教程，这里就不多说了

2. 全局安装doctoc插件

    ```
    npm i doctoc -g //install 简写 i
    ```
    
    **这里注意有可能出现安装停滞不前的问题，可以换成淘宝的源即可**
    
    运行代码：
    ```
    npm config set registry https://registry.npm.taobao.org //切换源
    npm config get registry //验证是否配置成功
    ```

3. 给post加入TOC

    直接cd到post所在目录，然后输入以下代码即可
    ```
    doctoc xxx.md
    ```

---
## 标题
    #一级标题

    ## 二级标题

    ### 三级标题

    #### 四级标题   
    .....

## 无序标题 
    *-textName
    
* textName

## 有序标题 
    1.textName

1. textName

---
##  嵌套列表
      + A
          - B
              + C  
              1. a
              2. b
              3. c

  + A
      - B
          + C  
          1. a
          2. b
          3. c
---

## 图片 
    ![icon](link to pictrue)

![狗子](img\dog.jpg)
---
## 链接
    [content](link to content)

[百度](www.baidu.com)

## 链接的另一种表现形式 

    <url><link to content>

---
## 分割线
    ***
    ---
    
---
## 表格
    冒号表示空白区
    |columm 1|column 2|column 3|
    | ------ |:------:|:-------|
    |xxxxx   |xxxxxx  |xxxxxx  |
    |aaaaa   |aaaaaa  |aaaaaa  |
    |ccccc   |cccccc  |cccccc  |

|columm 1|column 2|column 3|
| ------ |:------:|:-------|
|xxxxx   |xxxxxx  |xxxxxx  |
|aaaaa   |aaaaaa  |aaaaaa  |
|ccccc   |cccccc  |cccccc  |

---
## 代码块
    每行前+tab或者加4个空格实现原理一样
    ``` [c++]
    int main(){
        cout<<"Hello world"<<endl;
    }
    ```

``` [c++]
int main(){
    cout<<"Hello world"<<endl;
}
```
---
## 文章段
    __content__

__HelloWorld__

---
## 加粗段
    **content**

**Helloworld**

---
## 斜体
    ***Helloworld***

***Helloworld***    

---
## 字体、字号、颜色
    <font face="字体类型">文章内容</font>
    <font face="微软雅黑">微软雅黑</font>
    <font face="黑体">黑体</font>
    <font face="楷体">楷体</font>
    <font face="宋体">宋体</font>
    <font face="harlow solid">harlow solid</font>
<font face="微软雅黑">微软雅黑</font>
<font face="黑体">黑体</font>
<font face="楷体">楷体</font>
<font face="宋体">宋体</font>
<font face="harlow solid">harlow solid</font>

---
## 引用
    普通引用:>
    引用链接：
    [1][百度](www.baidu.com)

>亚里士多德曾经说没有网络的地方就是最遥远的地方








 




