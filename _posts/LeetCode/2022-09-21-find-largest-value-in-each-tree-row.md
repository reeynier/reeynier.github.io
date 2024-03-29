---
layout: post
title: "Find Largest Value In Each Tree Row Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 515. Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

---

<br />

## Description

LeetCode Problem 515.

Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

Example 1: 
```
Input: root = [1,3,2,5,3,null,9]
Output: [1,3,9]
```

Example 2:
```
Input: root = [1,2,3]
Output: [1,3]
```

Example 3:
```
Input: root = [1]
Output: [1]
```

Example 4:
```
Input: root = [1,null,2]
Output: [1,2]
```

Example 5:
```
Input: root = []
Output: []
```

Constraints:
* The number of nodes in the tree will be in the range [0, 10^4].
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
    vector<int> largestValues(TreeNode* root) {
        vector<int> ans;
        if (root == NULL)
            return ans;
        
        queue<TreeNode*> bfsQ;
        bfsQ.push(root);
        
        TreeNode* curr;
        int len;
        int max_node;

        while (!bfsQ.empty()) {
            len = bfsQ.size();
            max_node = bfsQ.front()->val;

            for (int i = 0; i < len; i ++) {
                curr = bfsQ.front(); 
                bfsQ.pop();

                if (curr != NULL) {
                    if (curr->val > max_node)
                        max_node = curr->val;
                    if (curr->left != NULL)
                        bfsQ.push(curr->left);
                    if (curr->right != NULL)
                        bfsQ.push(curr->right);
                }
            }

            ans.push_back(max_node);
        }

        return ans;
    }
};
```


