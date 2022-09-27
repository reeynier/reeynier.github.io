---
layout: post
title: "Longest Univalue Path Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 687. Given the root of a binary tree, return the length of the longest path, where each node in the path has the same value. This path may or may not pass through the root.

---

<br />

## Description

LeetCode Problem 687.

Given the root of a binary tree, return the length of the longest path, where each node in the path has the same value. This path may or may not pass through the root.

The length of the path between two nodes is represented by the number of edges between them.

Example 1: 
```
Input: root = [5,4,5,1,1,5]
Output: 2
```

Example 2: 
```
Input: root = [1,4,5,4,4,5]
Output: 2
```

Constraints:
* The number of nodes in the tree is in the range [0, 10^4].
* -1000 <= Node.val <= 1000
* The depth of the tree will not exceed 1000.

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
    int longestPath(TreeNode* root, int& max_path) {
        if (root == NULL)
            return 0;
        int left_path = longestPath(root->left, max_path);
        int right_path = longestPath(root->right, max_path);
        if ((root->left != NULL) && (root->val == root->left->val)) {
            left_path ++;
        } else {
            left_path = 0;
        }
        if ((root->right != NULL) && (root->val == root->right->val)) {
            right_path ++;
        } else {
            right_path = 0;
        }
        max_path = max(max_path, left_path + right_path);
        return max(left_path, right_path);
    }
    
    int longestUnivaluePath(TreeNode* root) {
        int max_path = 0;
        int val = longestPath(root, max_path);
        return max_path;
    }
};
```


