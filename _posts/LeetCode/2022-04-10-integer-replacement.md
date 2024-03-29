---
layout: post
title: "Integer Replacement Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Greedy, Bit Manipulation, Memoization ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 397. Given a positive integer n,you can apply one of the following operations.
---

<br />

## Description

LeetCode Problem 397.

Given a positive integer n,you can apply one of the following operations:
* If n is even, replace n with n / 2.
* If n is odd, replace n with either n + 1 or n - 1.

Return the minimum number of operations needed for n to become 1.

Example 1:
```
Input: n = 8
Output: 3
Explanation: 8 -> 4 -> 2 -> 1
```

Example 2:
```
Input: n = 7
Output: 4
Explanation: 7 -> 8 -> 4 -> 2 -> 1
or 7 -> 6 -> 3 -> 2 -> 1
```

Example 3:
```
Input: n = 4
Output: 2
```

Constraints:
* 1 <= n <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
private:
    unordered_map<int, int> visited;

public:
    int integerReplacement(int n) {        
        if (n == 1) { return 0; }
        if (visited.count(n) == 0) {
            if (n & 1 == 1) {
                visited[n] = 2 + min(integerReplacement(n / 2), integerReplacement(n / 2 + 1));
            } else {
                visited[n] = 1 + integerReplacement(n / 2);
            }
        }
        return visited[n];
    }
};
```


