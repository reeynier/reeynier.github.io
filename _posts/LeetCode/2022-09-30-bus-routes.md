---
layout: post
title: "Bus Routes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 815. You are given an array routes representing bus routes where routes[i] is a bus route that the i^th bus repeats forever.

---

<br />

## Description

LeetCode Problem 815.

You are given an array routes representing bus routes where routes[i] is a bus route that the i^th bus repeats forever.

* For example, if routes[0] = [1, 5, 7], this means that the 0^th bus travels in the sequence 1 -> 5 -> 7 -> 1 -> 5 -> 7 -> 1 -> ... forever.

You will start at the bus stop source (You are not on any bus initially), and you want to go to the bus stop target. You can travel between bus stops by buses only.

Return the least number of buses you must take to travel from source to target. Return -1 if it is not possible.

Example 1:
```
Input: routes = [[1,2,7],[3,6,7]], source = 1, target = 6
Output: 2
Explanation: The best strategy is take the first bus to the bus stop 7, then take the second bus to the bus stop 6.
```

Example 2:
```
Input: routes = [[7,12],[4,5,15],[6],[15,19],[9,12,13]], source = 15, target = 12
Output: -1
```

Constraints:
* 1 <= routes.length <= 500.
* 1 <= routes[i].length <= 10^5
* All the values of routes[i] are unique.
* sum(routes[i].length) <= 10^5
* 0 <= routes[i][j] < 10^6
* 0 <= source, target < 10^6

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numBusesToDestination(vector<vector<int>>& routes, int S, int T) {
        unordered_map<int, vector<int>> to_routes;
        for (int i = 0; i < routes.size(); ++i)
            for (int j : routes[i])
                to_routes[j].push_back(i);
        queue<pair<int, int>> bfs;
        bfs.push({S, 0});
        unordered_set<int> seen = {S};
        while (!bfs.empty()) {
            int stop = bfs.front().first, bus = bfs.front().second;
            bfs.pop();
            if (stop == T)
                return bus;
            for (int i : to_routes[stop]) {
                for (int j : routes[i]) {
                    if (seen.find(j) == seen.end()) {
                        seen.insert(j);
                        bfs.push({j, bus + 1});
                    }
                }
                routes[i].clear();
            }
        }
        return -1;
    }
};
```


