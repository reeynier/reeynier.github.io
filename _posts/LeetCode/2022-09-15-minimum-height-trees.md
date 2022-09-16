---
layout: post
title: "Minimum Height Trees Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Graph, Topological Sort ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 310. A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

---

<br />

## Description

LeetCode Problem 310.

A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of n nodeslabelled from 0 to n - 1, and an array ofn - 1edges where edges[i] = [a_i, b_i] indicates that there is an undirected edge between the two nodesa_i andb_i in the tree,you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h)) are called minimum height trees (MHTs).

Return a list of all MHTs' root labels.You can return the answer in any order.

The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

Example 1:
```
Input: n = 4, edges = [[1,0],[1,2],[1,3]]
Output: [1]
Explanation: As shown, the height of the tree is 1 when the root is the node with label 1 which is the only MHT.
```

Example 2:
```
Input: n = 6, edges = [[3,0],[3,1],[3,2],[3,4],[5,4]]
Output: [3,4]
```

Example 3:
```
Input: n = 1, edges = []
Output: [0]
```

Example 4:
```
Input: n = 2, edges = [[0,1]]
Output: [0,1]
```

Constraints:
* 1 <= n <= 2 * 10^4
* edges.length == n - 1
* 0 <= a_i, b_i < n
* a_i != b_i
* All the pairs (a_i, b_i) are distinct.
* The given input is guaranteed to be a tree and there will be no repeated edges.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        //base case i.e only one node is available
        if (n == 1) return vector<int>{0};
        
        vector<vector<int>> graph(n);
        vector<int> degree(n,0);
        
        for (int i = 0; i < edges.size(); i++){
            int a = edges[i][0], b = edges[i][1];
            
            graph[a].push_back(b);
            graph[b].push_back(a);
            degree[a]++;
            degree[b]++;
        }

        queue<int> queue_degree_1;
        for (int i = 0; i < n; i++) 
        	if (degree[i] == 1) queue_degree_1.push(i);
        
        vector<int> res;
        
        //Run BFS until queue is empty
        while (!queue_degree_1.empty()) {
            int n = queue_degree_1.size();
            res.clear();
            
            //This is our level order traverse
            while (n--) {
                int node = queue_degree_1.front();
                queue_degree_1.pop();
                
                //add current node into the root node vector
                res.push_back(node);
                
                //Now it's time for neighbouring nodes
                for (int i = 0; i < graph[node].size(); i++) {
                    //decrease degree of neighbour nodes and push leaff nodes intp queue
                    degree[graph[node][i]]--;
                    if (degree[graph[node][i]] == 1) queue_degree_1.push(graph[node][i]);
                }
            }
        }
        
        return res;
    }
};
```


