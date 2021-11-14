---
layout: post
title:  "Unique Binary Search Trees II Problem"
categories: [ Algorithm ]
tags: [ Dynamic Programming, Backtracking, Tree, Binary Search Tree, Binary Tree, Leetcode ]
similar: [ Binary Search Tree ]
featured: false
hidden: false
excerpt: LeetCode 95. Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.
---

<br />

## Description

LeetCode Problem 95. 

Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.

 

Example 1:
```
Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```

Example 2:
```
Input: n = 1
Output: [[1]]
```

Constraints:

* 1 <= n <= 8

<br />

## Sample C++ Code


```c
/* Given a tree which n nodes, it has the follwing form:
(0)root(n-1)
(1)root(n-2)
(2)root(n-3)
where (x) denotes the trees with x nodes.

Now take n=3 for example. Given n=3, we have [1 2 3] in which 
each of them can be used as the tree root.

when root=1: [1 # 2 # 3]; [1 # 3 2];
when root=2: [2 1 3];
when root=3: (similar with the situations when root=1.)

Thus, if we write a recursive function who generates a group of 
trees in which the numbers range from f to t, we have to generate 
the left trees and right trees of each tree in the vector. */
vector<TreeNode *> generateTree(int from, int to)
{
    vector<TreeNode *> ret;
    if(to - from < 0) ret.push_back(0);
    if(to - from == 0) ret.push_back(new TreeNode(from));
    if(to - from > 0)
    {
        for(int i=from; i<=to; i++)
        {
            vector<TreeNode *> l = generateTree(from, i-1);
            vector<TreeNode *> r = generateTree(i+1, to);

            for(int j=0; j<l.size(); j++)
            {
                for(int k=0; k<r.size(); k++)
                {
                    TreeNode * h = new TreeNode (i);
                    h->left = l[j];
                    h->right = r[k];
                    ret.push_back(h);
                }
            }
        }
    }
    return ret;
}

vector<TreeNode *> generateTrees(int n) {
    return generateTree(1, n);
}
```
