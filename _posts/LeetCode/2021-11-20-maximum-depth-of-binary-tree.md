---
layout: post
title:  "Maximum Depth of Binary Tree Problem"
categories: [ Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree, Leetcode ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 104. Given the root of a binary tree, return its maximum depth.
---

<br />

## Description

LeetCode Problem 104. 

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

 

Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

Example 2:
```
Input: root = [1,null,2]
Output: 2
```

Example 3:
```
Input: root = []
Output: 0
```

Example 4:
```
Input: root = [0]
Output: 1
```

Constraints:

* The number of nodes in the tree is in the range [0, 10^4].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL)
            return 0;
        else if ((root->left == NULL) && (root->right == NULL))
            return 1;
        else if (root->left == NULL)
            return maxDepth(root->right) + 1;
        else if (root->right == NULL)
            return maxDepth(root->left) + 1;
        else
            return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```
