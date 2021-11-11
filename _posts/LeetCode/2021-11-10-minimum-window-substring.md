---
layout: post
title:  "Minimum Window Substring Problem"
categories: [ Data Structure ]
tags: [ Hash Table String, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 76. Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window.
---

<br />

## Description

LeetCode Problem 76. 

Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

A substring is a contiguous sequence of characters within the string.

 

Example 1:
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

Example 2:
```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
```

Example 3:
```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```
 

Constraints:

* m == s.length
* n == t.length
* 1 <= m, n <= 10^5
* s and t consist of uppercase and lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string minWindow(string s, string t) {
        int len_s = s.size();
        int len_t = t.size();
        
        unordered_map<char, int> ht;
        for (int i = 0; i < len_t; i ++) {
            ht[t[i]] ++;
        }
        
        int i = 0, j = 0;
        int cnt = ht.size();
        int min_win = INT_MAX;
        string ans;
        for (i = 0; i < len_s; i ++) {
            while ((cnt != 0) && (j < len_s)) {
                if (ht.find(s[j]) != ht.end()) {
                    ht[s[j]] --;
                    if (ht[s[j]] == 0)
                        cnt --;
                }
                j ++;
            }
            if ((cnt == 0) && (min_win > j - i)) {
                min_win = j - i;
                ans = s.substr(i, j - i);
            }
            if (t.find(s[i]) != string::npos) {
                ht[s[i]] ++;
                if (ht[s[i]] > 0)
                    cnt ++;
            }
            

        }
        return ans;
    }
};
```
