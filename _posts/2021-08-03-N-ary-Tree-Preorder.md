---
layout: post
title: N-ary Tree Preorder
date:   2021-8-03
categories: Algorithm
tags: 栈 树 遍历
author: Karl Harris
mathjax: true
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [N-ary Tree Preorder(implement iteratively)](#n-ary-tree-preorderimplement-iteratively)
- [N叉树的前序遍历的迭代实现](#n%E5%8F%89%E6%A0%91%E7%9A%84%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%BF%AD%E4%BB%A3%E5%AE%9E%E7%8E%B0)
  - [思路：](#%E6%80%9D%E8%B7%AF)
    - [前序遍历(迭代实现)要点：](#%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%E8%BF%AD%E4%BB%A3%E5%AE%9E%E7%8E%B0%E8%A6%81%E7%82%B9)
  - [实现代码：](#%E5%AE%9E%E7%8E%B0%E4%BB%A3%E7%A0%81)
  - [**LeetCode相关题目链接**: 589](#leetcode%E7%9B%B8%E5%85%B3%E9%A2%98%E7%9B%AE%E9%93%BE%E6%8E%A5-589)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# N-ary Tree Preorder(implement iteratively)    
# N叉树的前序遍历的迭代实现
## 思路：
### 前序遍历(迭代实现)要点：
1. 遍历顺顺序：根节点->左节点->右节点    
2. 从整体来看，遍历顺序为根节点->**左子树**->**右子树**，要想实现这种顺序，就必须得缓存节点信息，不然就无法遍历右子树了，只能一直访问左节点也就无法产生左子树了。根据这种关系，我们可以选择一种后进先出(FIFO)的数据结构，也就是栈(stack)

## 实现代码:

    vector<int> preorder(Node* root) {
        vector<int> ans;
        stack<Node*> stk;
        if(!root)
            return ans;
        stk.push(root);
        while(!stk.empty()){
            Node* node = stk.top();
            stk.pop();//每次取顶操作就对应着一个出栈操作
            ans.emplace_back(node->val);
            for(auto it=node->children.rbegin();it!=node->children.rend();it++){//使用反向迭代器
                if(*it!=nullptr)
                    stk.push(*it);//将子节点入栈，这里注意子节点要从右到左一次入栈，因为左节点要先被访问，要先出
            }
        }
        return ans;
    }

---
    //循环处理操作可以替换为下面版本
    auto it=node->children.end();
    while(it!=node->children.begin()){
        if(*(--it)!=nullptr)
            stk.push(*it);
        }
        
## **LeetCode相关题目链接**: [589](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/submissions/)