---
layout: post
title: "Univalued Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 965. A binary tree is uni-valued if every node in the tree has the same value.

---

<br />

## Description

LeetCode Problem 965.

A binary tree is uni-valued if every node in the tree has the same value.

Given the root of a binary tree, return true if the given tree is uni-valued, or false otherwise.

Example 1: 
```
Input: root = [1,1,1,1,1,null,1]
Output: true
```

Example 2: 
```
Input: root = [2,2,2,5,2]
Output: false
```

Constraints:
* The number of nodes in the tree is in the range [1, 100].
* 0 <= Node.val < 100

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
    bool isUnivalTree(TreeNode* root) {
        if (root == NULL)
            return true;
        else if ((root->left == NULL) && (root->right == NULL))
            return true;
        else if (root->left == NULL)
            return ((root->val == root->right->val) && isUnivalTree(root->right));
        else if (root->right == NULL)
            return ((root->val == root->left->val) && isUnivalTree(root->left));
        else
            return ((root->val == root->left->val) && (root->val == root->right->val) &&
                   isUnivalTree(root->left) && isUnivalTree(root->right));
    }
};
```


