---
layout: post
title: "Water And Jug Problem Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Depth-First Search, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 365. You are given two jugs with capacities jug1Capacity and jug2Capacity liters. There is an infinite amount of water supply available. Determine whether it is possible to measure exactly targetCapacity liters using these two jugs.

---

<br />

## Description

LeetCode Problem 365.

You are given two jugs with capacities jug1Capacity and jug2Capacity liters. There is an infinite amount of water supply available. Determine whether it is possible to measure exactly targetCapacity liters using these two jugs.

If targetCapacity liters of water are measurable, you must have targetCapacity liters of water contained within one or both buckets by the end.

Operations allowed:
* Fill any of the jugs with water.
* Empty any of the jugs.
* Pour water from one jug into another till the other jug is completely full, or the first jug itself is empty.

Example 1:
```
Input: jug1Capacity = 3, jug2Capacity = 5, targetCapacity = 4
Output: true
Explanation: The famous <a href="https://www.youtube.com/watch?v=BVtQNK_ZUJg&amp;ab_channel=notnek01" target="_blank">Die Hard</a> example 
```

Example 2:
```
Input: jug1Capacity = 2, jug2Capacity = 6, targetCapacity = 5
Output: false
```

Example 3:
```
Input: jug1Capacity = 1, jug2Capacity = 2, targetCapacity = 3
Output: true
```

Constraints:
* 1 <= jug1Capacity, jug2Capacity, targetCapacity <= 10^6

<br />

## Sample C++ Code using Breadth-First Search


```c
class Solution {
public:
    bool canMeasureWater(int jug1Capacity, int jug2Capacity, int targetCapacity) {
        
        int x = jug1Capacity, y = jug2Capacity, z = x + y;
        int steps[] = {x, -x, -y, y}; 
        
        queue<int> q;
        vector<int> vis(z + 1, 0); 
        q.push(0);
        vis[0] = 1;
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            
            if (node == targetCapacity) {
                return true; 
            }
            for (int i = 0; i < 4; i++) {
                int newNode = node + steps[i];
                if (newNode >= 0 && newNode <= z && vis[newNode] == 0) {
                    q.push(newNode);
                    vis[newNode] = 1;
                }
            }
        }
        return false; 
    }
};
```


