---
layout: post
title: "Two Sum IV - Input Is A BST Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Two Pointers, Tree, Depth-First Search, Breadth-First Search, Binary Search Tree, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 653. Given the root of a Binary Search Tree and a target number k, return true if there exist two elements in the BST such that their sum is equal to the given target.

---

<br />

## Description

LeetCode Problem 653.

Given the root of a Binary Search Tree and a target number k, return true if there exist two elements in the BST such that their sum is equal to the given target.

Example 1: 
```
Input: root = [5,3,6,2,4,null,7], k = 9
Output: true
```

Example 2: 
```
Input: root = [5,3,6,2,4,null,7], k = 28
Output: false
```

Example 3:
```
Input: root = [2,1,3], k = 4
Output: true
```

Example 4:
```
Input: root = [2,1,3], k = 1
Output: false
```

Example 5:
```
Input: root = [2,1,3], k = 3
Output: true
```

Constraints:
* The number of nodes in the tree is in the range [1, 10^4].
* -10^4<= Node.val <= 10^4
* root is guaranteed to be a valid binary search tree.
* -10^5<= k <= 10^5

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
    map<int, int> m;
    bool findTarget(TreeNode* root, int k) {
        if (root == NULL)
            return false;
        if (m.find(k-root->val) != m.end()) {
            return true;
        }
        m[root->val] = 1;
        return findTarget(root->left, k) || findTarget(root->right, k);
    }
};
```


