---
layout: post
title: "Add One Row To Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 623. Given the root of a binary tree and two integers val and depth, add a row of nodes with value val at the given depth depth.

---

<br />

## Description

LeetCode Problem 623.

Given the root of a binary tree and two integers val and depth, add a row of nodes with value val at the given depth depth.

Note that the root node is at depth 1.

The adding rule is:
* Given the integer depth, for each not null tree node cur at the depth depth - 1, create two tree nodes with value val as cur's left subtree root and right subtree root.
* cur's original left subtree should be the left subtree of the new left subtree root.
* cur's original right subtree should be the right subtree of the new right subtree root.
* If depth == 1 that means there is no depth depth - 1 at all, then create a tree node with value val as the new root of the whole original tree, and the original tree is the new root's left subtree.

Example 1: 
```
Input: root = [4,2,6,3,1,5], val = 1, depth = 2
Output: [4,1,1,2,null,null,6,3,1,5]
```

Example 2: 
```
Input: root = [4,2,null,3,1], val = 1, depth = 3
Output: [4,2,null,1,1,3,null,null,1]
```

Constraints:
* The number of nodes in the tree is in the range [1, 10^4].
* The depth of the tree is in the range [1, 10^4].
* -100 <= Node.val <= 100
* -10^5 <= val <= 10^5
* 1 <= depth <= the depth of tree + 1

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
    TreeNode* addOneRow(TreeNode* root, int v, int d) {
        if (d == 1) {
            TreeNode* newroot = new TreeNode(v);
            newroot->left = root;
            return newroot;
        }
        else if (d == 0) {
            TreeNode* newroot = new TreeNode(v);
            newroot->right = root;
            return newroot;
        }

        if (!root) {
            return nullptr;
        }
        else if (d == 2) {
            root->left  = addOneRow(root->left,  v, 1);
            root->right = addOneRow(root->right, v, 0);
            return root;
        }
        else if (d > 2) {
            root->left  = addOneRow(root->left,  v, d - 1);
            root->right = addOneRow(root->right, v, d - 1);
        }
        return root;
    }
};
```


