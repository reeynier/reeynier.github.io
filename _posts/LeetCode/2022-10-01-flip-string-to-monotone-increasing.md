---
layout: post
title: "Flip String To Monotone Increasing Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 926. A binary string is monotone increasing if it consists of some number of 0's (possibly none), followed by some number of 1's (also possibly none).

---

<br />

## Description

LeetCode Problem 926.

A binary string is monotone increasing if it consists of some number of 0's (possibly none), followed by some number of 1's (also possibly none).

You are given a binary string s. You can flip s[i] changing it from 0 to 1 or from 1 to 0.

Return the minimum number of flips to make s monotone increasing.

Example 1:
```
Input: s = "00110"
Output: 1
Explanation: We flip the last digit to get 00111.
```

Example 2:
```
Input: s = "010110"
Output: 2
Explanation: We flip to get 011111, or alternatively 000111.
```

Example 3:
```
Input: s = "00011000"
Output: 2
Explanation: We flip to get 00000000.
```

Constraints:
* 1 <= s.length <= 10^5
* s[i] is either '0' or '1'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minFlipsMonoIncr(const std::string& S, int counter_one  = 0, int counter_flip = 0) {
        for (auto ch : S) {
            // if c is 1, then it will not inpact the minFlips
            // if c is 0, then 2 options we can do to make it mono incr
            // 1. keep it as 0, and flip all the preceeding 1 to 0, 
            // need to know the count of ones so far
            // 2. flip it to 1, will not need to do anything
            if (ch == '1') {
                ++counter_one;
            } else {
                ++counter_flip;
            }
            counter_flip = std::min(counter_one, counter_flip);
        }
        return counter_flip;
    }
};
```


