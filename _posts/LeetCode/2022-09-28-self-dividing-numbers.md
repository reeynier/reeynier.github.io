---
layout: post
title: "Self Dividing Numbers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 728. A self-dividing number is a number that is divisible by every digit it contains.

---

<br />

## Description

LeetCode Problem 728.

A self-dividing number is a number that is divisible by every digit it contains.
* For example, 128 is a self-dividing number because 128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0.

A self-dividing number is not allowed to contain the digit zero.

Given two integers left and right, return a list of all the self-dividing numbers in the range [left, right].

Example 1:
```
Input: left = 1, right = 22
Output: [1,2,3,4,5,6,7,8,9,11,12,15,22]
```

Example 2:
```
Input: left = 47, right = 85
Output: [48,55,66,77]
```

Constraints:
* 1 <= left <= right <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool checkSelfDividing(int num) {
        bool isSelfDividing = true;
        int n = num, p;
        while (n > 0) {
            p = n % 10;
            if (p == 0) {
                isSelfDividing = false;
                break;
            }
            if (num % p != 0) {
                isSelfDividing = false;
                break;
            }
            n = n / 10;
        }
        return isSelfDividing;
    }
    
    vector<int> selfDividingNumbers(int left, int right) {
        vector<int> ans;
        for (int i = left; i <= right; i ++) {
            if (checkSelfDividing(i))
                ans.push_back(i);
        }
        return ans;
    }
};
```


