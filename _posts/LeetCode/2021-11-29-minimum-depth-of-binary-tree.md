---
layout: post
title: "Minimum Depth Of Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 111. Given a binary tree, find its minimum depth.

---

<br />

## Description

LeetCode Problem 111.

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: 2
```

Example 2:
```
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5
```

Constraints:
* The number of nodes in the tree is in the range [0, 10^5].
* -1000 <= Node.val <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (root == NULL)
            return 0;
        if ((root->left == NULL) && (root->right == NULL))
            return 1;
        else if (root->left == NULL)
            return minDepth(root->right) + 1;
        else if (root->right == NULL)
            return minDepth(root->left) + 1;
        else 
            return min(minDepth(root->left), minDepth(root->right)) + 1;
    }
};
```


