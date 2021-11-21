---
layout: post
title:  "Binary Tree Zigzag Level Order Traversal Problem"
categories: [ Data Structure ]
tags: [ Tree, Breadth-First Search, Binary Tree, Leetcode ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 103. Given the root of a binary tree, return the zigzag level order traversal of its nodes' values.
---

<br />

## Description

LeetCode Problem 103. 

Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

 

Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
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
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if (root == NULL)
            return ans;
        
        queue<TreeNode*> bfsQ;
        bfsQ.push(root);
        int len = 1, cnt = 1;
        vector<int> line;
        TreeNode* curr;
        while (!bfsQ.empty()) {
            len = bfsQ.size();
            line.clear();
            for (int i = 0; i < len; i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                if (curr != NULL) {
                    line.push_back(curr->val);
                    bfsQ.push(curr->left);
                    bfsQ.push(curr->right);
                } 
            }
            if (cnt % 2 == 0)
                reverse(line.begin(), line.end());
            cnt ++;
            if (!line.empty())
                ans.push_back(line);
        }
        return ans;
    }
};
```
