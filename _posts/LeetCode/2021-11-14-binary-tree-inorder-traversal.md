---
layout: post
title:  "Binary Tree Inorder Traversal Problem"
categories: [ Data Structure ]
tags: [ Stack, Tree, Depth-First Search, Binary Tree, Leetcode ]
similar: [ Binary Tree ]
featured: false
hidden: false
excerpt: LeetCode 94. Given an m x n grid of characters board and a string word, return true if word exists in the grid.
---

<br />

## Description

LeetCode Problem 94. 

Given the root of a binary tree, return the inorder traversal of its nodes' values.

 

Example 1:
```
Input: root = [1,null,2,3]
Output: [1,3,2]
```

Example 2:
```
Input: root = []
Output: []
```

Example 3:
```
Input: root = [1]
Output: [1]
```

Example 4:
```
Input: root = [1,2]
Output: [2,1]
```

Example 5:
```
Input: root = [1,null,2]
Output: [1,2]
```

Constraints:

* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100


<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> nodes;
        inorder(root, nodes);
        return nodes;
    }

    void inorder(TreeNode* root, vector<int>& nodes) {
        if (!root) {
            return;
        }
        inorder(root -> left, nodes);
        nodes.push_back(root -> val);
        inorder(root -> right, nodes);
    }
};
```

```c
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> nodes;
        stack<TreeNode*> todo;
        while (root || !todo.empty()) {
            while (root) {
                todo.push(root);
                root = root -> left;
            }
            root = todo.top();
            todo.pop();
            nodes.push_back(root -> val);
            root = root -> right;
        }
        return nodes;
    }
};
```
