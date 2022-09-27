---
layout: post
title: "Kth Smallest Number In Multiplication Table Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 668. Nearly everyone has used the Multiplication Table. The multiplication table of size m x n is an integer matrix mat where mat[i][j] == i * j (1-indexed).

---

<br />

## Description

LeetCode Problem 668.

Nearly everyone has used the Multiplication Table. The multiplication table of size m x n is an integer matrix mat where mat[i][j] == i * j (1-indexed).

Given three integers m, n, and k, return the k^th smallest element in the m x n multiplication table.

Example 1: 
```
Input: m = 3, n = 3, k = 5
Output: 3
Explanation: The 5^th smallest number is 3.
```

Example 2: 
```
Input: m = 2, n = 3, k = 6
Output: 6
Explanation: The 6^th smallest number is 6.
```

Constraints:
* 1 <= m, n <= 3 * 10^4
* 1 <= k <= m * n

<br />

## Sample C++ Code using Binary Search 


```c
class Solution {
public:
    int findKthNumber(int m, int n, int k) {
        int left = 1, right = m * n;
        int mid;
        while (left < right) {
            mid = (left + right) / 2;
            int lessthanmid = 0;
            int i = m, j = 1;
            while (i >= 1 && j <= n) {
                if (i * j <= mid) {
                    lessthanmid += i;
                    j ++;
                } else {
                    i --;
                }
            }
            if (lessthanmid < k) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
};
```


