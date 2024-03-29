---
layout: post
title: "Leaf-Similar Trees Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 872. Consider all the leaves of a binary tree, fromleft to right order, the values of thoseleaves form a leaf value sequence.

---

<br />

## Description

LeetCode Problem 872.

Consider all the leaves of a binary tree, fromleft to right order, the values of thoseleaves form a leaf value sequence. 

For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similarif their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

Example 1: 
```
Input: root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
Output: true
```

Example 2:
```
Input: root1 = [1], root2 = [1]
Output: true
```

Example 3:
```
Input: root1 = [1], root2 = [2]
Output: false
```

Example 4:
```
Input: root1 = [1,2], root2 = [2,2]
Output: true
```

Example 5: 
```
Input: root1 = [1,2,3], root2 = [1,3,2]
Output: false
```

Constraints:
* The number of nodes in each tree will be in the range [1, 200].
* Both of the given trees will have values in the range [0, 200].

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
    void dfs(TreeNode* root, vector<int> &leafs) {
        if ((root->left == NULL) && (root->right == NULL))
            leafs.push_back(root->val);
        
        if (root->left != NULL)
            dfs(root->left, leafs);
        
        if (root->right != NULL)
            dfs(root->right, leafs);
            
    }
    
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int> leafs1;
        vector<int> leafs2;
        
        if (root1 != NULL)
            dfs(root1, leafs1);
        
        if (root2 != NULL)
            dfs(root2, leafs2);
        
        return (leafs1 == leafs2);
    }
};
```


