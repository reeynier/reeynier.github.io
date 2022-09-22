---
layout: post
title: "Find Mode In Binary Search Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Binary Search Tree, Binary Tree ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 501. Given the root of a binary search tree (BST) with duplicates, return all the mode(s) (i.e., the most frequently occurred element) in it.

---

<br />

## Description

LeetCode Problem 501.

Given the root of a binary search tree (BST) with duplicates, return all the mode(s) (i.e., the most frequently occurred element) in it.

If the tree has more than one mode, return them in any order.

Assume a BST is defined as follows:
* The left subtree of a node contains only nodes with keys less than or equal to the node's key.
* The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
* Both the left and right subtrees must also be binary search trees.

Example 1: 
```
Input: root = [1,null,2,2]
Output: [2]
```

Example 2:
```
Input: root = [0]
Output: [0]
```

Constraints:
* The number of nodes in the tree is in the range [1, 10^4].
* -10^5 <= Node.val <= 10^5

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
    vector<int> findMode(TreeNode* root) {
        unordered_map<int, int> map;
        vector<int> result;

        int modeCount = getModeCount(root, map);
        
        for(pair<int,int> p : map) {
            if(p.second == modeCount) {
                result.push_back(p.first);
            }
        }
        
        return result;
    }
    
    /**
     * Traverse the tree using depth first search.
     * Return the mode count (i.e. The count of a repeated number that occurs the most.) of the tree.
     */
    int getModeCount(TreeNode* root, unordered_map<int, int> &map) {
        if(root == NULL)
            return 0;
        
        if(map.find(root->val) == map.end()) {
            map.insert(pair<int, int>(root->val, 1));
        }
        else {
            map[root->val]++;
        }
        
        return max(map[root->val], max(getModeCount(root->left, map), getModeCount(root->right, map)));
    }
};
```


