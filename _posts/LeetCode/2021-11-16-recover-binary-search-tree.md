---
layout: post
title:  "Recover Binary Search Tree Problem"
categories: [ Data Structure ]
tags: [ Tree, Depth-First Search, Binary Search Tree, Binary Tree, Leetcode ]
similar: [ Binary Search Tree ]
featured: false
hidden: false
excerpt: LeetCode 99. You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake.
---

<br />

## Description

LeetCode Problem 99. 

You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.

 

Example 1:
```
Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.
```

Example 2:
```
Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.
```

Constraints:

* The number of nodes in the tree is in the range [2, 1000].
* -2^31 <= Node.val <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
    TreeNode* first=NULL;
    TreeNode* second=NULL;
    TreeNode* prev = new TreeNode(INT_MIN);
public:
    void recoverTree(TreeNode* root) {
        help(root);
        swp(first->val, second->val);
    }
    
    void help(TreeNode* root){
        if(root==NULL)  return;
        help(root->left);
        if(first==NULL && prev->val >= root->val)   first=prev;
        if(first!=NULL && prev->val >= root->val)   second=root;
        prev=root;
        help(root->right);
    }
};
```
