---
layout: post
title: "Beautiful Arrangement II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 667. Given two integers n and k, construct a list answer that contains n different positive integers ranging from 1 to n and obeys the following requirement

---

<br />

## Description

LeetCode Problem 667.

Given two integers n and k, construct a list answer that contains n different positive integers ranging from 1 to n and obeys the following requirement:

* Suppose this list is answer = [a_1, a_2, a_3, ... , a_n], then the list [\|a_1 - a_2\|, \|a_2 - a_3\|, \|a_3 - a_4\|, ... , \|a_n-1 - a_n\|] has exactly k distinct integers.

Return the list answer. If there multiple valid answers, return any of them.

Example 1:
```
Input: n = 3, k = 1
Output: [1,2,3]
Explanation: The [1,2,3] has three different positive integers ranging from 1 to 3, and the [1,1] has exactly 1 distinct integer: 1
```

Example 2:
```
Input: n = 3, k = 2
Output: [1,3,2]
Explanation: The [1,3,2] has three different positive integers ranging from 1 to 3, and the [2,1] has exactly 2 distinct integers: 1 and 2.
```

Constraints:
* 1 <= k < n <= 10^4

<br />

## Sample C++ Code

We can construct the array in the following way:

1, k+1, 2, k, 3, k-1, ...

The distance of this array is k, k-1, k-2, ..., 2, 1.

```c
class Solution {
public:
    vector<int> constructArray(int n, int k) {
        int l = 1, r = k + 1;
        vector<int> ans;
        while (l <= r) {
            ans.push_back(l++);
            if (l <= r) ans.push_back(r--);
        }
        for (int i = k + 2; i <= n; i++)
            ans.push_back(i);
        return ans;
    }
};
```


