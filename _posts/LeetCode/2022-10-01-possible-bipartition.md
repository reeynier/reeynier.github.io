---
layout: post
title: "Possible Bipartition Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Breadth-First Search, Union Find, Graph ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 886. We want to split a group of n people (labeled from 1 to n) into two groups of any size. Each person may dislike some other people, and they should not go into the same group.

---

<br />

## Description

LeetCode Problem 886.

We want to split a group of n people (labeled from 1 to n) into two groups of any size. Each person may dislike some other people, and they should not go into the same group.

Given the integer n and the array dislikes where dislikes[i] = [a_i, b_i] indicates that the person labeled a_i does not like the person labeled b_i, return true if it is possible to split everyone into two groups in this way.

Example 1:
```
Input: n = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4] and group2 [2,3].
```

Example 2:
```
Input: n = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```

Example 3:
```
Input: n = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```

Constraints:
* 1 <= n <= 2000
* 0 <= dislikes.length <= 10^4
* dislikes[i].length == 2
* 1 <= dislikes[i][j] <= n
* a_i < b_i
* All the pairs of dislikes are unique.

<br />

## Sample C++ Code using Breadth-First Search 


```c
class Solution {
public:
    bool possibleBipartition(int N, vector<vector<int>>& dislikes) {
        int m = dislikes.size();
        if (m == 0)
            return true;

        vector<vector<int>> edges(N+1, vector<int>());
        
        for (auto &x : dislikes) {
            edges[x[0]].push_back(x[1]);
            edges[x[1]].push_back(x[0]);
        }
        
        vector<int> color(N+1, -1);
        queue<int> q;
        int curr;
        for (int i = 1; i <= N; i ++) {
            if (color[i] == -1) {
                q.push(i);
                color[i] = 0;
                while (!q.empty()) {
                    curr = q.front();
                    q.pop();
                    for (auto j : edges[curr]) {
                        if (color[curr] == color[j])
                            return false;
                        if (color[j] == -1) {
                            color[j] = 1 - color[curr];
                            q.push(j);
                        }
                    }
                }
            }
        }
        return true;
    }
};
```


