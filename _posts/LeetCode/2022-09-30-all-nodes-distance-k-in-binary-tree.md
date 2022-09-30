---
layout: post
title: "All Nodes Distance K In Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 863. Given the root of a binary tree, the value of a target node target, and an integer k, return an array of the values of all nodes that have a distance k from the target node.

---

<br />

## Description

LeetCode Problem 863.

Given the root of a binary tree, the value of a target node target, and an integer k, return an array of the values of all nodes that have a distance k from the target node.

You can return the answer in any order.

Example 1: 
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, k = 2
Output: [7,4,1]
Explanation: The nodes that are a distance 2 from the target node (with value 5) have values 7, 4, and 1.
```

Example 2:
```
Input: root = [1], target = 1, k = 3
Output: []
```

Constraints:
* The number of nodes in the tree is in the range [1, 500].
* 0 <= Node.val <= 500
* All the values Node.val are unique.
* target is the value of one of the nodes in the tree.
* 0 <= k <= 1000

<br />

## Sample C++ Code


```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<TreeNode*> path(TreeNode *root, int val) {
        if (!root) 
            return {};
        if (root->val == val) 
            return {root};
        vector<TreeNode*> l, r;
        l = path(root->left, val);
        r = path(root->right, val);
        if (l.size()) {
            l.push_back(root); 
            return l;
        }
        if (r.size()) {
            r.push_back(root); 
            return r;
        }
        return {};
    }
    
    void distance(TreeNode *root, int k, TreeNode* before, vector<int> &ans) {
        if (!root || root == before) 
            return;
        distance(root->left, k - 1, before, ans);
        distance(root->right, k - 1, before, ans);
        if (k == 0) 
            ans.push_back(root->val);
        return;
    }
    
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        vector<TreeNode*> v = path(root, target->val);
        vector<int> ans;
        for (int i = 0; i < v.size() && k >= i; i++)
            distance(v[i], k - i, i == 0 ? NULL : v[i - 1], ans);
        return ans;
    }
};
```


