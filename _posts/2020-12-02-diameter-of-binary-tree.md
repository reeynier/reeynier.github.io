---
layout: post
title:  "Diameter of Binary Tree Problem"
categories: [ Data Structure ]
tags: [ Tree, Depth First Search, Leetcode ]
similar: [ DFS ]
featured: false
hidden: false
excerpt: LeetCode 543. Given a binary tree, compute the diameter of the tree.
---

<br />

## Description

LeetCode Problem 543. Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example: 
```
Input: 
        1
       / \
      2   3
     / \
    4   5
Output: 3
Explanation: The diameter of this tree is the length of the path [4,2,1,3] or [5,2,1,3].
Note: The length of path between two nodes is represented by the number of edges between them.
```

<br />

## Solution

#### Depth First Search

We can use `depth first search` to explore every node in the tree. 

During the search, we calculate the depth of each node. The depth of the node means if we treat the node as the root node of a tree, the maximum number of edges from the root node to the leaf node in the tree. The depth of the node can be calculated recursively. It equals to the maximum of the depth of the left child node and the depth of the right child node. If the node is NULL, the depth of this node is 0.

Calculating the depth of each node can be useful for calculating the diameter of the tree. The path length of the tree **across a node** equals the sum of the depth of the left child node and the depth of the right child node plus 1. We can use a global variable to keep track of the maximum path length.

The time complexity is O(n) because we visit every node once.

<br />

## Sample C++ Code


This is a C++ implementation of the above approach.

```c
#include <iostream>
#include <algorithm>

using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {} 
};

int diameter;
int getDepth(TreeNode* node) {
    if (node == NULL)
        return 0;
    int l = getDepth(node->left);
    int r = getDepth(node->right);
    diameter = max(diameter, l + r);
    return max(l, r) + 1;
}
int diameterOfBinaryTree(TreeNode* root) {
    diameter = 0;
    getDepth(root);
    return diameter;
}

int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    cout << diameterOfBinaryTree(root) << endl;
}
```
