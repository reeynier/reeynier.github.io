---
layout: post
title: "Binary Tree Preorder Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Stack, Tree, Depth-First Search, Binary Tree ]
similar: [ Tree ]
featured: false
hidden: false
excerpt: LeetCode 144. Given the root of a binary tree, return the preorder traversal of its nodes' values.

---

<br />

## Description

LeetCode Problem 144.

Given the root of a binary tree, return the preorder traversal of its nodes' values.

Example 1: 
```
Input: root = [1,null,2,3]
Output: [1,2,3]
```

Example 2:
```
Input: root = []
Output: []
```

Example 3:
```
Input: root = [1]
Output: [1]
```

Example 4: 
```
Input: root = [1,2]
Output: [1,2]
```

Example 5: 
```
Input: root = [1,null,2]
Output: [1,2]
```

Constraints:
* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> preorder;
        
        if (root == NULL)
            return preorder;
        
        stack<TreeNode*> s;
        s.push(root);
        TreeNode* tp;
        
        while (!s.empty()) {
            tp = s.top();
            s.pop();
            if (tp == NULL)
                continue;
            s.push(tp->right);
            s.push(tp->left);
            preorder.push_back(tp->val);
        }
        return preorder;
    }
};
```


