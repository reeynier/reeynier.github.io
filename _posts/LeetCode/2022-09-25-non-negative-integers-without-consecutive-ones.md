---
layout: post
title: "Non-Negative Integers Without Consecutive Ones Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 600. Given a positive integer n, return the number of the integers in the range [0, n] whose binary representations do not contain consecutive ones.

---

<br />

## Description

LeetCode Problem 600.

Given a positive integer n, return the number of the integers in the range [0, n] whose binary representations do not contain consecutive ones.

Example 1:
```
Input: n = 5
Output: 5
Explanation:
Here are the non-negative integers <= 5 with their corresponding binary representations:
0 : 0
1 : 1
2 : 10
3 : 11
4 : 100
5 : 101
Among them, only integer 3 disobeys the rule (two consecutive ones) and the other 5 satisfy the rule. 
```

Example 2:
```
Input: n = 1
Output: 2
```

Example 3:
```
Input: n = 2
Output: 3
```

Constraints:
* 1 <= n <= 10^9

<br />

## Sample C++ Code

The number of length k string without consecutive 1 is Fibonacci sequence f(k) = f(k-1) + f(k-2). 

For example, if k = 5, the range is 00000-11111. We can consider two ranges: 00000-01111 and 10000-10111. Any number >= 11000 is not allowed due to consecutive 1. The first case is actually f(4), and the second case is f(3), so f(5) = f(4) + f(3).

Then we can the number from left to right in binary format. If we find a '1' with k digits to the right, we count increases by f(k) because we can put a '0' at this digit and any valid length k string behind. After that, we continue the loop to consider the remaining cases, i.e., we put a '1' at this digit. If consecutive 1s are found, we exit the loop and return the answer. By the end of the loop, we return count+1 to include the number n itself.

For example, if n is 10010110, we find first '1' at 7 digits to the right, we add range 00000000-01111111, which is f(7). The second '1' at 4 digits to the right, add range 10000000-10001111, f(4). The third '1' at 2 digits to the right, add range 10010000-10010011, f(2). The fourth '1' at 1 digits to the right, add range 10010100-10010101, f(1). Those ranges are continuous from 00000000 to 10010101. And any greater number <= n will have consecutive 1.

```c
class Solution {
public:
    int findIntegers(int num) {
        int f[32];
        f[0] = 1;
        f[1] = 2;
        for (int i = 2; i < 32; ++i)
            f[i] = f[i-1] + f[i-2];
        int ans = 0, k = 30, pre_bit = 0;
        while (k >= 0) {
            if (num & (1 << k)) {
                ans += f[k];
                if (pre_bit) return ans;
                pre_bit = 1;
            }
            else
                pre_bit = 0;
            --k;
        }
        return ans + 1;
    }
};
```


