---
layout: post
title: "Remove Duplicate Letters Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Stack, Greedy, Monotonic Stack ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 316. Given a string s, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

---

<br />

## Description

LeetCode Problem 316.

Given a string s, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

Example 1:
```
Input: s = "bcabc"
Output: "abc"
```

Example 2:
```
Input: s = "cbacdcbc"
Output: "acdb"
```

Constraints:
* 1 <= s.length <= 10^4
* s consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string removeDuplicateLetters(string s) {
        int len = s.size();
        string res = "";
        unordered_map<char, int> M;
        unordered_map<char, bool> V;
        stack<int> S;
        
        for (auto c : s) {
            if (M.find(c) == M.end()) M[c] = 1;
            else M[c]++; 
        }
        for (unordered_map<char, int>::iterator iter=M.begin(); iter!=M.end(); iter++) V[iter->first] = false;
        
        for (int i=0; i<len; i++) {
            M[s[i]]--;
            if (V[s[i]] == true) continue;
            
            while (!S.empty() and s[i] < s[S.top()] and M[s[S.top()]] > 0) {
                V[s[S.top()]] = false;
                S.pop();
            }
            S.push(i);
            V[s[i]] = true;
        }
        while (!S.empty()) {
            res = s[S.top()] + res;
            S.pop();
        }
        return res;
    }
};
```


