---
layout: post
title: "Implement Rand10() Using Rand7() Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Rejection Sampling, Randomized, Probability and Statistics ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 470. Given the API rand7() that generates a uniform random integer in the range [1, 7], write a function rand10() that generates a uniform random integer in the range [1, 10]. You can only call the API rand7(), and you shouldn't call any other API. Please do not use a language's built-in random API.

---

<br />

## Description

LeetCode Problem 470.

Given the API rand7() that generates a uniform random integer in the range [1, 7], write a function rand10() that generates a uniform random integer in the range [1, 10]. You can only call the API rand7(), and you shouldn't call any other API. Please do not use a language's built-in random API.

Each test case will have one internal argument n, the number of times that your implemented function rand10() will be called while testing. Note that this is not an argument passed to rand10().

Example 1:
```
Input: n = 1
Output: [2]
```

Example 2:
```
Input: n = 2
Output: [2,8]
```

Example 3:
```
Input: n = 3
Output: [3,8,10]
```

Constraints:
* 1 <= n <= 10^5

<br />

## Sample C++ Code


```c
// The rand7() API is already defined for you.
// int rand7();
// @return a random integer in the range 1 to 7

class Solution {
public:
    int rand10() {
        int i,j;
        while ((i = rand7()) > 6);  // P(i is even) = P(i is odd) = 0.5
        while ((j = rand7()) > 5);  // P(j==1) = P(j==2) = P(j==3) = P(j==4) = P(j==5) = 0.2
        return (i&1) ? j : j+5;
    }
};
```


