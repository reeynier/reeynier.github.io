---
layout: post
title: "Redundant Connection II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 685. In this problem, a rooted tree is a directed graph such that, there is exactly one node (the root) for which all other nodes are descendants of this node, plus every node has exactly one parent, except for the root node which has no parents.

---

<br />

## Description

LeetCode Problem 685.

In this problem, a rooted tree is a directed graph such that, there is exactly one node (the root) for which all other nodes are descendants of this node, plus every node has exactly one parent, except for the root node which has no parents.

The given input is a directed graph that started as a rooted tree with n nodes (with distinct values from 1 to n), with one additional directed edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed.

The resulting graph is given as a 2D-array of edges. Each element of edges is a pair [u_i, v_i] that represents a directed edge connecting nodes u_i and v_i, where u_i is a parent of child v_i.

Return an edge that can be removed so that the resulting graph is a rooted tree of n nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array.

Example 1: 
```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```

Example 2: 
```
Input: edges = [[1,2],[2,3],[3,4],[4,1],[1,5]]
Output: [4,1]
```

Constraints:
* n == edges.length
* 3 <= n <= 1000
* edges[i].length == 2
* 1 <= u_i, v_i <= n
* u_i != v_i

<br />

## Sample C++ Code


```c
class Solution {
public:
    // 1) Check whether there is a node having two parents. 
    // If so, store them as candidates A and B, and set the second edge invalid. 
    // 2) Perform normal union find. 
    // If the tree is now valid, simply return candidate B
    // else if candidates not existing, we find a circle, return current edge; 
    // else, remove candidate A instead of B.  
    vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        vector<int> parent(n+1, 0), candA, candB;
        
        // step 1, check whether there is a node with two parents
        for (auto &edge:edges) {
            if (parent[edge[1]] == 0)
                parent[edge[1]] = edge[0]; 
            else {
                candA = {parent[edge[1]], edge[1]};
                candB = edge;
                edge[1] = 0;
            }
        } 
        
        // step 2, union find
        for (int i = 1; i <= n; i++) 
            parent[i] = i;
        
        for (auto &edge:edges) {
            if (edge[1] == 0) 
                continue;
            int u = edge[0], v = edge[1], pu = root(parent, u);
            // Now every node only has 1 parent, so root of v is implicitly v
            if (pu == v) {
                if (candA.empty()) 
                    return edge;
                return candA;
            }
            parent[v] = pu;
        }
        return candB;
    }
    
private:
    int root(vector<int>& parent, int k) {
        if (parent[k] != k) 
            parent[k] = root(parent, parent[k]);
        return parent[k];
    }
};
```


