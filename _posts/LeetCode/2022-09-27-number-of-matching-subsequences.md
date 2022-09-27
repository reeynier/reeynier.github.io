---
layout: post
title: "Number Of Matching Subsequences Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Trie, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 792. Given a string s and an array of strings words, return the number of words[i] that is a subsequence of s.

---

<br />

## Description

LeetCode Problem 792.

Given a string s and an array of strings words, return the number of words[i] that is a subsequence of s.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.
* For example, "ace" is a subsequence of "abcde".

Example 1:
```
Input: s = "abcde", words = ["a","bb","acd","ace"]
Output: 3
Explanation: There are three strings in words that are a subsequence of s: "a", "acd", "ace".
```

Example 2:
```
Input: s = "dsahjpjauf", words = ["ahjpjau","ja","ahbwzgqnuk","tnmlanowax"]
Output: 2
```

Constraints:
* 1 <= s.length <= 5 * 10^4
* 1 <= words.length <= 5000
* 1 <= words[i].length <= 50
* s and words[i] consist of only lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    // Brute force checking will time out, we need efficent way to look up words
    // Create an vector that stores indices for each character a-z in S
    // Then for each word, do a binary search for next index for current character in word 
    // that is greater than the index we last found for the last character
    // If it doesn't exist, word doesn't exist, otherwise continue to search for word
    int numMatchingSubseq (string S, vector<string>& words) {
        vector<vector<int>> alpha (26);
        for (int i = 0; i < S.size (); ++i) 
            alpha[S[i] - 'a'].push_back (i);
        int res = 0;

        for (const auto& word : words) {
            int x = -1;
            bool found = true;

            for (char c : word) {
                auto it = upper_bound (alpha[c - 'a'].begin (), alpha[c - 'a'].end (), x);
                if (it == alpha[c - 'a'].end ()) 
                    found = false;
                else 
                    x = *it;
            }

            if (found) res++;
        }

        return res;
    }
};
```


