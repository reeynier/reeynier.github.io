---
layout: post
title: "Find Bottom Left Tree Value Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 513. Given the root of a binary tree, return the leftmost value in the last row of the tree.

---

<br />

## Description

LeetCode Problem 513.

Given the root of a binary tree, return the leftmost value in the last row of the tree.

Example 1: 
```
Input: root = [2,1,3]
Output: 1
```

Example 2: 
```
Input: root = [1,2,3,4,null,5,6,null,null,7]
Output: 7
```

Constraints:
* The number of nodes in the tree is in the range [1, 10^4].
* -2^31 <= Node.val <= 2^31 - 1

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
    int findBottomLeftValue(TreeNode* root) {
        if (root == NULL)
            return 0;
        
        queue<TreeNode*> bfsQ;
        bfsQ.push(root);
        
        TreeNode* curr;
        int len, leftmost;
        
        while (!bfsQ.empty()) {
            len = bfsQ.size();
            
            for (int i = 0; i < len; i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                
                if (i == 0)
                    leftmost = curr->val;
                
                if (curr->left != NULL)
                    bfsQ.push(curr->left);
                
                if (curr->right != NULL)
                    bfsQ.push(curr->right);
            }
        }
        
        return leftmost;
    }
};
```


