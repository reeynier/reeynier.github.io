---
layout: post
title: "N-Ary Tree Preorder Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Stack, Tree, Depth-First Search ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 589. Given the root of an n-ary tree, return the preorder traversal of its nodes' values.

---

<br />

## Description

LeetCode Problem 589.

Given the root of an n-ary tree, return the preorder traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

Example 1: 
```
Input: root = [1,null,3,2,4,null,5,6]
Output: [1,3,5,6,2,4]
```

Example 2: 
```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [1,2,3,6,7,11,14,4,8,12,5,9,13,10]
```

Constraints:
* The number of nodes in the tree is in the range [0, 10^4].
* 0 <= Node.val <= 10^4
* The height of the n-ary tree is less than or equal to 1000.

<br />

## Sample C++ Code


```c
class Solution {
private:
    void travel(Node* root, vector<int>& result) {
        if (root == nullptr) {
            return;
        }
        
        result.push_back(root -> val);
        for (Node* child : root -> children) {
            travel(child, result);
        }
    }
public:
    vector<int> preorder(Node* root) {
        vector<int> result;
        travel(root, result);
        return result;
    }
};
```


