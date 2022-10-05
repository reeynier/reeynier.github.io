---
layout: post
title: "Word Subsets Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 916. You are given two string arrays words1 and words2.

---

<br />

## Description

LeetCode Problem 916.

You are given two string arrays words1 and words2.

A string b is a subset of string a if every letter in b occurs in a including multiplicity.
* For example, "wrr" is a subset of "warrior" but is not a subset of "world".

A string a from words1 is universal if for every string b in words2, b is a subset of a.

Return an array of all the universal strings in words1. You may return the answer in any order.

Example 1:
```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["e","o"]
Output: ["facebook","google","leetcode"]
```

Example 2:
```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["l","e"]
Output: ["apple","google","leetcode"]
```

Example 3:
```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["e","oo"]
Output: ["facebook","google"]
```

Example 4:
```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["lo","eo"]
Output: ["google","leetcode"]
```

Example 5:
```
Input: words1 = ["amazon","apple","facebook","google","leetcode"], words2 = ["ec","oc","ceo"]
Output: ["facebook","leetcode"]
```

Constraints:
* 1 <= words1.length, words2.length <= 10^4
* 1 <= words1[i].length, words2[i].length <= 10
* words1[i] and words2[i] consist only of lowercase English letters.
* All the strings of words1 are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> wordSubsets(vector<string>& words1, vector<string>& words2) {
        vector<string> ans;
        vector<int> universal(26, 0);
        for (char &ch : words2[0]) 
            universal[ch-'a']++;
        for (int i = 1; i < words2.size(); ++i) {
            vector<int> temp(26,0);
            for (char &ch : words2[i])
                if (universal[ch-'a'] < ++temp[ch-'a']) 
                    universal[ch-'a']++;
        }
        for (string &str  : words1) {
            vector<int> freq(26, 0);
            for (char &ch : str) 
                freq[ch-'a']++;
            bool valid = true;
            for (int i = 0; i < 26 && valid; i++)
                if (freq[i] < universal[i]) 
                    valid = false;
            if (valid) 
                ans.emplace_back(str);
        }
        return ans;
    }
};
```


