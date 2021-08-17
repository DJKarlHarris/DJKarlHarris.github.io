---
layout: post
title: Three-way partition(三分法)
date: 2021-8-17
categories: Algorithm
tags: 分治
author: Karl Harris
mathjax: true
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Three-way partiton](#three-way-partiton)
  - [作用](#%E4%BD%9C%E7%94%A8)
  - [代码](#%E4%BB%A3%E7%A0%81)
  - [思想](#%E6%80%9D%E6%83%B3)
  - [**参考博文**: Three-way-partition](#%E5%8F%82%E8%80%83%E5%8D%9A%E6%96%87-three-way-partition)
  - [**LeetCode相关题目链接**: 324](#leetcode%E7%9B%B8%E5%85%B3%E9%A2%98%E7%9B%AE%E9%93%BE%E6%8E%A5-324)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Three-way partiton
## 作用
将数组按照某个target分为三个部分,第一个部分为小于target的值所在部分,第二个部分等于target值,第三部分大于target值。实现思路与QuickSort的partition部分算法原理一样,不同在于多了一根指向大于target数的指针。
## 代码

    void threeWayPartition(vector<int>& nums,int target){
        int i=0,j=0,k=nums.size()-1;
        while(j<k){
            if(nums[j]>target){
                swap(nums[k++],nums[j]);//没有j++是因为从尾部换上来的数不能确定是否小于等于target
            }
            else if(nums[j]<target){
                swap(nums[i++],nums[j++]);
            }
            else
                j++;
        }
    }

## 思想
通过一次扫描与交换数,使得数组符合一定的规律,快排的**partition**思想则是分成**两个部分**,而**three-way-partition**则是分成**三个部分**,分别为[**小于target**][**等于target**][**大于target**]

## **参考博文**: [Three-way-partition](https://blog.csdn.net/petersmart123/article/details/78419745)

## **LeetCode相关题目链接**: [324](https://leetcode-cn.com/problems/wiggle-sort-ii/)
    


