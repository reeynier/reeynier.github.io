---
layout: post
title: "Arranging Coins Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 441. You have n coins and you want to build a staircase with these coins. The staircase consists of k rows where the i^th row has exactly i coins. The last row of the staircase may be incomplete.

---

<br />

## Description

LeetCode Problem 441.

You have n coins and you want to build a staircase with these coins. The staircase consists of k rows where the i^th row has exactly i coins. The last row of the staircase may be incomplete.

Given the integer n, return the number of complete rows of the staircase you will build.

Example 1: 
```
Input: n = 5
Output: 2
Explanation: Because the 3^rd row is incomplete, we return 2.
```

Example 2: 
```
Input: n = 8
Output: 3
Explanation: Because the 4^th row is incomplete, we return 3.
```

Constraints:
* 1 <= n <= 2^31 - 1

<br />

## Sample C++ Code using Binary Search 


```c
class Solution {
public:
    int arrangeCoins(int n) {
        int l = 1, r = n, ans;
		long rows, coinsNeeded;
        while (l <= r) {
            rows = l + ((r-l) >> 1);                            // finding mid of range [l, r]
            coinsNeeded = (rows * (rows + 1)) >> 1;             // coins needed for 'rows' number of row
            if (coinsNeeded <= n) 
            	l = rows + 1, ans = rows;                       // if available coins are sufficient
            else r = rows - 1;                                  // coins insufficient, eliminate the half greater than rows
        }
        return ans;
    }
};
```


