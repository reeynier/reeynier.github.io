---
layout: post
title: "Flip Binary Tree To Match Preorder Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 971. You are given the root of a binary tree with n nodes, where each node is uniquely assigned a value from 1 to n. You are also given a sequence of n values voyage,

---

<br />

## Description

LeetCode Problem 971.

You are given the root of a binary tree with n nodes, where each node is uniquely assigned a value from 1 to n. You are also given a sequence of n values voyage, which is the desired pre-order traversal of the binary tree.

Any node in the binary tree can be flipped by swapping its left and right subtrees. 

Flip the smallest number of nodes so that the pre-order traversal of the tree matches voyage.

Return a list of the values of all flipped nodes. You may return the answer in any order. If it is impossible to flip the nodes in the tree to make the pre-order traversal match voyage, return the list [-1].

Example 1: 
```
Input: root = [1,2], voyage = [2,1]
Output: [-1]
Explanation: It is impossible to flip the nodes such that the pre-order traversal matches voyage.
```

Example 2: 
```
Input: root = [1,2,3], voyage = [1,3,2]
Output: [1]
Explanation: Flipping node 1 swaps nodes 2 and 3, so the pre-order traversal matches voyage.
```

Example 3:
```
Input: root = [1,2,3], voyage = [1,2,3]
Output: []
Explanation: The tree's pre-order traversal already matches voyage, so no nodes need to be flipped.
```

Constraints:
* The number of nodes in the tree is n.
* n == voyage.length
* 1 <= n <= 100
* 1 <= Node.val, voyage[i] <= n
* All the values in the tree are unique.
* All the values in voyage are unique.

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
private:
    vector<int> m_voyage;
    vector<int> res;
    int i = 0;
    
public:
    bool rec(TreeNode* root) {
        if (!root) return true;
        if (root->val != m_voyage[i++]) {
            return false;
        }
        if (root->left && root->left->val != m_voyage[i]) {
            res.push_back(root->val);
            return rec(root->right) && rec(root->left);
        }
        else
            return rec(root->left) && rec(root->right);
    }
    
    vector<int> flipMatchVoyage(TreeNode* root, vector<int>& voyage) {
        m_voyage = voyage;
        return rec(root) ? res : vector<int>{-1};
    }
};
```


