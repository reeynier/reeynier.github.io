---
layout: post
title:  "Binary Tree Level Order Traversal Problem"
categories: [ Data Structure ]
tags: [ Tree, Breadth-First Search, Binary Tree, Leetcode ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 102. Given the root of a binary tree, return the level order traversal of its nodes' values.
---

<br />

## Description

LeetCode Problem 102. 

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).


Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

Example 2:
```
Input: root = [1]
Output: [[1]]
```

Example 3:
```
Input: root = []
Output: []
```

Constraints:

* The number of nodes in the tree is in the range [0, 2000].
* -1000 <= Node.val <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> levelOrder;
        queue<TreeNode*> bfsQ;
        queue<int> levelQ;
        if (root == NULL)
            return levelOrder;
        bfsQ.push(root);
        levelQ.push(1);
        
        TreeNode* curr;
        vector<int> currLevel;
        int level;
        int lastLevel = 1;
        while (!bfsQ.empty()) {
            curr = bfsQ.front();
            bfsQ.pop();
            level = levelQ.front();
            levelQ.pop();
            if (level > lastLevel) {
                levelOrder.push_back(currLevel);
                currLevel.clear();
            }
            if (curr != NULL) {
                currLevel.push_back(curr->val);
                bfsQ.push(curr->left);
                bfsQ.push(curr->right);
                levelQ.push(level+1);
                levelQ.push(level+1);
            }    
            lastLevel = level;
            
        }
        return levelOrder;
    }
};
```
