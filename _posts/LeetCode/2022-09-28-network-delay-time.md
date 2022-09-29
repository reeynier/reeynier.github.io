---
layout: post
title: "Network Delay Time Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Graph, Heap, Shortest Path ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 743. You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (u_i, v_i, w_i), where u_i is the source node, v_i is the target node, and w_i is the time it takes for a signal to travel from source to target.

---

<br />

## Description

LeetCode Problem 743.

You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (u_i, v_i, w_i), where u_i is the source node, v_i is the target node, and w_i is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

Example 1: 
```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```

Example 2:
```
Input: times = [[1,2,1]], n = 2, k = 1
Output: 1
```

Example 3:
```
Input: times = [[1,2,1]], n = 2, k = 2
Output: -1
```

Constraints:
* 1 <= k <= n <= 100
* 1 <= times.length <= 6000
* times[i].length == 3
* 1 <= u_i, v_i <= n
* u_i != v_i
* 0 <= w_i <= 100
* All the pairs (u_i, v_i) are unique. (i.e., no multiple edges.)

<br />

## Sample C++ Code using Breadth-First Search 


```c
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<pair<int,int>> adj[n+1];
        for (int i = 0; i < times.size(); i++)
            adj[times[i][0]].push_back({times[i][1], times[i][2]});
        
        vector<int> dist(n+1, INT_MAX);
        queue<int> q;
        q.push(k);
        dist[k] = 0;
        
        while (!q.empty()) {
            int t = q.front();
            q.pop();
            for (pair<int,int> it : adj[t]) {
                if (dist[it.first] > dist[t] + it.second) {
                    dist[it.first] = dist[t] + it.second;
                    q.push(it.first);
                }
            }
        }
        
        int res = 0;
        for (int i = 1; i <= n; i++) {
            if (dist[i] == INT_MAX)
                return -1;
            res = max(res, dist[i]);
        }
        return res;
    }
};
```


