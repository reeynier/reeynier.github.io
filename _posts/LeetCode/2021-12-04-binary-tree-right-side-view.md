---
layout: post
title: "Binary Tree Right Side View Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 199. Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

---

<br />

## Description

LeetCode Problem 199.

Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example 1: 
```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

Example 2:
```
Input: root = [1,null,3]
Output: [1,3]
```

Example 3:
```
Input: root = []
Output: []
```

Constraints:
* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;
        if (root == NULL)
            return ans;
        queue<TreeNode*> bfsQ;
        bfsQ.push(root);
        
        TreeNode* curr;
        int len;
        while (!bfsQ.empty()) {
            len = bfsQ.size();
            for (int i = 0; i < len; i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                if (curr != NULL) {
                    if (curr->left != NULL) {
                        bfsQ.push(curr->left);
                    }
                    if (curr->right != NULL) {
                        bfsQ.push(curr->right);
                    }
                    if (i == len - 1) {
                        ans.push_back(curr->val);
                    }
                }
            }
        }
        return ans;
    }
};
```


