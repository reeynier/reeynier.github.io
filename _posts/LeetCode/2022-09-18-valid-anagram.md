---
layout: post
title: "Valid Anagram Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 242. Given two strings s and t, return true if t is an anagram of s, and false otherwise.

---

<br />

## Description

LeetCode Problem 242.

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

Example 1:
```
Input: s = "anagram", t = "nagaram"
Output: true
```

Example 2:
```
Input: s = "rat", t = "car"
Output: false
```

Constraints:
* 1 <= s.length, t.length <= 5 * 10^4
* s and t consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isAnagram(string s, string t) {
        map<int, int> ht;
        for (int i = 0; i < s.size(); i ++) {
            if (ht.find(s[i]) == ht.end()) 
                ht[s[i]] = 0;
            ht[s[i]] ++;
        }
        for (int i = 0; i < t.size(); i ++) {
            if (ht.find(t[i]) == ht.end())
                ht[t[i]] = 0;
            ht[t[i]] --;
        }
        bool anagram = true;
        for (map<int, int>::iterator mit = ht.begin(); 
            mit != ht.end(); mit ++) {
            if (mit->second != 0) {
                anagram = false;
                break;
            }
        }
        return anagram;
    }
};
```


