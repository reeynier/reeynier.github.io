---
layout: post
title: "Sum Of Distances In Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Tree, Depth-First Search, Graph ]
similar: [ Depth-First Search  ]
featured: false
hidden: false
excerpt: LeetCode 834. There is an undirected connected tree with n nodes labeled from 0 to n - 1 and n - 1 edges.

---

<br />

## Description

LeetCode Problem 834.

There is an undirected connected tree with n nodes labeled from 0 to n - 1 and n - 1 edges.

You are given the integer n and the array edges where edges[i] = [a_i, b_i] indicates that there is an edge between nodes a_i and b_i in the tree.

Return an array answer of length n where answer[i] is the sum of the distances between the i^th node in the tree and all other nodes.

Example 1: 
```
Input: n = 6, edges = [[0,1],[0,2],[2,3],[2,4],[2,5]]
Output: [8,12,6,10,10,10]
Explanation: The tree is shown above.
We can see that dist(0,1) + dist(0,2) + dist(0,3) + dist(0,4) + dist(0,5)
equals 1 + 1 + 2 + 2 + 2 = 8.
Hence, answer[0] = 8, and so on.
```

Example 2: 
```
Input: n = 1, edges = []
Output: [0]
```

Example 3: 
```
Input: n = 2, edges = [[1,0]]
Output: [1,1]
```

Constraints:
* 1 <= n <= 3 * 10^4
* edges.length == n - 1
* edges[i].length == 2
* 0 <= a_i, b_i < n
* a_i != b_i
* The given input represents a valid tree.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<unordered_set<int>> tree;
    vector<int> v, count;
    // Counts the path to each node and sums them for every particular node
    void func1(int root, int x) {
        for (auto i: tree[root]) {
            if (i == x) continue;
            func1(i, root);
            count[root] += count[i];
            v[root] += v[i] + count[i];
        }
    }
    // Parent node count - count of closer nodes + count of farther nodes
    void func2(int root, int x) {
        for (auto i: tree[root]) {
            if (i == x) continue;
            count[root] += count[i];
            v[i] = v[root] - count[i] + count.size() - count[i];
            func2(i, root);
        }
    }
    vector<int> sumOfDistancesInTree(int n, vector<vector<int>>& a) {
        tree.resize(n);
        v.assign(n, 0);
        count.assign(n, 1);
        for (auto i: a) {
            tree[i[0]].insert(i[1]);
            tree[i[1]].insert(i[0]);
        }
        func1(0, -1);
        func2(0, -1);
        return v;
    }
};
```


