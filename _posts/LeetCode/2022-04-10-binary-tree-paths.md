---
layout: post
title: "Binary Tree Paths Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Backtracking, Tree, Depth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 257. Given the root of a binary tree, return all root-to-leaf paths in any order.

---

<br />

## Description

LeetCode Problem 257.

Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

Example 1:
```
Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]
```

Example 2:
```
Input: root = [1]
Output: ["1"]
```

Constraints:
* The number of nodes in the tree is in the range [1, 100].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    void dfs(TreeNode* root, vector<string> &result, string s) {
        if (root->left == NULL && root->right == NULL) {
            result.push_back(s);
            return;
        }
        if (root->left)
            dfs(root->left, result, s + "->" + to_string(root->left->val));
        if (root->right)
            dfs(root->right, result, s + "->" + to_string(root->right->val));
        return;
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        if (root == NULL)
            return result;
        dfs(root, result, to_string(root->val));
        return result;
    }
};
```


