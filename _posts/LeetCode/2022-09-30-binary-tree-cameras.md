---
layout: post
title: "Binary Tree Cameras Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Tree, Depth-First Search, Binary Tree ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 968. You are given the root of a binary tree. We install cameras on the tree nodes where each camera at a node can monitor its parent, itself, and its immediate children.

---

<br />

## Description

LeetCode Problem 968.

You are given the root of a binary tree. We install cameras on the tree nodes where each camera at a node can monitor its parent, itself, and its immediate children.

Return the minimum number of cameras needed to monitor all nodes of the tree.

Example 1: 
```
Input: root = [0,0,null,0,0]
Output: 1
Explanation: One camera is enough to monitor all nodes if placed as shown.
```

Example 2: 
```
Input: root = [0,0,null,0,null,0,null,null,0]
Output: 2
Explanation: At least two cameras are needed to monitor all nodes of the tree. The above image shows one of the valid configurations of camera placement.
```

Constraints:
* The number of nodes in the tree is in the range [1, 1000].
* Node.val == 0

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
    #define NO_CAMERA       0
    #define HAS_CAMERA      2
    #define NOT_NEEDED      1
    int ans = 0;
    int dfs(TreeNode *root) {
        if (!root) return NOT_NEEDED;
        int l = dfs(root->left);
        int r = dfs(root->right);
        if (l == NO_CAMERA || r == NO_CAMERA) {
            ans++;
            return HAS_CAMERA;
        } else if (l == HAS_CAMERA || r == HAS_CAMERA) {
            return NOT_NEEDED;
        } else {
            return NO_CAMERA;
        }
    }
    int minCameraCover(TreeNode* root) {
        if (dfs(root) == NO_CAMERA) ans++;
        return ans;
    }
};
```


