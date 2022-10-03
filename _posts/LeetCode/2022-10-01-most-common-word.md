---
layout: post
title: "Most Common Word Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Counting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 819. Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.

---

<br />

## Description

LeetCode Problem 819.

Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.

The words in paragraph are case-insensitive and the answer should be returned in lowercase.

Example 1:
```
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```

Example 2:
```
Input: paragraph = "a.", banned = []
Output: "a"
```

Constraints:
* 1 <= paragraph.length <= 1000
* paragraph consists of English letters, space ' ', or one of the symbols: "!?',;.".
* 0 <= banned.length <= 100
* 1 <= banned[i].length <= 10
* banned[i] consists of only lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string mostCommonWord(string paragraph, vector<string>& banned) {
        unordered_map<string, int>m;
        for (int i = 0; i < paragraph.size();) {
            string s = "";
            while (i < paragraph.size() && isalpha(paragraph[i])) 
                s.push_back(tolower(paragraph[i++]));
            while (i < paragraph.size() && !isalpha(paragraph[i])) 
                i++;
            m[s]++;
        }
        for (auto x : banned) 
            m[x] = 0;
        string res = "";
        int count = 0;
        for (auto x : m)
            if (x.second > count) 
                res = x.first, count = x.second;
        return res;  
    }
};
```


