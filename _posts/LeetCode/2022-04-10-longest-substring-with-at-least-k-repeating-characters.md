---
layout: post
title: "Longest Substring With At Least K Repeating Characters Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Divide and Conquer, Sliding Window ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 395. Given a string s and an integer k, return the length of the longest substring of s such that the frequency of each character in this substring is greater than or equal to k.

---

<br />

## Description

LeetCode Problem 395.

Given a string s and an integer k, return the length of the longest substring of s such that the frequency of each character in this substring is greater than or equal to k.

Example 1:
```
Input: s = "aaabb", k = 3
Output: 3
Explanation: The longest substring is "aaa", as 'a' is repeated 3 times.
```

Example 2:
```
Input: s = "ababbc", k = 2
Output: 5
Explanation: The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```

Constraints:
* 1 <= s.length <= 10^4
* s consists of only lowercase English letters.
* 1 <= k <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    int longestSubstring(string s, int k) {
        if (s.size() == 0 || k > s.size())   
        	return 0;
        if (k == 0)  
        	return s.size();
        
        unordered_map<char,int> Map;
        for (int i = 0; i < s.size(); i++) {
            Map[s[i]]++;
        }
        
        int idx =0;
        while (idx <s.size() && Map[s[idx]] >= k) 
        	idx++;
        if (idx == s.size()) 
        	return s.size();
        
        int left = longestSubstring(s.substr(0, idx), k);
        int right = longestSubstring(s.substr(idx+1), k);
        
        return max(left, right);
    }
};
```


