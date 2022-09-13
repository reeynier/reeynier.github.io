---
layout: post
title: "Invert Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 226. Given the root of a binary tree, invert the tree, and return its root.

---

<br />

## Description

LeetCode Problem 226.

Given the root of a binary tree, invert the tree, and return its root.

Example 1:
```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```

Example 2:
```
Input: root = [2,1,3]
Output: [2,3,1]
```

Example 3:
```
Input: root = []
Output: []
```

Constraints:
* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

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
    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL)
            return root;
        TreeNode* new_left = invertTree(root->right);
        TreeNode* new_right = invertTree(root->left);
        root->left = new_left;
        root->right = new_right;
        return root;
    }
};
```


