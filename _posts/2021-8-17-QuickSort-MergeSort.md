---
layout: post
title: QuickSort与MergeSort的效率比较
date:  2021-8-16
categories: Algorithm
tags: 分治 排序 递归
author: Karl Harris
mathjax: true
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [QuickSort(快速排序)&&MergeSort(归并排序)的效率比较](#quicksort%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8Fmergesort%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F%E7%9A%84%E6%95%88%E7%8E%87%E6%AF%94%E8%BE%83)
  - [QuickSort代码](#quicksort%E4%BB%A3%E7%A0%81)
  - [mergeSort代码](#mergesort%E4%BB%A3%E7%A0%81)
  - [比较结果](#%E6%AF%94%E8%BE%83%E7%BB%93%E6%9E%9C)
  - [总结](#%E6%80%BB%E7%BB%93)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# QuickSort(快速排序)&&MergeSort(归并排序)的效率比较

## QuickSort代码

    void quickSort(vector<int>& nums,int left,int right){
        if(left>=right)
            return;
        int r=rand()%(right-left+1)+left;
        int x=nums[r];
        swap(nums[r],nums[right]);
        int i=left-1;
        for(int j=left;j<right;j++){
            if(nums[j]<x)//由于随机数生成范围在[0,32768]之间,若生成数量大，则数重复率高,若此处改为nums[j]<=x,效率会变低很多很多
                swap(nums[++i],nums[j]);
        }
        swap(nums[++i],nums[right]);
        quickSort(nums,left,i-1);
        quickSort(nums,i+1,right);
    }

## mergeSort代码

    void mergeSort(vector<int>& nums,vector<int>& temp,int left,int right){
        if(left>=right)
            return;
        int mid=(right+left)>>1
        mergeSort(nums,left,mid);
        mergeSort(nums,mid+1,right);
        for(int i=left;i<=right;i++)
            temp[i]=nums[i];
        int i=left,j=mid+1;
        for(int k=left;k<=right;k++){
            if(i==mid+1)
                nums[k]=temp[j++];
            else if(j==right+1||temp[i]<=temp[j])
                nums[k]=temp[i++];
            else    
                nums[k]=nums[j++];
        }
    }

## 比较结果
![1W数据]({{"https://www.karlharris.cn/img/1W.png"|absolute_url}})

![10W数据]({{"https://www.karlharris.cn/img/10W.png"|absolute_url}})

![100W数据]({{"https://www.karlharris.cn/img/100W.png"|absolute_url}})

![1000W数据]({{"https://www.karlharris.cn/img/1000W.png"|absolute_url}})

## 总结
1. 快速排序与归并算法都运用了**分治思想**,将问题分成子问题(可以简单求解的子问题)解决后再合并,归并注重与如何**治**(合并子问题),而快速排序着重于如何**分**(分解子问题)
2. 快速排序相对归并排序来说不够稳定，不稳定的因素有以下三点：
    1. 与基准数比较之后产生的swap(相同值的相对位置的交换)会导致排序的不稳定
    2. 基准数归位之后的swap也会导致不稳定
    3. 基准数的随机选取也会导致不稳定
    
    **解决方案：用额外空间辅助空间实现稳定快速排序**

        def MySort(self , arr ):  
        if len(arr) <= 1:  
            return arr  
        left, right = [], []  
        for i in range(1,len(arr)):  
            if arr[i] < arr[0]:  
                left.append(arr[i])  
            else:  
                right.append(arr[i])  
        return self.MySort(left) + [arr[0]] + self.MySort(right) 

    大于等于(必须时大于等于)的放在右侧数组，小于的放在左侧数组，保证相同数字的相对位置,因为选用的是头部元素，相同的元素本来就在头部元素的右边，所以必须是大于等于

        return self.MySort(left) + [arr[0]] + self.MySort(right) //保证了相同数字的相同数字的相对位置

3. 而效率取决于元素的排列是否随机，若接近排列接近有序时时间复杂度会达到O(n^2),我们应该根据不同的情况使用不同的算法，int，double，且数组长度在一定阀值内，则使用快排，如果在阀值外，则用归并。

    ---

4. 衍生出来的子问题：
    1. ### 求数组中第k大的元素 [215](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)
        用快速排序即可快速得到答案，只需增加一个比较即可，返回选中的分割数的下标等于(nums.size()-k)即可，因为是顺序排序，所以第k大的元素的下标为元素总数-k，若为要找的元素为第k小的元素则下标为k，逆序排序则反之。这里使用快速排序的时间复杂度其实O(n)，因为每次只递归一个部分，该算法也叫**快速选择**，C++中的STL的nth_element()函数可以进行快速选择，此函数的效果为将数组第n小的元素放在数组的第n个位置，同时保证左侧元素不大于自身，右侧元素不小于自身。

        **由快速选择引出的另一道题：**

    2. ### 摆动排序 [324](https://leetcode-cn.com/problems/wiggle-sort-ii/)
    
        解法1：排序后分成两半，进行一小一大拉链合并，

        解法2：快速选择+Three way partition解决此题，时间复杂度为O(n)，由于只需要找一个中位数，我们并不关心中位数的左右部分是否顺序，只需要满足左部分的元素小于中部分(中位数集合，因为中位数可能很多个)，中部分的元素小于右部分即可。利用快速选择找出中位数，three way patition 解决三部分问题

        **当元素总数为奇数时mid=mid+1**

    3. ### 求数组中的逆序对 [剑指Offer-51](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)
        逆序对的意思按顺序从数组随机抽两个数，若后一个数比前一个大，则为逆序对。
    如何使用归并排序的思想解决这道题呢？举个例子，数组A[2,8,10,11]和数组B[4,6,7,9]，我们设置一个归并后的数组为C,当C数组为[2]时，数组B并无比2小的数，即2这个数字没有逆序对，当C数组为[2,4,6,7]时，数组A的二号元素**8**<数组B的三号元素**9**，此时到**8**入列为止之前B数组已经入列了三个元素分别为4、6、7，这三个元素都处于8的后面，且比8小，符合逆序对的标准
    ，即数组A的8能组成3个逆序对，之后C数组为[**2**,4,6,7,**8**,9]时，数组B已无元素可以归并，接下来依次将A数组的元素入列，入列的元素**10**与**11**能组成的逆序对数量均为B数组已经入列的元素数量4,逆序对的总数量为3+4+4=11