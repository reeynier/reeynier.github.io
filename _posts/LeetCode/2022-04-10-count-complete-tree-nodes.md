---
layout: post
title: "Count Complete Tree Nodes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Binary Search, Tree, Depth-First Search, Binary Tree ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 222. Given the root of a complete binary tree, return the number of the nodes in the tree.

---

<br />

## Description

LeetCode Problem 222.

Given the root of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2^h nodes inclusive at the last level h.

Design an algorithm that runs in less than O(n) time complexity.

Example 1:
```
Input: root = [1,2,3,4,5,6]
Output: 6
```

Example 2:
```
Input: root = []
Output: 0
```

Example 3:
```
Input: root = [1]
Output: 1
```

Constraints:
* The number of nodes in the tree is in the range [0, 5 * 10^4].
* 0 <= Node.val <= 5 * 10^4
* The tree is guaranteed to be complete.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(!root) 
        	return 0;

        int hl=0, hr=0;
        TreeNode *l=root, *r=root;

        while (l) {
        	hl ++;
        	l = l->left;
        }

        while (r) {
        	hr ++;
        	r = r->right;
        }

        if (hl==hr) 
        	return pow(2,hl)-1;

        return 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```


