---
layout: post
title: "Self Crossing Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Geometry ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 335. You are given an array of integers distance.

---

<br />

## Description

LeetCode Problem 335.

You are given an array of integers distance.

You start at point (0,0) on an X-Y plane and you move distance[0] meters to the north, then distance[1] meters to the west, distance[2] meters to the south, distance[3] meters to the east, and so on. In other words, after each move, your direction changes counter-clockwise.

Return true if your path crosses itself, and false if it does not.

Example 1:
```
Input: distance = [2,1,1,2]
Output: true
```

Example 2:
```
Input: distance = [1,2,3,4]
Output: false
```

Example 3:
```
Input: distance = [1,1,1,1]
Output: true
```

Constraints:
* 1 <=distance.length <= 10^5
* 1 <=distance[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isSelfCrossing(vector<int>& x) {
        x.insert(x.begin(), 4, 0);

        int len = x.size();
        int i = 4;

        // outer spiral
        for (; i < len && x[i] > x[i - 2]; i++);

        if (i == len) return false;

        // check border
        if (x[i] >= x[i - 2] - x[i - 4]) {
            x[i - 1] -= x[i - 3];
        }

        // inner spiral
        for (i++; i < len && x[i] < x[i - 2]; i++);

        return i != len;
    }
};
```


