---
layout: post
title: "Smallest Good Base Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 483. Given an integer n represented as a string, return the smallest good base of n.

---

<br />

## Description

LeetCode Problem 483.

Given an integer n represented as a string, return the smallest good base of n.

We call k >= 2 a good base of n, if all digits of n base k are 1's.

Example 1:
```
Input: n = "13"
Output: "3"
Explanation: 13 base 3 is 111.
```

Example 2:
```
Input: n = "4681"
Output: "8"
Explanation: 4681 base 8 is 11111.
```

Example 3:
```
Input: n = "1000000000000000000"
Output: "999999999999999999"
Explanation: 1000000000000000000 base 999999999999999999 is 11.
```

Constraints:
* n is an integer in the range [3, 10^18].
* n does not contain any leading zeros.

<br />

## Sample C++ Code using Binary Search 


```c
class Solution {
public:
	// For a given length d, we use binary search to check whether 
	// there is a base k which satisfies 1+k^1+k^2+...k^d=n. 
	// The left limit is 1, and the right limit is pow(n,1/d)+1, 
	// i.e., the d th square root of n.
	
    string smallestGoodBase(string n) {
        unsigned long long tn = (unsigned long long)stoll(n);
        unsigned long long x = 1;
        for (int i = 62; i >= 1; i--) {
            if ((x<<i) < tn) {
                unsigned long long cur = mysolve(tn, i);
                if (cur != 0) return to_string(cur);
            }
        }
        return to_string(tn - 1);
    }
    
    unsigned long long mysolve(unsigned long long n,int d) {
        double tn = (double) n;
        unsigned long long right = (unsigned long long)(pow(tn, 1.0/d) + 1);
        unsigned long long left = 1;
        while (left <= right){
            unsigned long long mid = left + (right - left) / 2;
            unsigned long long sum = 1,cur = 1;
            for (int i = 1; i <= d;i ++) {
                cur *= mid;
                sum += cur;
            }
            if (sum == n) return mid;
            if (sum > n) right = mid - 1;
            else left = mid + 1;
        }
        return 0;
    }

};
```


