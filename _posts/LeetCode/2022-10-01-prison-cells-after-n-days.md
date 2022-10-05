---
layout: post
title: "Prison Cells After N Days Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Math, Bit Manipulation ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 957. There are 8 prison cells in a row and each cell is either occupied or vacant.

---

<br />

## Description

LeetCode Problem 957.

There are 8 prison cells in a row and each cell is either occupied or vacant.

Each day, whether the cell is occupied or vacant changes according to the following rules:
* If a cell has two adjacent neighbors that are both occupied or both vacant, then the cell becomes occupied.
* Otherwise, it becomes vacant.

Note that because the prison is a row, the first and the last cells in the row can't have two adjacent neighbors.

You are given an integer array cells where cells[i] == 1 if the i^th cell is occupied and cells[i] == 0 if the i^th cell is vacant, and you are given an integer n.

Return the state of the prison after n days (i.e., n such changes described above).

Example 1:
```
Input: cells = [0,1,0,1,1,0,0,1], n = 7
Output: [0,0,1,1,0,0,0,0]
Explanation: The following table summarizes the state of the prison on each day:
Day 0: [0, 1, 0, 1, 1, 0, 0, 1]
Day 1: [0, 1, 1, 0, 0, 0, 0, 0]
Day 2: [0, 0, 0, 0, 1, 1, 1, 0]
Day 3: [0, 1, 1, 0, 0, 1, 0, 0]
Day 4: [0, 0, 0, 0, 0, 1, 0, 0]
Day 5: [0, 1, 1, 1, 0, 1, 0, 0]
Day 6: [0, 0, 1, 0, 1, 1, 0, 0]
Day 7: [0, 0, 1, 1, 0, 0, 0, 0]
```

Example 2:
```
Input: cells = [1,0,0,1,0,0,1,0], n = 1000000000
Output: [0,0,1,1,1,1,1,0]
```

Constraints:
* cells.length == 8
* cells[i]is either 0 or 1.
* 1 <= n <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:    
    vector<int> prisonAfterNDays(vector<int>& cells, int N) {
        int n = cells.size(), cycle = 0;
        vector<int> cur(n, 0), direct;
        while (N-- > 0) {
            for (int i = 1; i < n - 1; ++i) 
                cur[i] = cells[i - 1] == cells[i + 1];
            if (direct.empty()) 
                direct = cur;
            else if (direct == cur) 
                N %= cycle;

            ++cycle;
            cells = cur;
        }
        return cur;
    }
};
```


