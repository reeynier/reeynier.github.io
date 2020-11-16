---
layout: post
title:  "Valid Perfect Square Problem"
categories: [ Algorithm, Leetcode ]
tags: [ Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
---

<br />

## Description

Given a positive integer **num**, write a function which returns True if **num** is a perfect square,  else False. Do not use any built-in library function such as sqrt.


Example: 
```
Input: num = 16
Output: true

Input: num = 14
Output: false
```

<br />

## Solution

This problem is similar to the [`Sqrt(x) Problem`]({% post_url 2020-11-15-sqrtx %}).

#### Binary Search Approach

A simple `brute force` approach is to enumerate all possible solutions from 1 to *num/2*, and check if there is an integer whose square equals *num*. If so, return true; otherwise, return false. The time complexity of this approach is O(n).


We can use `binary search` to speed up the search. We set two pointers *l* and *r*. The left pointer *l* starts from 0, and the right pointer *r* starts from *num*. During each iteration, we calculate *m* to be the average of *l* and *r* (*m = (l + r) / 2*). If *m * m* equals *num*, *num* is a perfect square. We can stop the search and return true. If *m * m* is larger than *x*, it means the right range *r* is too big. We can set *r* to be *m - 1* and keep on searching. If *m * m* is smaller than *num*, it means the left range *l* is too small. We can set *l* to be *m + 1* and keep on searching. We abort the search until *l* is greater than *r*.

When *l* is greater than *r*, it means we could not find an integer whose square is *num*. Thus, *num* is not a perfect square. We return false.

The time complexity of the binary search approach is O(logn), and the space complexity is O(1).

<br />

## Sample C++ Code

This is a C++ implementation of the binary search approach.

```c
#include <iostream>
#include <algorithm>

using namespace std;

bool isPerfectSquare(int num) {
    long long l, m, r;
    l = 0, r = num;
    while (l <= r) {
        m = (l + r) / 2;
        if (m*m == num)
            return true;
        if (m*m < num)
            l = m + 1;
        else
            r = m - 1;
    }
    return false;
}

int main() {
    cout << isPerfectSquare(45) << endl;
}
```
