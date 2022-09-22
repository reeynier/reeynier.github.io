---
layout: post
title: "Longest Repeating Character Replacement Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Sliding Window ]
similar: [ Sliding Window ]
featured: false
hidden: false
excerpt: LeetCode 424. You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

---

<br />

## Description

LeetCode Problem 424.

You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

Example 1:
```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```

Example 2:
```
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

Constraints:
* 1 <= s.length <= 10^5
* s consists of only uppercase English letters.
* 0 <= k <= s.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    int characterReplacement(string s, int k) {
        int len = s.size();
        
        int maxlen = 0;
        for (char c = 'A'; c <= 'Z'; c ++) {
            int left = 0;
            int replaced = 0;
            for (int right = 0; right < len; right ++) {
                if (s[right] != c) {
                    replaced ++;
                }
                if (replaced <= k) {
                    maxlen = max(maxlen, right - left + 1);
                } else {
                    while (left < right && replaced > k) {
                        if (s[left] != c)
                            replaced --;
                        left ++;
                    }
                }
            }
        }
        return maxlen;
    }
};
```


