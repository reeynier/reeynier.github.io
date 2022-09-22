---
layout: post
title: "Find All Anagrams In A String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Sliding Window ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 438. Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

---

<br />

## Description

LeetCode Problem 438.

Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:
```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

Example 2:
```
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

Constraints:
* 1 <= s.length, p.length <= 3 * 10^4
* s and p consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        int len_s = s.size(), len_p = p.size();
        vector<int> ans;
        if (len_s < len_p)
            return ans;
        
        vector<int> cnt_s(26, 0);
        vector<int> cnt_p(26, 0);
        
        for (int i = 0; i < len_p; i ++) {
            cnt_s[s[i]-'a'] ++;
            cnt_p[p[i]-'a'] ++;
        }
        
        bool eq = true;
        for (int i = 0; i < 26; i ++) {
            if (cnt_s[i] != cnt_p[i]) {
                eq = false;
                break;
            }
        }
        if (eq) ans.push_back(0);
        
        for (int i = 0; i < len_s - len_p; i ++) {
            cnt_s[s[i]-'a'] --;
            cnt_s[s[i+len_p]-'a'] ++;
            bool eq = true;
            for (int j = 0; j < 26; j ++) {
                if (cnt_s[j] != cnt_p[j]) {
                    eq = false;
                    break;
                }
            }
            if (eq) ans.push_back(i+1);
        }
        
        return ans;
    }
};
```


