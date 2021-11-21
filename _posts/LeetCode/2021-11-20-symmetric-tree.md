---
layout: post
title:  "Symmetric Tree Problem"
categories: [ Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree, Leetcode ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 101. Given the root of a binary tree, check whether it is a mirror of itself.
---

<br />

## Description

LeetCode Problem 101. 

Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

Example 1:
```
Input: root = [1,2,2,3,4,4,3]
Output: true
```

Example 2:
```
Input: root = [1,2,2,null,3,null,3]
Output: false
```

Constraints:

* The number of nodes in the tree is in the range [1, 1000].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isMirror(TreeNode* t1, TreeNode* t2) {
        if ((t1 == NULL) && (t2 == NULL))
            return true;
        else if (t1 == NULL)
            return false;
        else if (t2 == NULL)
            return false;
        else
            return (
                (t1->val == t2->val) && 
                isMirror(t1->left, t2->right) && 
                isMirror(t1->right, t2->left)
            );
    }
    
    bool isSymmetric(TreeNode* root) {
        return isMirror(root, root);
    }
};
```
