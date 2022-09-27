---
layout: post
title: "Minimum Distance Between BST Nodes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Search Tree, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 783. Given the root of a Binary Search Tree (BST), return the minimum difference between the values of any two different nodes in the tree.

---

<br />

## Description

LeetCode Problem 783.

Given the root of a Binary Search Tree (BST), return the minimum difference between the values of any two different nodes in the tree.

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
* The number of nodes in the tree is in the range [2, 100].
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
    int minDiffInBST(TreeNode *root) {
        int res = INT_MAX, pre = -1;
        helper(root, pre, res);
        return res;
    }

    void helper(TreeNode *root, int &pre, int &res) {
        if (root) {
            helper(root->left, pre, res);
            if (pre != -1) {
                res = min(res, root->val - pre);
            }
            pre = root->val;
            helper(root->right, pre, res);
        }
    }
};
```


