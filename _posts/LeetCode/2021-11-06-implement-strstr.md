---
layout: post
title:  "Implement strStr() Problem"
categories: [ Data Structure ]
tags: [ String, Two Pointers, Leetcode ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 28. Implement strStr().
---

<br />

## Description

LeetCode Problem 28. 

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

 

Example 1:
```
Input: haystack = "hello", needle = "ll"
Output: 2
```

Example 2:
```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

Example 3:
```
Input: haystack = "", needle = ""
Output: 0
```

Constraints:

* 0 <= haystack.length, needle.length <= 5 * 10^4
* haystack and needle consist of only lower-case English characters.


<br />

## Sample C++ Code


```c
class Solution {
public:
    int strStr(string haystack, string needle) {
        int l1 = haystack.size(), l2 = needle.size();
        int i = 0, j = 0, k = 0;
        if (l2 == 0)
            return 0;
        if (l1 == 0)
            return -1;
        bool isSub = true;
        while (i < l1 - l2 + 1) {
            if (haystack[i] == needle[0]) {
                isSub = true;
                for (k = 0; k < l2; k ++) {
                    if (haystack[i + k] != needle[k]) {
                        isSub = false;
                        break;
                    }
                }
                if (isSub)
                    return i;
            } 
            i ++;
        }
        return -1;
    }
};
```
