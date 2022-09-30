---
layout: post
title: "All Possible Full Binary Trees Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Tree, Recursion, Memoization, Binary Tree ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 894. Given an integer n, return a list of all possible full binary trees with n nodes. Each node of each tree in the answer must have Node.val == 0.

---

<br />

## Description

LeetCode Problem 894.

Given an integer n, return a list of all possible full binary trees with n nodes. Each node of each tree in the answer must have Node.val == 0.

Each element of the answer is the root node of one possible tree. You may return the final list of trees in any order.

A full binary tree is a binary tree where each node has exactly 0 or 2 children.

Example 1: 
```
Input: n = 7
Output: [[0,0,0,null,null,0,0,null,null,0,0],[0,0,0,null,null,0,0,0,0],[0,0,0,0,0,0,0],[0,0,0,0,0,null,null,null,null,0,0],[0,0,0,0,0,null,null,0,0]]
```

Example 2:
```
Input: n = 3
Output: [[0,0,0]]
```

Constraints:
* 1 <= n <= 20

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
    vector<TreeNode*> allPossibleFBT(int N) {
        vector<TreeNode*> ans;
        TreeNode* root = new TreeNode(0);
        if (N == 1) {
            ans.push_back(root);
            return ans;
        } else if (N % 2 == 1) {
            for (int x = 0; x < N; x ++) {
                int y = N - x - 1;
                vector<TreeNode*> left_ans = allPossibleFBT(x);
                vector<TreeNode*> right_ans = allPossibleFBT(y);
                for (vector<TreeNode*>::iterator it1 = left_ans.begin(); 
                    it1 != left_ans.end(); it1 ++) {
                    for (vector<TreeNode*>::iterator it2 = right_ans.begin(); 
                        it2 != right_ans.end(); it2 ++) {
                        TreeNode* top = new TreeNode(0);
                        top->left = *it1;
                        top->right = *it2;
                        ans.push_back(top);
                    }
                }
            }
        }
        return ans;
    }
};
```


