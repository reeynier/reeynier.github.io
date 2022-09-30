---
layout: post
title: "Backspace String Compare Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String, Stack, Simulation ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 844. Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

---

<br />

## Description

LeetCode Problem 844.

Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

Example 1:
```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```

Example 2:
```
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```

Example 3:
```
Input: s = "a##c", t = "#a#c"
Output: true
Explanation: Both s and t become "c".
```

Example 4:
```
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```

Constraints:
* <span>1 <= s.length, t.length <= 200</span>
* <span>sand t only containlowercase letters and '#' characters.</span>

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        int i = S.size() - 1;
        int j = T.size() - 1;
        int skipS = 0, skipT = 0;
        
        while (i >= 0 || j >= 0) {
            while (i >= 0) {
                if (S[i] == '#') {
                    skipS ++; i --;
                } else if (skipS > 0) {
                    skipS --; i --;
                } else {
                    break;
                }
            }
            
            while (j >= 0) {
                if (T[j] == '#') {
                    skipT ++; j --;
                } else if (skipT > 0) {
                    skipT --; j --;
                } else {
                    break;
                }
            }
            
            if (i >= 0 && j >= 0 && S[i] != T[j])
                return false;
            if ((i >= 0) != (j >= 0))
                return false;
            
            i --;
            j --;
        }
        return true;
    }
};
```


