---
layout: post
title: "Most Frequent Subtree Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Tree, Depth-First Search, Binary Search ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 508. Given the root of a binary tree, return the most frequent subtree sum. If there is a tie, return all the values with the highest frequency in any order.

---

<br />

## Description

LeetCode Problem 508.

Given the root of a binary tree, return the most frequent subtree sum. If there is a tie, return all the values with the highest frequency in any order.

The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself).

Example 1: 
```
Input: root = [5,2,-3]
Output: [2,-3,4]
```

Example 2: 
```
Input: root = [5,2,-5]
Output: [2]
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
    vector<int> findFrequentTreeSum(TreeNode* root) {
        unordered_map<int,int> counts;
        int maxCount = 0;
        countSubtreeSums(root, counts, maxCount); 
        
        vector<int> maxSums;
        for(const auto& x :  counts){
            if(x.second == maxCount) maxSums.push_back(x.first);
        }
        return maxSums;
    }
    
    int countSubtreeSums(TreeNode *r, unordered_map<int,int> &counts, int& maxCount){
        if(r == nullptr) return 0;
        int sum = r->val;
        sum += countSubtreeSums(r->left, counts, maxCount);
        sum += countSubtreeSums(r->right, counts, maxCount);
        ++counts[sum];
        maxCount = max(maxCount, counts[sum]);
        return sum;
    }
};
```


