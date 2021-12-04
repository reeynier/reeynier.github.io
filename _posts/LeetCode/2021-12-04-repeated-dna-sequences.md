---
layout: post
title: "Repeated DNA Sequences Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Bit Manipulation, Sliding Window, Rolling Hash, Hash Function ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 187. The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'.

---

<br />

## Description

LeetCode Problem 187.

The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'.
* For example, "ACGAATTCCG" is a DNA sequence.

When studying DNA, it is useful to identify repeated sequences within the DNA.

Given a string s that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in any order.

Example 1:
```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
Output: ["AAAAACCCCC","CCCCCAAAAA"]
```

Example 2:
```
Input: s = "AAAAAAAAAAAAA"
Output: ["AAAAAAAAAA"]
```

Constraints:
* 1 <= s.length <= 10^5
* s[i] is either 'A', 'C', 'G', or 'T'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        int l = s.size();
        vector<string> ans;
        if (l < 10)
            return ans;
        
        unordered_map<string, int> ht;
        string subs;
        for (int i = 0; i < l - 10 + 1; i ++) {
            subs = s.substr(i, 10);
            if (ht.find(subs) == ht.end()) {
                ht[subs] = 0;
            } 
            ht[subs] ++;
            if (ht[subs] == 2)
                ans.push_back(subs);
                
        }
        return ans;
            
    }
};
```


