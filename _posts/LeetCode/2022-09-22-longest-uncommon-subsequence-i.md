---
layout: post
title: "Longest Uncommon Subsequence I Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 521. Given two strings a and b, return the length of the longest uncommon subsequence between a and b. If the longest uncommon subsequence does not exist, return -1.

---

<br />

## Description

LeetCode Problem 521.

Given two strings a and b, return the length of the longest uncommon subsequence between a and b. If the longest uncommon subsequence does not exist, return -1.

An uncommon subsequence between two strings is a string that is a subsequence of one but not the other.

A subsequence of a string s is a string that can be obtained after deleting any number of characters from s.

* For example, "abc" is a subsequence of "aebdc" because you can delete the underlined characters in "aebdc" to get "abc". Other subsequences of "aebdc" include "aebdc", "aeb", and "" (empty string).

Example 1:
```
Input: a = "aba", b = "cdc"
Output: 3
Explanation: One longest uncommon subsequence is "aba" because "aba" is a subsequence of "aba" but not "cdc".
Note that "cdc" is also a longest uncommon subsequence.
```

Example 2:
```
Input: a = "aaa", b = "bbb"
Output: 3
Explanation:The longest uncommon subsequences are "aaa" and "bbb".
```

Example 3:
```
Input: a = "aaa", b = "aaa"
Output: -1
Explanation:Every subsequence of string a is also a subsequence of string b. Similarly, every subsequence of string b is also a subsequence of string a.
```

Constraints:
* 1 <= a.length, b.length <= 100
* a and b consist of lower-case English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findLUSlength(string a, string b) {
        if (a == b)
            // There is no subsequence in a that is not in b. return -1.
            return -1;
        else
            // If a.size() == b.size() but a != b, return the length of a and b.
            // If a.size() != b.size(), we can return the maximum length.
            return max(a.size(), b.size());
    }
};
```


