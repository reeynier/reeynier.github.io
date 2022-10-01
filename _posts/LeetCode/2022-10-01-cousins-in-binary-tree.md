---
layout: post
title: "Cousins In Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 993. Given the root of a binary tree with unique values and the values of two different nodes of the tree x and y, return true if the nodes corresponding to the values x and y in the tree are cousins, or false otherwise.

---

<br />

## Description

LeetCode Problem 993.

Given the root of a binary tree with unique values and the values of two different nodes of the tree x and y, return true if the nodes corresponding to the values x and y in the tree are cousins, or false otherwise.

Two nodes of a binary tree are cousins if they have the same depth with different parents.
Note that in a binary tree, the root node is at the depth 0, and children of each depth k node are at the depth k + 1.

Example 1: 
```
Input: root = [1,2,3,4], x = 4, y = 3
Output: false
```

Example 2: 
```
Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
```

Example 3: 
```
Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
```

Constraints:
* The number of nodes in the tree is in the range [2, 100].
* 1 <= Node.val <= 100
* Each node has a unique value.
* x != y
* x and y are exist in the tree.

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
    void rec(TreeNode* root, int x, int y, int d, int parent) {
        if (!root) return;
        
        if (root->val == x) 
            dx = d, x_par = parent;
        if (root->val == y) 
            dy = d, y_par = parent;
        
        if (dx != -1 && dy != -1) return;
        
        rec(root->left, x, y, d+1, root->val);
        rec(root->right, x, y, d+1, root->val);
    }
    
    bool isCousins(TreeNode* root, int x, int y) {
        rec(root, x, y, 0, -1);
        return dx == dy && x_par != y_par;
    }
    
private:
    int dx = -1, dy = -1, x_par = -1, y_par = -1;
};
```


