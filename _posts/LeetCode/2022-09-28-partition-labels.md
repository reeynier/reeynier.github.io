---
layout: post
title: "Partition Labels Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Two Pointers, String, Greedy ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 763. You are given a string s. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

---

<br />

## Description

LeetCode Problem 763.

You are given a string s. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Return a list of integers representing the size of these parts.

Example 1:
```
Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.
```

Example 2:
```
Input: s = "eccbbbbdec"
Output: [10]
```

Constraints:
* 1 <= s.length <= 500
* s consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> partitionLabels(string S) {
        vector<int> res, pos(26, 0);  
        for (auto i = 0; i < S.size(); ++i) 
            pos[S[i] - 'a'] = i;
        for (auto i = 0, idx = INT_MIN, last_i = 0; i < S.size(); ++i) {
            idx = max(idx, pos[S[i] - 'a']);
            if (idx == i) 
                res.push_back(i - exchange(last_i, i + 1) + 1);
        }
        return res;
    }
};
```


