---
layout: post
title: "Binary Tree Maximum Path Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Tree, Depth-First Search, Binary Tree ]
similar: []
featured: false
hidden: false
excerpt: LeetCode 124. A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.
---

<br />

## Description

LeetCode Problem 124.

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

Example 1: 
```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

Example 2: 
```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```

Constraints:
* The number of nodes in the tree is in the range [1, 3 * 10^4].
* -1000 <= Node.val <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int dfsMaxSum(TreeNode* root, int &max_sum) {
        if (root == NULL)
            return 0;
        int left_sum = dfsMaxSum(root->left, max_sum);
        int right_sum = dfsMaxSum(root->right, max_sum);
        
        int temp = max(max(left_sum, right_sum) + root->val, root->val);
        max_sum = max(max_sum, max(temp, left_sum + right_sum + root->val));
        
        return temp;
        
    }
    int maxPathSum(TreeNode* root) {
        if (root == NULL)
            return 0;
        int max_sum = root->val;
        int val = dfsMaxSum(root, max_sum);
        return max_sum;
    }
};
```


