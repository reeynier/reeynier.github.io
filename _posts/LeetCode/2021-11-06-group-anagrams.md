---
layout: post
title:  "Group Anagrams Problem"
categories: [ Data Structure ]
tags: [ Hash Table, String, Sorting, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 49. Given an array of strings strs, group the anagrams together. You can return the answer in any order.
---

<br />

## Description

LeetCode Problem 49. 

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

Example 2:
```
Input: strs = [""]
Output: [[""]]
```

Example 3:
```
Input: strs = ["a"]
Output: [["a"]]
``` 

Constraints:

* 1 <= strs.length <= 10^4
* 0 <= strs[i].length <= 100
* strs[i] consists of lowercase English letters.


<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        int freq[26] = {0};
        map<string, int> ht;
        vector<vector<string>> ans;
        int idx = 0;
        
        for (int i = 0; i < strs.size(); i ++) {
            for (int j = 0; j < 26; j ++)
                freq[j] = 0;
            for (int j = 0; j < strs[i].size(); j ++) {
                freq[strs[i][j] - 'a'] ++;
            }
            string s = "";
            for (int j = 0; j < 26; j ++) {
                s += to_string(j) + to_string(freq[j]);
            }
            if (ht.find(s) == ht.end()) {
                ht[s] = idx;
                idx ++;
                vector<string> line;
                ans.push_back(line);
            }
            ans[ht[s]].push_back(strs[i]);
        }
        return ans;
    }
};
```
