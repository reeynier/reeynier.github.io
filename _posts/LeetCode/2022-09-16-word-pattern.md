---
layout: post
title: "Word Pattern Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 290. Given a pattern and a string s, find if sfollows the same pattern.

---

<br />

## Description

LeetCode Problem 290.

Given a pattern and a string s, find if sfollows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

Example 1:
```
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```

Example 2:
```
Input: pattern = "abba", s = "dog cat cat fish"
Output: false
```

Example 3:
```
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false
```

Example 4:
```
Input: pattern = "abba", s = "dog dog dog dog"
Output: false
```

Constraints:
* 1 <= pattern.length <= 300
* pattern contains only lower-case English letters.
* 1 <= s.length <= 3000
* s contains only lower-case English letters and spaces ' '.
* s does not contain any leading or trailing spaces.
* All the words in s are separated by a single space.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool wordPattern(string pattern, string str) {
        int i = 0, j = 0;
        map<char, string> ht;
        map<string, char> ht2;
        bool match = true;
        string s;
        
        while (!str.empty()) {
            size_t p = str.find(' ');
            int len = str.size();
            s = str.substr(0, p);
            str = str.substr(p+1, len-p-1);
            
            if (pattern.size() < i+1) {
                match = false;
                break;
            }
            
            if (ht.find(pattern[i]) == ht.end()) {
                if (ht2.find(s) != ht2.end()) {
                    match = false;
                    break;
                }
                ht[pattern[i]] = s;
                ht2[s] = pattern[i];
            } else {
                if (ht[pattern[i]] != s) {
                    match = false;
                    break;
                }
            }
            i ++;
            if (p == -1) {
                if (i < pattern.size()) {
                    match = false;
                }
                break;
            }
        }
        
        return match;
    }
};
```


