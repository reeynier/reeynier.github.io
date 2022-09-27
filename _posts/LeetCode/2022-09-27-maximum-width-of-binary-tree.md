---
layout: post
title: "Maximum Width Of Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Depth-First Search, Breadth-First Search, Binary Tree ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 662. Given the root of a binary tree, return the maximum width of the given tree.

---

<br />

## Description

LeetCode Problem 662.

Given the root of a binary tree, return the maximum width of the given tree.

The maximum width of a tree is the maximum width among all levels.

The width of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes are also counted into the length calculation.

It is guaranteed that the answer will in the range of 32-bit signed integer.

Example 1: 
```
Input: root = [1,3,2,5,3,null,9]
Output: 4
Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).
```

Example 2: 
```
Input: root = [1,3,null,5,3]
Output: 2
Explanation: The maximum width existing in the third level with the length 2 (5,3).
```

Example 3: 
```
Input: root = [1,3,2,5]
Output: 2
Explanation: The maximum width existing in the second level with the length 2 (3,2).
```

Example 4: 
```
Input: root = [1,3,2,5,null,null,9,6,null,null,7]
Output: 8
Explanation: The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```

Constraints:
* The number of nodes in the tree is in the range [1, 3000].
* -100 <= Node.val <= 100

<br />

## Sample C++ Code using Breadth-First Search 


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
    int widthOfBinaryTree(TreeNode* root) {
        if (!root)
            return 0;
        
        queue<pair<TreeNode*, unsigned long long int>> que;
        que.push({ root, 0 });
        int width = 0;
        
        while (que.size() != 0) {
            unsigned long long int left = que.front().second, right = 0;
            int size = que.size();
            
            while (size-- > 0) {
                pair<TreeNode*, unsigned long long int> rNode = que.front();
                que.pop();
                right = rNode.second;
                if (rNode.first->left) {
                    que.push({rNode.first->left, 2 * rNode.second + 1});
                }
                if (rNode.first->right) {
                    que.push({rNode.first->right, 2 * rNode.second + 2});
                }
            }
            
            width = max(width, int(right - left + 1));
        }
        
        return width;
    }
};
```


