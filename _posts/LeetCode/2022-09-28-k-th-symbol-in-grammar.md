---
layout: post
title: "K-Th Symbol In Grammar Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Bit Manipulation, Recursion ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 779. We build a table of n rows (1-indexed). We start by writing 0 in the 1^st row. Now in every subsequent row, we look at the previous row and replace each occurrence of 0 with 01, and each occurrence of 1 with 10.

---

<br />

## Description

LeetCode Problem 779.

We build a table of n rows (1-indexed). We start by writing 0 in the 1^st row. Now in every subsequent row, we look at the previous row and replace each occurrence of 0 with 01, and each occurrence of 1 with 10.

* For example, for n = 3, the 1^st row is 0, the 2^nd row is 01, and the 3^rd row is 0110.

Given two integer n and k, return the k^th (1-indexed) symbol in the n^th row of a table of n rows.

Example 1:
```
Input: n = 1, k = 1
Output: 0
Explanation: row 1: 0
```

Example 2:
```
Input: n = 2, k = 1
Output: 0
Explanation:
row 1: 0
row 2: 01
```

Example 3:
```
Input: n = 2, k = 2
Output: 1
Explanation:
row 1: 0
row 2: 01
```

Example 4:
```
Input: n = 3, k = 1
Output: 0
Explanation:
row 1: 0
row 2: 01
row 3: 0110
```

Constraints:
* 1 <= n <= 30
* 1 <= k <= 2^n - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    int kthGrammar(int N, int K) {
        if (K == 1)
            return 0;
        if (K % 2 == 1)
            return (kthGrammar(N, K/2+1) == 0) ? 0 : 1;
        else
            return (kthGrammar(N, K/2) == 0) ? 1 : 0;
    }
};
```


