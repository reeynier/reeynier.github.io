---
layout: post
title: "Path Sum III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 437. Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the valuesalong the path equalstargetSum.

---

<br />

## Description

LeetCode Problem 437.

Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the valuesalong the path equalstargetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

Example 1: 
```
Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.
```

Example 2:
```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: 3
```

Constraints:
* The number of nodes in the tree is in the range [0, 1000].
* -10^9 <= Node.val <= 10^9
* -1000 <= targetSum <= 1000

<br />

## Sample C++ Code using Depth-First Search 


```c
class Solution {
public:
    int pathSum(TreeNode* root, int sum) {
        if(!root) return 0;
        return sumUp(root, 0, sum) + pathSum(root->left, sum) + pathSum(root->right, sum);
    }
private:
    int sumUp(TreeNode* root, int pre, int& sum){
        if(!root) return 0;
        int current = pre + root->val;
        return (current == sum) + sumUp(root->left, current, sum) + sumUp(root->right, current, sum);
    }
};
```


