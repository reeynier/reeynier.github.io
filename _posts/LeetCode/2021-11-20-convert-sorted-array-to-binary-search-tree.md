---
layout: post
title:  "Convert Sorted Array to Binary Search Tree Problem"
categories: [ Data Structure ]
tags: [ Array, Divide and Conquer, Tree, Binary Search Tree, Binary Tree Leetcode ]
similar: [ Binary Search Tree ]
featured: false
hidden: false
excerpt: LeetCode 108. Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.
---

<br />

## Description

LeetCode Problem 108. 

Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

 

Example 1:
```
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
```

Example 2:
```
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,3] and [3,1] are both a height-balanced BSTs.
```

Constraints:

* 1 <= nums.length <= 10^4
* -10^4 <= nums[i] <= 10^4
* nums is sorted in a strictly increasing order.

<br />

## Sample C++ Code


```c
class Solution {
public:
    TreeNode *sortedArrayToBST(vector<int> &num) {
        if(num.size() == 0) return NULL;
        if(num.size() == 1) return new TreeNode(num[0]);
        
        int middle = num.size()/2;
        TreeNode* root = new TreeNode(num[middle]);
        
        vector<int> leftInts(num.begin(), num.begin()+middle);
        vector<int> rightInts(num.begin()+middle+1, num.end());
        
        root->left = sortedArrayToBST(leftInts);
        root->right = sortedArrayToBST(rightInts);
        
        return root;
    }
};
```
