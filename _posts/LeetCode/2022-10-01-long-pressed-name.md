---
layout: post
title: "Long Pressed Name Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 925. Your friend is typing his name into a keyboard. Sometimes, when typing a character c, the key might get long pressed, and the character will be typed 1 or more times.

---

<br />

## Description

LeetCode Problem 925.

Your friend is typing his name into a keyboard. Sometimes, when typing a character c, the key might get long pressed, and the character will be typed 1 or more times.

You examine the typed characters of the keyboard. Return True if it is possible that it was your friends name, with some characters (possibly none) being long pressed.

Example 1:
```
Input: name = "alex", typed = "aaleex"
Output: true
Explanation: 'a' and 'e' in 'alex' were long pressed.
```

Example 2:
```
Input: name = "saeed", typed = "ssaaedd"
Output: false
Explanation: 'e' must have been pressed twice, but it wasn't in the typed output.
```

Example 3:
```
Input: name = "leelee", typed = "lleeelee"
Output: true
```

Example 4:
```
Input: name = "laiden", typed = "laiden"
Output: true
Explanation: It's not necessary to long press any character.
```

Constraints:
* 1 <= name.length <= 1000
* 1 <= typed.length <= 1000
* name and typed contain only lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isLongPressedName(string name, string typed) {
        int i =0; int j =0;
        while (i < name.size() || j < typed.size()) {
            char current = name[i];
            if (name[i] != typed[j]) 
                return false;
            i++;
            j++;
            if (name[i] != typed[j]) {
                while (current == typed[j]) j++;
            } 
        }
        return true;
    };
};
```


