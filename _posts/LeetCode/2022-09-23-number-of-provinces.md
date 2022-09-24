---
layout: post
title: "Number Of Provinces Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Union Find ]
featured: false
hidden: false
excerpt: LeetCode 547. There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

---

<br />

## Description

LeetCode Problem 547.

There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

A province is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the i^th city and the j^th city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of provinces.

Example 1: 
```
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2
```

Example 2: 
```
Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3
```

Constraints:
* 1 <= n <= 200
* n == isConnected.length
* n == isConnected[i].length
* isConnected[i][j] is 1 or 0.
* isConnected[i][i] == 1
* isConnected[i][j] == isConnected[j][i]

<br />

## Sample C++ Code using Union Find


```c
class Solution {
public:
    int _find(int p, vector<int>& num) {
        while (p != num[p])
            p = num[p];
        return p;
    }
    
    void _union(int i, int j, vector<int>& num) {
        int r1 = _find(i, num);
        int r2 = _find(j, num);
        num[r1] = r2;
    }
    
    int findCircleNum(vector<vector<int>>& M) {
        int n = M.size();
        
        vector<int> parent(n);
        for (int i = 0; i < n; i ++) 
            parent[i] = i;
        
        int r1, r2;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < n; j ++) {
                if (i == j) continue;
                if (M[i][j] == 0) continue;
                
                _union(i, j, parent);
            }
        }
        
        unordered_map<int, int> mp;
        for (int i = 0; i < n; i ++)
            mp[_find(i, parent)] = 1;
        
        return mp.size();
    }
};
```


