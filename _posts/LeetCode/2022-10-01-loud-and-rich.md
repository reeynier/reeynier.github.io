---
layout: post
title: "Loud And Rich Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Depth-First Search, Graph, Topological Sort ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 851. There is a group of n people labeled from 0 to n - 1 where each person has a different amount of money and a different level of quietness.

---

<br />

## Description

LeetCode Problem 851.

There is a group of n people labeled from 0 to n - 1 where each person has a different amount of money and a different level of quietness.

You are given an array richer where richer[i] = [a_i, b_i] indicates that a_i has more money than b_i and an integer array quiet where quiet[i] is the quietness of the i^th person. All the given data in richer are logically correct (i.e., the data will not lead you to a situation where x is richer than y and y is richer than x at the same time).

Return an integer array answer where answer[x] = y if y is the least quiet person (that is, the person y with the smallest value of quiet[y]) among all people who definitely have equal to or more money than the person x.

Example 1:
```
Input: richer = [[1,0],[2,1],[3,1],[3,7],[4,3],[5,3],[6,3]], quiet = [3,2,5,4,6,1,7,0]
Output: [5,5,2,5,4,5,6,7]
Explanation: 
answer[0] = 5.
Person 5 has more money than 3, which has more money than 1, which has more money than 0.
The only person who is quieter (has lower quiet[x]) is person 7, but it is not clear if they have more money than person 0.
answer[7] = 7.
Among all people that definitely have equal to or more money than person 7 (which could be persons 3, 4, 5, 6, or 7), the person who is the quietest (has lower quiet[x]) is person 7.
The other answers can be filled out with similar reasoning.
```

Example 2:
```
Input: richer = [], quiet = [0]
Output: [0]
```

Constraints:
* n == quiet.length
* 1 <= n <= 500
* 0 <= quiet[i] < n
* All the values of quiet are unique.
* 0 <= richer.length <= n * (n - 1) / 2
* 0 <= a_i, b_i < n
* a_i != b_i
* All the pairs of richer are unique.
* The observations in richer are all logically consistent.

<br />

## Sample C++ Code using Breadth-First Search 


```c
class Solution {
public:
    vector<int> loudAndRich(vector<vector<int>>& richer, vector<int>& quiet) {
        int n = quiet.size();
        
        vector<vector<int>> adj(n);
        vector<int> indegree(n, 0);
        for (auto& rich : richer) {
            adj[rich[0]].push_back(rich[1]);
            indegree[rich[1]] ++;
        }
        
        queue<int> q;
        vector<int> answer(n);
        
        for (int i = 0; i < n; i++) {
            answer[i] = i;
            if (indegree[i] == 0) 
                q.push(i);
        }
        
        while (q.size()) {
            int node = q.front(); 
            q.pop();
            
            for (auto& adjNode : adj[node]) {
                if (quiet[answer[adjNode]] > quiet[answer[node]]) {
                    answer[adjNode] = answer[node];
                }
                
                indegree[adjNode] --;
                if (indegree[adjNode] == 0) 
                    q.push(adjNode);
            }
        }
        return answer;
    }
};
```


