---
layout: post
title: "Reachable Nodes In Subdivided Graph Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Graph, Heap, Shortest Path ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 882. You are given an undirected graph (the "original graph") with n nodes labeled from 0 to n - 1. You decide to subdivide each edge in the graph into a chain of nodes, with the number of new nodes varying between each edge.

---

<br />

## Description

LeetCode Problem 882.

You are given an undirected graph (the "original graph") with n nodes labeled from 0 to n - 1. You decide to subdivide each edge in the graph into a chain of nodes, with the number of new nodes varying between each edge.

The graph is given as a 2D array of edges where edges[i] = [u_i, v_i, cnt_i] indicates that there is an edge between nodes u_i and v_i in the original graph, and cnt_i is the total number of new nodes that you will subdivide the edge into. Note that cnt_i == 0 means you will not subdivide the edge.

To subdivide the edge [u_i, v_i], replace it with (cnt_i + 1) new edges and cnt_i new nodes. The new nodes are x_1, x_2, ..., x_cnt_i, and the new edges are [u_i, x_1], [x_1, x_2], [x_2, x_3], ..., [x_cnt_i-1, x_cnt_i], [x_cnt_i, v_i].

In this new graph, you want to know how many nodes are reachable from the node 0, where a node is reachable if the distance is maxMoves or less.

Given the original graph and maxMoves, return the number of nodes that are reachable from node 0 in the new graph.

Example 1: 
```
Input: edges = [[0,1,10],[0,2,1],[1,2,2]], maxMoves = 6, n = 3
Output: 13
Explanation: The edge subdivisions are shown in the image above.
The nodes that are reachable are highlighted in yellow.
```

Example 2:
```
Input: edges = [[0,1,4],[1,2,6],[0,2,8],[1,3,1]], maxMoves = 10, n = 4
Output: 23
```

Example 3:
```
Input: edges = [[1,2,4],[1,4,5],[1,3,1],[2,3,4],[3,4,5]], maxMoves = 17, n = 5
Output: 1
Explanation: Node 0 is disconnected from the rest of the graph, so only node 0 is reachable.
```

Constraints:
* 0 <= edges.length <= min(n * (n - 1) / 2, 10^4)
* edges[i].length == 3
* 0 <= u_i < v_i < n
* There are no multiple edges in the graph.
* 0 <= cnt_i <= 10^4
* 0 <= maxMoves <= 10^9
* 1 <= n <= 3000

<br />

## Sample C++ Code using Priority Queue


```c
class Solution {
public:
    int reachableNodes(vector<vector<int>>& edges, int M, int N) {
        vector<int> dist(N, INT_MAX);
        unordered_map<int, unordered_map<int, int>> g;

        for (auto& e:edges) 
            g[e[0]][e[1]] = g[e[1]][e[0]] = e[2] + 1;
        
        auto cmp = [](const pair<int, int>& a, const pair<int, int>& b) { 
            return a.second > b.second; 
        };
        
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> pq(cmp);
        pq.push({0,0});
        dist[0] = 0;
        
        while (!pq.empty()) {
            auto u = pq.top().first; 
            pq.pop();
            if (dist[u] >= M) 
                break;
            for (auto n_w : g[u]) {
                int v = n_w.first, w = n_w.second;
                if (dist[u] + w < dist[v]) {
                    dist[v] = w + dist[u];
                    pq.push({v, dist[v]});
                }
            }
        }
        
        int res = 0;
        for (int i = 0; i < N; i++) 
            if (dist[i] <= M) 
                res++;
        for (auto& e : edges) {
            int a = dist[e[0]] >= M ? 0 : min(M-dist[e[0]], e[2]);
            int b = dist[e[1]] >= M ? 0 : min(M-dist[e[1]], e[2]);
            res += min(a + b, e[2]);
        }
        
        return res;  
    }
};
```


