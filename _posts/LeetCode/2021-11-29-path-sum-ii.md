---
layout: post
title: "Path Sum II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Tree ]
similar: [ Tree ]
featured: false
hidden: false
excerpt: LeetCode 113. Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

---

<br />

## Description

LeetCode Problem 113.

Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

A root-to-leaf path is a path starting from the root and ending at any leaf node. A leaf is a node with no children.

Example 1: 
```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
```

Example 2: 
```
Input: root = [1,2,3], targetSum = 5
Output: []
```

Example 3:
```
Input: root = [1,2], targetSum = 0
Output: []
```

Constraints:
* The number of nodes in the tree is in the range [0, 5000].
* -1000 <= Node.val <= 1000
* -1000 <= targetSum <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    void getPathSum(TreeNode* root, int sum, int curr_sum, vector<int>& path, vector<vector<int>>& ans) {
        if (root == NULL)
            return;
        curr_sum += root->val;
        path.push_back(root->val);
        if ((root->left == NULL) && (root->right == NULL)) {
            if (curr_sum == sum) {
                ans.push_back(path);
            }
        }
        if (root->left != NULL)
            getPathSum(root->left, sum, curr_sum, path, ans);
        if (root->right != NULL)
            getPathSum(root->right, sum, curr_sum, path, ans);
        curr_sum -= root->val;
        path.pop_back();
    }
    
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> ans;
        vector<int> path;
        getPathSum(root, sum, 0, path, ans);
        return ans;
    }
};
```


