---
layout: post
title:  "Length Of Last Word Problem"
categories: [ Data Structure ]
tags: [ String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 58. Given a string s consisting of some words separated by some number of spaces, return the length of the last word in the string. 
---

<br />

## Description

LeetCode Problem 58. 

Given a string s consisting of some words separated by some number of spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

 

Example 1:
```
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

Example 2:
```
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```

Example 3:
```
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

Constraints:

* 1 <= s.length <= 10^4
* s consists of only English letters and spaces ' '.
* There will be at least one word in s.


<br />

## Sample C++ Code


```c
class Solution {
public:
    /* Start from the tail of s and move backwards to find the first non-space character. 
    Then from this character, move backwards and count the number of non-space characters 
    until we pass over the head of s or meet a space character. The count will then be the 
    length of the last word. */
    int lengthOfLastWord(string s) { 
        int len = 0, tail = s.length() - 1;
        while (tail >= 0 && s[tail] == ' ') tail--;
        while (tail >= 0 && s[tail] != ' ') {
            len++;
            tail--;
        }
        return len;
    }
};
```
