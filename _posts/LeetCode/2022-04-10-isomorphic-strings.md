---
layout: post
title: "Isomorphic Strings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 205. Given two strings s and t, determine if they are isomorphic.

---

<br />

## Description

LeetCode Problem 205.

Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.
All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

Example 1:
```
Input: s = "egg", t = "add"
Output: true
```

Example 2:
```
Input: s = "foo", t = "bar"
Output: false
```

Example 3:
```
Input: s = "paper", t = "title"
Output: true
```

Constraints:
* 1 <= s.length <= 5 * 10^4
* t.length == s.length
* s and t consist of any valid ascii character.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        map<char, char> replaced;
        map<char, char> reverse_replaced;
        map<char, char>::iterator mit1, mit2;
        
        if (s.size() != t.size())
            return false;
        
        for (int i = 0; i < s.size(); i ++) {
            mit1 = replaced.find(s[i]);
            mit2 = reverse_replaced.find(t[i]);
            
            if ((mit1 == replaced.end()) && (mit2 == reverse_replaced.end())) {
                replaced.emplace(s[i], t[i]);
                reverse_replaced.emplace(t[i], s[i]);
                s[i] = t[i];
            } else if ((mit1 == replaced.end()) && (mit2 != reverse_replaced.end())) {
                return false;
            } else if ((mit1 != replaced.end()) && (mit2 == reverse_replaced.end())) {
                return false;
            } else {
                if ((t[i] != mit1->second) || (s[i] != mit2->second))
                    return false;
                s[i] = t[i];
            }

        }
        if (s != t)
            return false;
        else 
            return true;
    }
};
```


