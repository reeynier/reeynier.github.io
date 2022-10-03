---
layout: post
title: "Find And Replace Pattern Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 890. Given a list of strings words and a string pattern, return a list of words[i] that match pattern. You may return the answer in any order.

---

<br />

## Description

LeetCode Problem 890.

Given a list of strings words and a string pattern, return a list of words[i] that match pattern. You may return the answer in any order.

A word matches the pattern if there exists a permutation of letters p so that after replacing every letter x in the pattern with p(x), we get the desired word.

Recall that a permutation of letters is a bijection from letters to letters: every letter maps to another letter, and no two letters map to the same letter.

Example 1:
```
Input: words = ["abc","deq","mee","aqq","dkd","ccc"], pattern = "abb"
Output: ["mee","aqq"]
Explanation: "mee" matches the pattern because there is a permutation {a -> m, b -> e, ...}. 
"ccc" does not match the pattern because {a -> c, b -> c, ...} is not a permutation, since a and b map to the same letter.
```

Example 2:
```
Input: words = ["a","b","c"], pattern = "a"
Output: ["a","b","c"]
```

Constraints:
* 1 <= pattern.length <= 20
* 1 <= words.length <= 50
* words[i].length == pattern.length
* pattern and words[i] are lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> findAndReplacePattern(vector<string>& words, string pattern) {
        int n = words.size();
        vector<map<char,char>> m(n);
        
        for (int i = 0; i < n; ++i) {
            set<int> s;
            for (int j = 0; j < words[i].size(); ++j) {
                if (s.find(pattern[j]) == s.end()) {
                    s.insert(pattern[j]);
                    m[i][words[i][j]] = pattern[j];
                }
            }
        }
        vector<string> ans;
        for (int i = 0; i < n; ++i) {
            string k = words[i];
            for (int j = 0; j < words[i].size(); ++j) {
                  words[i][j] = m[i][words[i][j]];
            }
            if (words[i] == pattern) {
                ans.push_back(k);
            }
        }
        return ans;
    }
};
```


