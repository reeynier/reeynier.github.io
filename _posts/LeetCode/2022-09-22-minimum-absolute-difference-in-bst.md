---
layout: post
title: "Minimum Absolute Difference In BST Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Search Tree, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 530. Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

---

<br />

## Description

LeetCode Problem 530.

Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

Example 1: 
```
Input: root = [4,2,6,1,3]
Output: 1
```

Example 2: 
```
Input: root = [1,0,48,null,null,12,49]
Output: 1
```

Constraints:
* The number of nodes in the tree is in the range [2, 10^4].
* 0 <= Node.val <= 10^5


<br />

## Sample C++ Code


```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int inorderTraverse(TreeNode* root, int& val, int& min_dif) {
        if (root->left != NULL)
            inorderTraverse(root->left, val, min_dif);
        if (val >= 0) 
            min_dif = min(min_dif, root->val - val);
        val = root->val;
        if (root->right != NULL) 
            inorderTraverse(root->right, val, min_dif);
        return min_dif;
    }
    
    int getMinimumDifference(TreeNode* root) {
        auto min_dif = INT_MAX, val = -1;
        return inorderTraverse(root, val, min_dif);
    }
};
```


