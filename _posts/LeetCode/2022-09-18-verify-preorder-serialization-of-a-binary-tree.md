---
layout: post
title: "Verify Preorder Serialization Of A Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Stack, Tree, Binary Tree ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 331. One way to serialize a binary tree is to use preorder traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as '#'.

---

<br />

## Description

LeetCode Problem 331.

One way to serialize a binary tree is to use preorder traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as '#'. 

For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where '#' represents a null node.

Given a string of comma-separated values preorder, return true if it is a correct preorder traversal serialization of a binary tree.

It is guaranteed that each comma-separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid.
* For example, it could never contain two consecutive commas, such as "1,,3".

Note:You are not allowed to reconstruct the tree.

Example 1:
```
Input: preorder = "9,3,4,#,#,1,#,#,2,#,6,#,#"
Output: true
```

Example 2:
```
Input: preorder = "1,#"
Output: false
```

Example 3:
```
Input: preorder = "9,#,#,1"
Output: false
```

Constraints:
* 1 <= preorder.length <= 10^4
* preorder consist of integers in the range [0, 100] and '#' separated by commas ','.

<br />

## Sample C++ Code

We use nodes to count the nodes we are allowed to have next. Every time we get a new node we decrease nodes, if we got below zero it's false. If we get a non-null node, we can have after it two more nodes. At the end, we are supposed to end up with nodes == 0, otherwise the tree is not good.

```c
class Solution {
public:
    bool isValidSerialization(string preorder) {
        stringstream ss(preorder);
        string curr;
        int nodes = 1;
        while (getline(ss, curr, ',')) {
            nodes--;
            if (nodes < 0) return false;
            if (curr != "#") nodes += 2;
        }
        return nodes == 0;
    }
};
```


