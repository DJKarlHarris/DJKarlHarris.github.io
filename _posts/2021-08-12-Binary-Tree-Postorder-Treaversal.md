---
layout: post
title: Binary Tree Postorder Treaversal
date:  2021-8-12
categories: Algorithm
tags: 二叉树 迭代 遍历
author: Karl Harris
mathjax: true
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [二叉树后序遍历迭代实现](#%E4%BA%8C%E5%8F%89%E6%A0%91%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%E8%BF%AD%E4%BB%A3%E5%AE%9E%E7%8E%B0)
  - [递归实现太简单，这里就不直接放出来了](#%E9%80%92%E5%BD%92%E5%AE%9E%E7%8E%B0%E5%A4%AA%E7%AE%80%E5%8D%95%E8%BF%99%E9%87%8C%E5%B0%B1%E4%B8%8D%E7%9B%B4%E6%8E%A5%E6%94%BE%E5%87%BA%E6%9D%A5%E4%BA%86)
    - [迭代实现：](#%E8%BF%AD%E4%BB%A3%E5%AE%9E%E7%8E%B0)
  - [**LeetCode相关题目链接**: 145](#leetcode%E7%9B%B8%E5%85%B3%E9%A2%98%E7%9B%AE%E9%93%BE%E6%8E%A5-145)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 二叉树后序遍历迭代实现
## 递归实现太简单，这里就不直接放出来了
### 迭代实现：

    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack<TreeNode*> stk;
        TreeNode* pre=nullptr;
        while(root!=nullptr||!stk.empty()){
            while(root!=nullptr){
                stk.emplace(root);
                root=root->left;
            }
            root=stk.top();
            stk.pop();
            if(!root->right||pre==root->right){//若无右节点或者已经访问过右节点，则访问本节点
                ans.emplace_back(root->val);
                pre=root;//标记本节点被访问过
                root=nullptr;//防止继续访问左节点
            }
            else{
                stk.emplace(root);//需要先向右节点搜索，所以先将本节点入栈
                root=root->right;
            }
        }   
        return ans;
    }

## **LeetCode相关题目链接**: [145](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)
