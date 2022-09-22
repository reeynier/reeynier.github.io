---
layout: post
title: "Longest Word In Dictionary Through Deleting Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, String, Sorting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 524. Given a string s and a string array dictionary, return the longest string in the dictionary that can be formed by deleting some of the given string characters. If there is more than one possible result, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

---

<br />

## Description

LeetCode Problem 524.

Given a string s and a string array dictionary, return the longest string in the dictionary that can be formed by deleting some of the given string characters. If there is more than one possible result, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

Example 1:
```
Input: s = "abpcplea", dictionary = ["ale","apple","monkey","plea"]
Output: "apple"
```

Example 2:
```
Input: s = "abpcplea", dictionary = ["a","b","c"]
Output: "a"
```

Constraints:
* 1 <= s.length <= 1000
* 1 <= dictionary.length <= 1000
* 1 <= dictionary[i].length <= 1000
* s and dictionary[i] consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool canFormByDeleting(string word, string str) {
        int word_i = 0, str_i = 0;
        while (word_i < word.size() && str_i < str.size()) {
            if (word[word_i] == str[str_i])
                word_i++; 
            str_i++;
        }
        return word_i == word.size();
    }
    
    string findLongestWord(string s, vector<string>& d) {
        string res = "";
        for (auto str : d) {
            if (canFormByDeleting(str, s)) {
                if (str.size() > res.size() || (str.size() == res.size() && str < res))
                    res = str;
            }
        }
        return res;
    }
};
```


