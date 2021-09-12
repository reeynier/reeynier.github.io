---
layout: post
title:  "Smallest Greater Multiple Made of Two Digits Problem"
categories: [ Data Structure ]
tags: [ DFS, Leetcode ]
similar: [ DFS ]
featured: false
hidden: false
excerpt: LeetCode 1999. Given three integers, k, digit1, and digit2, you want to find the smallest integer that is.
---

<br />

## Description

LeetCode Problem 1999. 

Given three integers, k, digit1, and digit2, you want to find the smallest integer that is:

* Larger than k,
* A multiple of k, and
* Comprised of only the digits digit1 and/or digit2.

Return the smallest such integer. If no such integer exists or the integer exceeds the limit of a signed 32-bit integer (231 - 1), return -1.

 

Example 1:
```
Input: k = 2, digit1 = 0, digit2 = 2
Output: 20
Explanation:
20 is the first integer larger than 2, a multiple of 2, and comprised of only the digits 0 and/or 2.
```

Example 2:
```
Input: k = 3, digit1 = 4, digit2 = 2
Output: 24
Explanation:
24 is the first integer larger than 3, a multiple of 3, and comprised of only the digits 4 and/or 2.
```

Example 3:
```
Input: k = 2, digit1 = 0, digit2 = 0
Output: -1
Explanation:
No integer meets the requirements so return -1.
```

Constraints:

* 1 <= k <= 1000
* 0 <= digit1 <= 9
* 0 <= digit2 <= 9

<br />

## Sample C++ Code

We build our number x recursivelly using digit d1 or d2. Note that we cannot use a digit if it's zero and x is zero.

Two cases:

* x gets too big. Return -1.
* x is greater than k and divisible by k. Return x.

If we get positive results for both digits, return the smallest one. For example, we can build 22 and 4 for k == 2 from digits 2 and 4. The result (smallest) is 4.


```c
int findInteger(int k, int d1, int d2, long long x = 0) {
    if (x > INT_MAX)
        return -1;        
    if (x > k && x % k == 0)
        return x;
    int x1 = (x + d1 == 0) ? -1 : findInteger(k, d1, d2, x * 10 + d1);
    int x2 = (x + d2 == 0) ? -1 : findInteger(k, d1, d2, x * 10 + d2);
    return x1 > 1 && x2 > 1 ? min(x1, x2) : max(x1, x2);
}
```
