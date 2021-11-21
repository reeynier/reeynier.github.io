---
layout: post
title:  "Binary Tree Level Order Traversal II Problem"
categories: [ Data Structure ]
tags: [ Tree, Breadth-First Search, Binary Tree, Leetcode ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 107. Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. 
---

<br />

## Description

LeetCode Problem 107. 

Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).

 

Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]
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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> levelOrder, reverseLevelOrder;
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
        for (vector<vector<int>>::reverse_iterator rvit = levelOrder.rbegin(); 
            rvit != levelOrder.rend(); rvit ++) {
            reverseLevelOrder.push_back(*rvit);
        }
        return reverseLevelOrder;
    }
};
```
