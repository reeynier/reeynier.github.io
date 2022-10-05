---
layout: post
title: "Uncommon Words From Two Sentences Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 884. A sentence is a string of single-space separated words where each word consists only of lowercase letters.

---

<br />

## Description

LeetCode Problem 884.

A sentence is a string of single-space separated words where each word consists only of lowercase letters.

A word is uncommon if it appears exactly once in one of the sentences, and does not appear in the other sentence.

Given two sentences s1 and s2, return a list of all the uncommon words. You may return the answer in any order.

Example 1:
```
Input: s1 = "this apple is sweet", s2 = "this apple is sour"
Output: ["sweet","sour"]
```

Example 2:
```
Input: s1 = "apple apple", s2 = "banana"
Output: ["banana"]
```

Constraints:
* 1 <= s1.length, s2.length <= 200
* s1 and s2 consist of lowercase English letters and spaces.
* s1 and s2 do not have leading or trailing spaces.
* All the words in s1 and s2 are separated by a single space.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> uncommonFromSentences(string A, string B) {
        string nw = A + " " + B, str = "";
        map<string, int> m;
        vector<string> ans;
        for (char x : nw) {
            i f(x == ' ') {
                m[str] ++;
                str = "";
            }
            else 
                str += x;
        }
        m[str] ++;
        for (auto it : m) {
            if (it.second == 1) 
                ans.push_back(it.first);
        }
        return ans;
    }
};
```


