---
layout: post
title: "Add To Array-Form Of Integer Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 989. The array-form of an integer num is an array representing its digits in left to right order.

---

<br />

## Description

LeetCode Problem 989.

The array-form of an integer num is an array representing its digits in left to right order.
* For example, for num = 1321, the array form is [1,3,2,1].

Given num, the array-form of an integer, and an integer k, return the array-form of the integer num + k.

Example 1:
```
Input: num = [1,2,0,0], k = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234
```

Example 2:
```
Input: num = [2,7,4], k = 181
Output: [4,5,5]
Explanation: 274 + 181 = 455
```

Example 3:
```
Input: num = [2,1,5], k = 806
Output: [1,0,2,1]
Explanation: 215 + 806 = 1021
```

Example 4:
```
Input: num = [9,9,9,9,9,9,9,9,9,9], k = 1
Output: [1,0,0,0,0,0,0,0,0,0,0]
Explanation: 9999999999 + 1 = 10000000000
```

Constraints:
* 1 <= num.length <= 10^4
* 0 <= num[i] <= 9
* numdoes not contain any leading zeros except for the zero itself.
* 1 <= k <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> addToArrayForm(vector<int> A, int K) {
        for (int i = A.size() - 1; i >= 0 && K > 0; i--) {
            A[i] += K;
            K = A[i] / 10;
            A[i] %= 10;
        }
        while (K > 0) {
            A.insert(A.begin(), K % 10);
            K /= 10;
        }
        return A;
    }
};
```


