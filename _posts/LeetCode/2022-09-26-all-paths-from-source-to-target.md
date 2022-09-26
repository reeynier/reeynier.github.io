---
layout: post
title: "All Paths From Source To Target Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Backtracking, Depth-First Search, Breadth-First Search, Graph ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 797. Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1 and return them in any order.

---

<br />

## Description

LeetCode Problem 797.

Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1 and return them in any order.

The graph is given as follows: graph[i] is a list of all nodes you can visit from node i (i.e., there is a directed edge from node i to node graph[i][j]).

Example 1: 
```
Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

Example 2: 
```
Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
```

Example 3:
```
Input: graph = [[1],[]]
Output: [[0,1]]
```

Example 4:
```
Input: graph = [[1,2,3],[2],[3],[]]
Output: [[0,1,2,3],[0,2,3],[0,3]]
```

Example 5:
```
Input: graph = [[1,3],[2],[3],[]]
Output: [[0,1,2,3],[0,3]]
```

Constraints:
* n == graph.length
* 2 <= n <= 15
* 0 <= graph[i][j] < n
* graph[i][j] != i (i.e., there will be no self-loops).
* All the elements of graph[i] are unique.
* The input graph is guaranteed to be a DAG.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> ans;
    int n;
    
    void dfs(vector<vector<int>>& graph, vector<int>& path) {
        int node = path.back();
        if (node == n-1)
            ans.push_back(path);
        
        for (int i = 0; i < graph[node].size(); i ++) {
            path.push_back(graph[node][i]);
            dfs(graph, path);
            path.pop_back();
        }
    }
    
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        n = graph.size();
        vector<int> path;
        path.push_back(0);
        
        dfs(graph, path);
        return ans;
    }
};
```


