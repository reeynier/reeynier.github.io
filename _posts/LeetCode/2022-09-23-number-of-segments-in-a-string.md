---
layout: post
title: "Number Of Segments In A String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 434. You are given a string s, return the number of segments in the string.

---

<br />

## Description

LeetCode Problem 434.

You are given a string s, return the number of segments in the string.

A segment is defined to be a contiguous sequence of non-space characters.

Example 1:
```
Input: s = "Hello, my name is John"
Output: 5
Explanation: The five segments are ["Hello,", "my", "name", "is", "John"]
```

Example 2:
```
Input: s = "Hello"
Output: 1
```

Example 3:
```
Input: s = "love live! mu'sic forever"
Output: 4
```

Example 4:
```
Input: s = ""
Output: 0
```

Constraints:
* 0 <= s.length <= 300
* s consists of lower-case and upper-case English letters, digits or one of the following characters "!@#$%^&\*()_+-=',.:".
* The only space character in s is ' '.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int countSegments(string s) {
        int seg = 0;
        char lastc = ' ';
        for (char c : s) {
            if ((lastc == ' ') && (c != ' ')) {
                seg ++;
            }
            lastc = c;
        }
        return seg;
    }
};
```


