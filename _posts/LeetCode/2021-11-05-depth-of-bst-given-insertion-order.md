---
layout: post
title:  "Depth of BST Given Insertion Order Problem"
categories: [ Data Structure ]
tags: [ BST, Leetcode ]
similar: [ BST ]
featured: false
hidden: false
excerpt: LeetCode 1902. You are given a 0-indexed integer array order of length n, a permutation of integers from 1 to n representing the order of insertion into a binary search tree.
---

<br />

## Description

LeetCode Problem 1902. 

You are given a 0-indexed integer array order of length n, a permutation of integers from 1 to n representing the order of insertion into a binary search tree.

A binary search tree is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

The binary search tree is constructed as follows: order[0] will be the root of the binary search tree.
All subsequent elements are inserted as the child of any existing node such that the binary search tree properties hold.

Return the depth of the binary search tree.

A binary tree's depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

 

Example 1:
```
Input: order = [2,1,4,3]
Output: 3
Explanation: The binary search tree has a depth of 3 with path 2->3->4.
```

Example 2:
```
Input: order = [2,1,3,4]
Output: 3
Explanation: The binary search tree has a depth of 3 with path 2->3->4.
```

Example 3:
```
Input: order = [1,2,3,4]
Output: 4
Explanation: The binary search tree has a depth of 4 with path 1->2->3->4.
``` 

Constraints:

* n == order.length
* 1 <= n <= 10^5
* order is a permutation of integers between 1 and n.

<br />

## Sample C++ Code



```c
int maxDepthBST(vector<int>& order) {
    map<int, int> m{ {0, 0}, {100001, 0} };
    for (int i : order) {
        auto it = m.upper_bound(i);
        m[i] = 1 + max(it->second, prev(it)->second);
    }
    return max_element(begin(m), end(m), [](const auto& a, const auto &b){ return a.second < b.second; })->second;
}
```