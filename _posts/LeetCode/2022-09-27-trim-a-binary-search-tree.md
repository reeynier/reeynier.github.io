---
layout: post
title: "Trim A Binary Search Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Search Tree, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 669. Given the root of a binary search tree and the lowest and highest boundaries as low and high, trim the tree so that all its elements lies in [low, high]. Trimming the tree should not change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a unique answer.

---

<br />

## Description

LeetCode Problem 669.

Given the root of a binary search tree and the lowest and highest boundaries as low and high, trim the tree so that all its elements lies in [low, high]. Trimming the tree should not change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a unique answer.

Return the root of the trimmed binary search tree. Note that the root may change depending on the given bounds.

Example 1: 
```
Input: root = [1,0,2], low = 1, high = 2
Output: [1,null,2]
```

Example 2: 
```
Input: root = [3,0,4,null,2,null,null,1], low = 1, high = 3
Output: [3,2,null,1]
```

Example 3:
```
Input: root = [1], low = 1, high = 2
Output: [1]
```

Example 4:
```
Input: root = [1,null,2], low = 1, high = 3
Output: [1,null,2]
```

Example 5:
```
Input: root = [1,null,2], low = 2, high = 4
Output: [2]
```

Constraints:
* The number of nodes in the tree in the range [1, 10^4].
* 0 <= Node.val <= 10^4
* The value of each node in the tree is unique.
* root is guaranteed to be a valid binary search tree.
* 0 <= low <= high <= 10^4

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
    TreeNode* trimBST(TreeNode* root, int L, int R) {
        if (root == NULL)
            return NULL;
        TreeNode* node;
        if (root->val < L) {
            node = root->right;
            root->right = NULL;
            return trimBST(node, L, R);
        } else if (root->val > R) {
            node = root->left;
            root->left = NULL;
            return trimBST(node, L, R);
        } else {
            root->left = trimBST(root->left, L, R);
            root->right = trimBST(root->right, L, R);
            return root;
        }
    }
};
```


