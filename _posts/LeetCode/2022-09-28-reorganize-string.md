---
layout: post
title: "Reorganize String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Greedy, Sorting, Heap ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 767. Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

---

<br />

## Description

LeetCode Problem 767.

Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

Return any possible rearrangement of s or return "" if not possible.

Example 1:
```
Input: s = "aab"
Output: "aba"
```

Example 2:
```
Input: s = "aaab"
Output: ""
```

Constraints:
* 1 <= s.length <= 500
* s consists of lowercase English letters.

<br />

## Sample C++ Code using Priority Queue


```c
class Solution {
public:
    string reorganizeString(string S) {
        string res = "";
        unordered_map<char,int> mp;
        priority_queue<pair<int,char>> pq;
        
        for (auto s : S)
            mp[s] += 1;
        for (auto m : mp)
            pq.push(make_pair(m.second, m.first));
        
        while (pq.size() > 1) {
            auto top1 = pq.top();
            pq.pop();
            auto top2 = pq.top();
            pq.pop();
            
            res += top1.second;
            res += top2.second;
            
            top1.first -= 1;
            top2.first -= 1;
            
            if (top1.first > 0)
                pq.push(top1);
            if (top2.first > 0)
                pq.push(top2);
        }
        
        if (!pq.empty()) {
            if (pq.top().first > 1)
                return "";
            else
                res += pq.top().second;
        }
        
        return res;
    }
};
```


