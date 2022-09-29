---
layout: post
title: "Redundant Connection Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Union Find ]
featured: false
hidden: false
excerpt: LeetCode 684. In this problem, a tree is an undirected graph that is connected and has no cycles.

---

<br />

## Description

LeetCode Problem 684.

In this problem, a tree is an undirected graph that is connected and has no cycles.

You are given a graph that started as a tree with n nodes labeled from 1 to n, with one additional edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed. The graph is represented as an array edges of length n where edges[i] = [a_i, b_i] indicates that there is an edge between nodes a_i and b_i in the graph.

Return an edge that can be removed so that the resulting graph is a tree of n nodes. If there are multiple answers, return the answer that occurs last in the input.

Example 1: 
```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```

Example 2: 
```
Input: edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]
Output: [1,4]
```

Constraints:
* n == edges.length
* 3 <= n <= 1000
* edges[i].length == 2
* 1 <= a_i < b_i <= edges.length
* a_i != b_i
* There are no repeated edges.
* The given graph is connected.

<br />

## Sample C++ Code using Union Find


```c
class Solution {
public:
    vector<int> nodes;

    int find(int p) {
        while (nodes[p] != p) {
            p = nodes[p];
        }
        return p;
    }
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        nodes.push_back(0);
        for (int i = 1; i <= n; i ++) {
            nodes.push_back(i);
        }
        
        int root1, root2;
        for (int i = 0; i < n; i ++) {
            root1 = find(edges[i][0]);
            root2 = find(edges[i][1]);
            
            if (root1 == root2)
                return edges[i];
            
            nodes[root2] = root1;
        }
        
        return edges.back();
    }
};
```


