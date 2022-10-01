---
layout: post
title: "Construct Binary Tree From Preorder And Postorder Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Divide and Conquer, Tree, Binary Tree ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 889. Given two integer arrays, preorder and postorder where preorder is the preorder traversal of a binary tree of distinct values and postorder is the postorder traversal of the same tree, reconstruct and return the binary tree.

---

<br />

## Description

LeetCode Problem 889.

Given two integer arrays, preorder and postorder where preorder is the preorder traversal of a binary tree of distinct values and postorder is the postorder traversal of the same tree, reconstruct and return the binary tree.

If there exist multiple answers, you can return any of them.

Example 1: 
```
Input: preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
Output: [1,2,3,4,5,6,7]
```

Example 2:
```
Input: preorder = [1], postorder = [1]
Output: [1]
```

Constraints:
* 1 <= preorder.length <= 30
* 1 <= preorder[i] <= preorder.length
* All the values of preorder are unique.
* postorder.length == preorder.length
* 1 <= postorder[i] <= postorder.length
* All the values of postorder are unique.
* It is guaranteed that preorder and postorder are the preorder traversal and postorder traversal of the same binary tree.

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
    int preidx = 0, postidx = 0;
    TreeNode* constructFromPrePost(vector<int>& pre, vector<int>& post) {
        TreeNode* root = new TreeNode(pre[preidx ++]);
        if (root->val != post[postidx])
            root->left = constructFromPrePost(pre, post);
        if (root->val != post[postidx])
            root->right = constructFromPrePost(pre, post);
        postidx ++;
        return root;
    }
};
```


