---
layout: post
title:  "Longest Substring Without Repeating Characters Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 3. Given a string s, find the length of the longest substring without repeating characters.
---

<br />

## Description

LeetCode Problem 3. 

Given a string s, find the length of the longest substring without repeating characters.

Example 1:
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

Example 2:
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

Example 3:
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

Example 4:
```
Input: s = ""
Output: 0
```

Constraints:

* 0 <= s.length <= 5 * 104
* s consists of English letters, digits, symbols and spaces.

<br />

## Sample C++ Code


This is a C++ solution using a `hash table`.

```c
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int len = s.size();
        int max_len = 0;
        unordered_map<char, int> ht;
        
        int i = 0, j = 0;
        for (i = 0; i < len; i ++) {
            while ((ht.find(s[j]) == ht.end()) && (j < len)) {
                ht[s[j]] = 1;
                j ++;
            }      
            
            max_len = max(max_len, j - i);
            ht.erase(s[i]);
        }
        return max_len;
    }
};
```
