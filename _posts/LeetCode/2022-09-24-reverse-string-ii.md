---
layout: post
title: "Reverse String II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 541. Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

---

<br />

## Description

LeetCode Problem 541.

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original.

Example 1:
```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

Example 2:
```
Input: s = "abcd", k = 2
Output: "bacd"
```

Constraints:
* 1 <= s.length <= 10^4
* s consists of only lowercase English letters.
* 1 <= k <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    string reverseStr(string s, int k) {
        for (int left = 0; left < s.size(); left += 2 * k) {
            for (int i = left, j = min(left + k - 1, (int)s.size() - 1); i < j; i++, j--) {
                swap(s[i], s[j]);
            }
        }
        return s;
    }
};
```


