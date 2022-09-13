---
layout: post
title: "Happy Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, Two Pointers ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 202. Write an algorithm to determine if a number n is happy.

---

<br />

## Description

LeetCode Problem 202.

Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:
* Starting with any positive integer, replace the number by the sum of the squares of its digits.
* Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
* Those numbers for which this process ends in 1 are happy.

Return true if n is a happy number, and false if not.

Example 1:
```
Input: n = 19
Output: true
Explanation:
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

Example 2:
```
Input: n = 2
Output: false
```

Constraints:
* 1 <= n <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isHappy(int n) {
        map<int, int> ht;
        int m;
        bool happy = false;
        while (1) {
            ht[n] = 1;
            m = 0;
            while (n > 0) {
                m += (n % 10) * (n % 10);
                n /= 10;
            }
            n = m;
            if (n == 1) {
                happy = true;
                break;
            }
            if (ht.find(n) != ht.end()) {
                happy = false;
                break;
            }
        }
        return happy;
    }
};
```


