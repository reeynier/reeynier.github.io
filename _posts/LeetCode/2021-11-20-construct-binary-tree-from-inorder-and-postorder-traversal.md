---
layout: post
title:  "Construct Binary Tree From Inorder And Postorder Traversal Problem"
categories: [ Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree, Leetcode ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 106. Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.
---

<br />

## Description

LeetCode Problem 106. 

Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.

 

Example 1:
```
Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
Output: [3,9,20,null,null,15,7]
```

Example 2:
```
Input: inorder = [-1], postorder = [-1]
Output: [-1]
```

Constraints:

* 1 <= inorder.length <= 3000
* postorder.length == inorder.length
* -3000 <= inorder[i], postorder[i] <= 3000
* inorder and postorder consist of unique values.
* Each value of postorder also appears in inorder.
* inorder is guaranteed to be the inorder traversal of the tree.
* postorder is guaranteed to be the postorder traversal of the tree.

<br />

## Sample C++ Code


```c
TreeNode *buildTree(vector<int> &inorder, vector<int> &postorder) {
    return create(inorder, postorder, 0, inorder.size() - 1, 0, postorder.size() - 1);
}

TreeNode* create(vector<int> &inorder, vector<int> &postorder, int is, int ie, int ps, int pe){
    if(ps > pe){
        return nullptr;
    }
    TreeNode* node = new TreeNode(postorder[pe]);
    int pos;
    for(int i = is; i <= ie; i++){
        if(inorder[i] == node->val){
            pos = i;
            break;
        }
    }
    node->left = create(inorder, postorder, is, pos - 1, ps, ps + pos - is - 1);
    node->right = create(inorder, postorder, pos + 1, ie, pe - ie + pos, pe - 1);
    return node;
}
```
