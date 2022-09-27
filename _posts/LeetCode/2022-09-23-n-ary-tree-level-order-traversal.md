---
layout: post
title: "N-Ary Tree Level Order Traversal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Tree, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 429. Given an n-ary tree, return the level order traversal of its nodes' values.

---

<br />

## Description

LeetCode Problem 429.

Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

Example 1: 
```
Input: root = [1,null,3,2,4,null,5,6]
Output: [[1],[3,2,4],[5,6]]
```

Example 2: 
```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

Constraints:
* The height of the n-ary tree is less than or equal to 1000
* The total number of nodes is between [0, 10^4]

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
    vector<vector<int>> levelOrder(Node* root) {
        if (root == nullptr) return {};
        
        queue<Node*> q;
        q.push(root);
        vector<vector<int>> ans;
        
        while (!q.empty()) {
            ans.emplace_back();
            for (int i = q.size(); i >= 1; i--) {
                Node* curr = q.front(); q.pop();
                ans.back().push_back(curr->val);
                for (Node* child : curr->children) {
                    q.push(child);
                }
            }
        }
        
        return ans;
    }
};
```

