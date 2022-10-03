---
layout: post
title: "K-Similar Strings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 854. Strings s1 and s2 are k-similar (for some non-negative integer k) if we can swap the positions of two letters in s1 exactly k times so that the resulting string equals s2.

---

<br />

## Description

LeetCode Problem 854.

Strings s1 and s2 are k-similar (for some non-negative integer k) if we can swap the positions of two letters in s1 exactly k times so that the resulting string equals s2.

Given two anagrams s1 and s2, return the smallest k for which s1 and s2 are k-similar.

Example 1:
```
Input: s1 = "ab", s2 = "ba"
Output: 1
```

Example 2:
```
Input: s1 = "abc", s2 = "bca"
Output: 2
```

Example 3:
```
Input: s1 = "abac", s2 = "baca"
Output: 2
```

Example 4:
```
Input: s1 = "aabc", s2 = "abca"
Output: 2
```

Constraints:
* 1 <= s1.length <= 20
* s2.length == s1.length
* s1 and s2 contain only lowercase letters from the set {'a', 'b', 'c', 'd', 'e', 'f'}.
* s2 is an anagram of s1.

<br />

## Sample C++ Code using Breadth-First Search 


```c
class Solution {
public:
    int kSimilarity(string A, string B) {
        if (A == B) return 0;
        
        unordered_set<string> visit;
        queue<pair<string, int>> q;
        
        int n = A.size();
        int step = 0;
        
        int i = 0;
        for (; i < n; ++i) {
            if (A[i] != B[i]) break;
        }
        
        q.push({A, i});
        visit.insert(A);
        
        while (!q.empty()) {
            int size = q.size();
            
            for (int i = 0; i < size; ++i) {
                string t = move(q.front().first);
                int index = q.front().second;
                q.pop();
                
                if (t == B) return step;
                
                while (t[index] == B[index]) ++index;
                for (int i = index + 1; i < n; ++i) {
                    if (t[i] == B[index] && t[i] != B[i]) {
                        swap(t[index], t[i]);
                        
                        if (visit.count(t) == 0) {
                            q.push({t, index+1});
                            visit.insert(t);
                        }
                        
                        swap(t[index], t[i]);
                    }
                }
            }
            ++step;
        }
        
        return step;
    }
};
```


