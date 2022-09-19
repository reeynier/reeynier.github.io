---
layout: post
title: "Reverse Vowels Of A String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 345. Given a string s, reverse only all the vowels in the string and return it.

---

<br />

## Description

LeetCode Problem 345.

Given a string s, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both cases.

Example 1:
```
Input: s = "hello"
Output: "holle"
```

Example 2:
```
Input: s = "leetcode"
Output: "leotcede"
```

Constraints:
* 1 <= s.length <= 3 * 10^5
* s consist of printable ASCII characters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isVowel(char c) {
        return (c == 'a') || (c == 'e') || (c == 'i') || (c == 'o') ||
            (c == 'u') || (c == 'A') || (c == 'E') || (c == 'I') ||
            (c == 'O') || (c == 'U');
    }
    string reverseVowels(string s) {
        int i = 0, j = s.size() - 1;
        char c;
        while (i <= j) {
            if ((isVowel(s[i])) && (isVowel(s[j]))) {
               c = s[i];
                s[i] = s[j];
                s[j] = c;
                i ++;
                j --;
            } else {
                if (!isVowel(s[i])) {
                    i ++;
                }
                if (!isVowel(s[j])) {
                    j --;
                }
            }
        }
        return s;
    }
};
```


