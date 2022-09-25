---
layout: post
title: "Permutation In String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Two Pointers, String, Sliding Window ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 567. Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

---

<br />

## Description

LeetCode Problem 567.

Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.
In other words, return true if one of s1's permutations is the substring of s2.

Example 1:
```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```

Example 2:
```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
```

Constraints:
* 1 <= s1.length, s2.length <= 10^4
* s1 and s2 consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:    
    bool checkInclusion(string s1, string s2) {
        int l1 = s1.size(), l2 = s2.size();
        if (l1 > l2) return false;
        
        vector<int> m(26, 0);
        
        for (int i = 0; i < l1; i ++) {
            m[s1[i] - 'a'] ++;
            m[s2[i] - 'a'] --;
        }
        
        bool contained = true;
        for (int i = 0; i < 26; i ++) {
            if (m[i] != 0) {
                contained = false;
                break;
            }
        }
        if (contained) return true;
        
        for (int i = l1; i < l2; i ++) {
            m[s2[i] - 'a'] --;
            m[s2[i-l1] - 'a'] ++;
            
            contained = true;
            for (int j = 0; j < 26; j ++) {
                if (m[j] != 0) {
                    contained = false;
                    break;
                }
            }
            if (contained) return true;
            
            
        }
        
        return false;
    }
};
```


