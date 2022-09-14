---
layout: post
title: "Kth Smallest Element In A BST Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Search Tree, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 230. Given the root of a binary search tree, and an integer k, return the k^th smallest value (1-indexed) of all the values of the nodes in the tree.

---

<br />

## Description

LeetCode Problem 230.

Given the root of a binary search tree, and an integer k, return the k^th smallest value (1-indexed) of all the values of the nodes in the tree.

Example 1:
```
Input: root = [3,1,4,null,2], k = 1
Output: 1
```

Example 2:
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```

Constraints:
* The number of nodes in the tree is n.
* 1 <= k <= n <= 10^4
* 0 <= Node.val <= 10^4

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
    vector<int> sorted;
    void inorder(TreeNode* node) {
        if (node == NULL)
            return;
        inorder(node->left);
        sorted.push_back(node->val);
        inorder(node->right);
    }
    
    int kthSmallest(TreeNode* root, int k) {
        inorder(root);
        return sorted[k-1];
    }
};
```


