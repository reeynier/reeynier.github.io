---
layout: post
title: "Binary Tree Postorder Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Stack, Tree, Depth-First Search, Binary Tree ]
similar: [ Tree ]
featured: false
hidden: false
excerpt: LeetCode 145. Given the root of abinary tree, return the postorder traversal of its nodes' values.

---

<br />

## Description

LeetCode Problem 145.

Given the root of abinary tree, return the postorder traversal of its nodes' values.

Example 1: 
```
Input: root = [1,null,2,3]
Output: [3,2,1]
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
Output: [2,1]
```

Example 5: 
```
Input: root = [1,null,2]
Output: [2,1]
```

Constraints:
* The number of the nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> postorder;
        if (root == NULL)
            return postorder;
        stack<TreeNode*> s1, s2;
        s1.push(root);
        
        TreeNode* curr;
        while(!s1.empty()) {
            curr = s1.top();
            s1.pop();
            if (curr->left != NULL)
                s1.push(curr->left);
            if (curr->right != NULL)
                s1.push(curr->right);
            s2.push(curr);
        }
        while(!s2.empty()) {
            curr = s2.top();
            postorder.push_back(curr->val);
            s2.pop();
        }
        return postorder;
    }
};
```


