---
layout: post
title:  "Substring with Concatenation of All Words Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Sliding Window, String, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 30. You are given a string s and an array of strings words of the same length.
---

<br />

## Description

LeetCode Problem 30. 

You are given a string s and an array of strings words of the same length. Return all starting indices of substring(s) in s that is a concatenation of each word in words exactly once, in any order, and without any intervening characters.

You can return the answer in any order.

 

Example 1:
```
Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```

Example 2:
```
Input: s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
Output: []
```

Example 3:
```
Input: s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
Output: [6,9,12]
```
 

Constraints:

* 1 <= s.length <= 10^4
* s consists of lower-case English letters.
* 1 <= words.length <= 5000
* 1 <= words[i].length <= 30
* words[i] consists of lower-case English letters.



<br />

## Sample C++ Code


```c
class Solution {
public:
    vector findSubstring(string s, vector& words) {
        unordered_map<string, int> counts;
        for (string word : words)
            counts[word]++;
        int n = s.length(), num = words.size(), len = words[0].length();
        vector indexes;
        for (int i = 0; i < n - num * len + 1; i++) {
            unordered_map<string, int> seen;
            int j = 0;
            for (; j < num; j++) {
                string word = s.substr(i + j * len, len);
                if (counts.find(word) != counts.end()) {
                    seen[word]++;
                    if (seen[word] > counts[word])
                        break;
                }
                else break;
            }
            if (j == num) indexes.push_back(i);
        }
        return indexes;
    }
};
```
