---
layout: post
title: "Sort Characters By Frequency Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Sorting, Heap ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 451. Given a string s, sort it in decreasing order based on the frequency of the characters. The frequency of a character is the number of times it appears in the string.

---

<br />

## Description

LeetCode Problem 451.

Given a string s, sort it in decreasing order based on the frequency of the characters. The frequency of a character is the number of times it appears in the string.

Return the sorted string. If there are multiple answers, return any of them.

Example 1:
```
Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

Example 2:
```
Input: s = "cccaaa"
Output: "aaaccc"
Explanation: Both 'c' and 'a' appear three times, so both "cccaaa" and "aaaccc" are valid answers.
Note that "cacaca" is incorrect, as the same characters must be together.
```

Example 3:
```
Input: s = "Aabb"
Output: "bbAa"
Explanation: "bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

Constraints:
* 1 <= s.length <= 5 * 10^5
* s consists of uppercase and lowercase English letters and digits.

<br />

## Sample C++ Code


```c
class Solution {
public:
    static bool comp(const pair<char, int>& a, const pair<char, int>& b) {
        return a.second > b.second;
    }
    string frequencySort(string s) {
        map<char, int> freq;
        vector<pair<char, int>> freq_sorted;
        for (int i = 0; i < s.size(); i ++) {
            if (freq.find(s[i]) == freq.end())
                freq[s[i]] = 0;
            freq[s[i]] ++;
        }
        for (map<char, int>::iterator mit = freq.begin(); 
            mit != freq.end(); mit ++) {
            freq_sorted.push_back({mit->first, mit->second});
        }
        sort(freq_sorted.begin(), freq_sorted.end(), comp);
        
        string sortedS = "";
        for (vector<pair<char, int>>::iterator vit = freq_sorted.begin(); 
            vit != freq_sorted.end(); vit ++) {
            for (int i = 0; i < vit->second; i ++)
                sortedS += vit->first;
        }
        return sortedS;
    }
};
```


