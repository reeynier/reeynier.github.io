---
layout: post
title: "Reverse String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 344. Write a function that reverses a string. The input string is given as an array of characters s.

---

<br />

## Description

LeetCode Problem 344.

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

Example 2:
```
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

Constraints:
* 1 <= s.length <= 10^5
* s[i] is a printable ascii character.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string reverseString(string s) {
        int i = 0, j = s.size() - 1;
        while(i < j){
            swap(s[i++], s[j--]); 
        }
        return s;
    }
};
```


