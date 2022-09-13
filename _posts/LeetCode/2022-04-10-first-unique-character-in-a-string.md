---
layout: post
title: "First Unique Character In A String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Queue, Counting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 387. Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.
---

<br />

## Description

LeetCode Problem 387.

Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

Example 1:
```
Input: s = "leetcode"
Output: 0
```

Example 2:
```
Input: s = "loveleetcode"
Output: 2
```

Example 3:
```
Input: s = "aabb"
Output: -1
```

Constraints:
* 1 <= s.length <= 10^5
* s consists of only lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int firstUniqChar(string s) {
        int ht[26] = {0};
        
        for (int i = 0; i < s.size(); i ++) {
            ht[s[i] - 'a'] ++;
        }
        
        for (int i = 0; i < s.size(); i ++) {
            if (ht[s[i] - 'a'] == 1)
                return i;
        }
        
        return -1;
    }
};
```


