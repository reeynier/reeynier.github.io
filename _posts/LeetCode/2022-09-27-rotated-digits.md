---
layout: post
title: "Rotated Digits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 788. An integer x is a good if after rotating each digit individually by 180 degrees, we get a valid number that is different from x. Each digit must be rotated - we cannot choose to leave it alone.

---

<br />

## Description

LeetCode Problem 788.

An integer x is a good if after rotating each digit individually by 180 degrees, we get a valid number that is different from x. Each digit must be rotated - we cannot choose to leave it alone.

A number is valid if each digit remains a digit after rotation. For example:
* 0, 1, and 8 rotate to themselves,
* 2 and 5 rotate to each other (in this case they are rotated in a different direction, in other words, 2 or 5 gets mirrored),
* 6 and 9 rotate to each other, and
* the rest of the numbers do not rotate to any other number and become invalid.

Given an integer n, return the number of good integers in the range [1, n].

Example 1:
```
Input: n = 10
Output: 4
Explanation: There are four good numbers in the range [1, 10] : 2, 5, 6, 9.
Note that 1 and 10 are not good numbers, since they remain unchanged after rotating.
```

Example 2:
```
Input: n = 1
Output: 0
```

Example 3:
```
Input: n = 2
Output: 1
```

Constraints:
* 1 <= n <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int rotatedDigits(int N) {
        int count = 0;
        int num, num_r;
        int rot[10] = {0, 1, 5, -1, -1, 2, 9, -1, 8, 6};
        
        for (int i = 0; i < 10; i ++) {
            for (int j = 0; j < 10; j ++) {
                for (int k = 0; k < 10; k ++) {
                    for (int l = 0; l < 10; l ++) {
                        num = 1000 * i + 100 * j + 10 * k + l;
                        if (num > N) {
                            return count;
                        }
                        if ((rot[i] == -1) || (rot[j] == -1) || (rot[k] == -1) || (rot[l] == -1)) {
                            continue;
                        }
                        num_r = 1000 * rot[i] + 100 * rot[j] + 10 * rot[k] + rot[l];
                        if (num != num_r)
                            count ++;
                    }
                }
            }
        }
        return count;
    }
};
```


