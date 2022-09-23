---
layout: post
title: "N-Ary Tree Postorder Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Stack, Tree, Depth-First Search ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 590. Given the root of an n-ary tree, return the postorder traversal of its nodes' values.

---

<br />

## Description

LeetCode Problem 590.

Given the root of an n-ary tree, return the postorder traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

Example 1: 
```
Input: root = [1,null,3,2,4,null,5,6]
Output: [5,6,3,2,4,1]
```

Example 2: 
```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [2,6,14,11,7,3,12,8,4,13,9,10,5,1]
```

Constraints:
* The number of nodes in the tree is in the range [0, 10^4].
* 0 <= Node.val <= 10^4
* The height of the n-ary tree is less than or equal to 1000.

<br />

## Sample C++ Code


```c
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<int> postorder(Node* root) {
        vector<int> post;
        vector<int> child;
        if (root == NULL)
            return post;
        for (int i = 0; i < root->children.size(); i ++) {
            child = postorder(root->children[i]);
            post.insert(post.end(), child.begin(), child.end());
        }
        post.push_back(root->val);
        return post;
    }
};
```


