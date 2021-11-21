---
layout: post
title:  "Construct Binary Tree from Preorder and Inorder Traversal Problem"
categories: [ Data Structure ]
tags: [ Array, Hash Table, Divide and Conquer, Tree, Binary Tree, Leetcode ]
similar: [ Binary Tree ]
featured: false
hidden: false
excerpt: LeetCode 105. Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.
---

<br />

## Description

LeetCode Problem 105. 

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

Example 1:
```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

Example 2:
```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

Constraints:

* 1 <= preorder.length <= 3000
* inorder.length == preorder.length
* -3000 <= preorder[i], inorder[i] <= 3000
* preorder and inorder consist of unique values.
* Each value of inorder also appears in preorder.
* preorder is guaranteed to be the preorder traversal of the tree.
* inorder is guaranteed to be the inorder traversal of the tree.

<br />

## Sample C++ Code


```c
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if (preorder.size() == 0)
            return NULL;
        TreeNode* root = new TreeNode(preorder[0]);
        
        vector<int> left_pre, right_pre, left_in, right_in;
        bool isleft = true;
        for (int i = 0; i < inorder.size(); i ++) {
            if (inorder[i] == preorder[0]) {
                isleft = false;
                continue;
            }
            if (isleft) {
                left_pre.push_back(preorder[i+1]);
                left_in.push_back(inorder[i]);
            } else {
                right_pre.push_back(preorder[i]);
                right_in.push_back(inorder[i]);
            }
        }
        
        root->left = buildTree(left_pre, left_in);
        root->right = buildTree(right_pre, right_in);
        
        return root;
    }
};
```
