---
layout: post
title: "Longest Uncommon Subsequence II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Two Pointers, String, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 522. Given an array of strings strs, return the length of the longest uncommon subsequence between them. If the longest uncommon subsequence does not exist, return -1.

---

<br />

## Description

LeetCode Problem 522.

Given an array of strings strs, return the length of the longest uncommon subsequence between them. If the longest uncommon subsequence does not exist, return -1.

An uncommon subsequence between an array of strings is a string that is a subsequence of one string but not the others.

A subsequence of a string s is a string that can be obtained after deleting any number of characters from s.

* For example, "abc" is a subsequence of "aebdc" because you can delete the underlined characters in "aebdc" to get "abc". Other subsequences of "aebdc" include "aebdc", "aeb", and "" (empty string).

Example 1:
```
Input: strs = ["aba","cdc","eae"]
Output: 3
```

Example 2:
```
Input: strs = ["aaa","aaa","aa"]
Output: -1
```

Constraints:
* 2 <= strs.length <= 50
* 1 <= strs[i].length <= 10
* strs[i] consists of lowercase English letters.

<br />

## Sample C++ Code


```c
// Desending order of string size
bool cmp(pair<string,int> &a, pair<string,int> &b) {
    return a.first.size() > b.first.size();
}

// Return true for s1 = abc, s2 = aebece
bool isSubStringOf(string &s1, string &s2){
    int i = 0, j = 0;
    while (i < s1.size()) {
        while (j < s2.size() && s1[i] != s2[j])
            j++;
        if (j == s2.size())
            return false;
        i++;
        j++;
    }
    return true;
}

class Solution {
public:
    int findLUSlength(vector<string>& strs) {
        // Define a string to int map to save the frequency of each string
        unordered_map<string, int> mp;
        for (const auto& str : strs)
            mp[str]++;
        
        // Define a vector of map element pair and sort it in descending order of string size
        vector<pair<string, int>> vec;
        for (const auto& m : mp)
            vec.push_back(m);
        sort(vec.begin(), vec.end(), cmp);
        
        // For each string in the sorted vector, if all the other string coming before it is
        // NOT super string of it then we use its size as LUS. If each pair of string have 
        // sub string relation then the longest uncommon subsequence doesn't exist
        for (int i = 0; i < vec.size(); i++) {
            if (1 == vec[i].second) {
                int j = 0;
                for (; j < i; j++)
                    if (isSubStringOf(vec[i].first, vec[j].first))
                        break;
                if (j == i)
                    return vec[i].first.size();        
            }
        }
        return -1;
    }
};
```


