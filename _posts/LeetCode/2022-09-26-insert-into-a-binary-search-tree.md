---
layout: post
title: "Insert Into A Binary Search Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Binary Search Tree, Binary Tree ]
similar: [ Binary Search Tree ]
featured: false
hidden: false
excerpt: LeetCode 701. You are given the root node of a binary search tree (BST) and a value to insert into the tree. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.

---

<br />

## Description

LeetCode Problem 701.

You are given the root node of a binary search tree (BST) and a value to insert into the tree. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.

Noticethat there may existmultiple valid ways for theinsertion, as long as the tree remains a BST after insertion. You can return any of them.

Example 1: 
```
Input: root = [4,2,7,1,3], val = 5
Output: [4,2,7,1,3,5]
Explanation: Another accepted tree is:
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/05/bst.jpg" style="width: 352px; height: 301px;" />
```

Example 2:
```
Input: root = [40,20,60,10,30,50,70], val = 25
Output: [40,20,60,10,30,50,70,null,null,25]
```

Example 3:
```
Input: root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
Output: [4,2,7,1,3,5]
```

Constraints:
* The number of nodes inthe tree will be in the range [0,10^4].
* -10^8 <= Node.val <= 10^8
* All the values Node.val are unique.
* -10^8 <= val <= 10^8
* It's guaranteed that val does not exist in the original BST.

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
    TreeNode* insertIntoBST(TreeNode *node, int val) {
        if (!node) {
            TreeNode *newNode = new TreeNode(val);
            return newNode;
        }
        if (val < node->val) {
            node->left = insertIntoBST(node->left, val);
        }
        else {
            node->right = insertIntoBST(node->right, val);
        }
        return node;
    }
};
```


