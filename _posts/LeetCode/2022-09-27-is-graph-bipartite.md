---
layout: post
title: "Is Graph Bipartite? Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 785. There is an undirected graph with n nodes, where each node is numbered between 0 and n - 1. You are given a 2D array graph, where graph[u] is an array of nodes that node u is adjacent to. More formally, for each v in graph[u], there is an undirected edge between node u and node v. 

---

<br />

## Description

LeetCode Problem 785.

There is an undirected graph with n nodes, where each node is numbered between 0 and n - 1. You are given a 2D array graph, where graph[u] is an array of nodes that node u is adjacent to. More formally, for each v in graph[u], there is an undirected edge between node u and node v. The graph has the following properties:
* There are no self-edges (graph[u] does not contain u).
* There are no parallel edges (graph[u] does not contain duplicate values).
* If v is in graph[u], then u is in graph[v] (the graph is undirected).
* The graph may not be connected, meaning there may be two nodes u and v such that there is no path between them.

A graph is bipartite if the nodes can be partitioned into two independent sets A and B such that every edge in the graph connects a node in set A and a node in set B.

Return true if and only if it is bipartite.

Example 1: 
```
Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
Output: false
Explanation: There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.
```

Example 2: 
```
Input: graph = [[1,3],[0,2],[1,3],[0,2]]
Output: true
Explanation: We can partition the nodes into two sets: {0, 2} and {1, 3}.
```

Constraints:
* graph.length == n
* 1 <= n <= 100
* 0 <= graph[u].length < n
* 0 <= graph[u][i] <= n - 1
* graph[u]does not containu.
* All the values of graph[u] are unique.
* If graph[u] contains v, then graph[v] contains u.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        int n = graph.size();
        vector<int> colors(n, 0);
        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (colors[i]) continue;
            colors[i] = 1;
            q.push(i);
            while (!q.empty()) {
                int temp = q.front();
                for (auto neighbor : graph[temp]) {
                    // Color neighbor with opposite color
                    if (!colors[neighbor]) {
                        colors[neighbor] = -colors[temp];
                        q.push(neighbor);
                    }
                    
                    // If the neighbor has the same color - can't bipartite.
                    else if (colors[neighbor] == colors[temp]) 
                        return false;
                }
                q.pop();
            }
        }
        return true;
    }
};
```


