---
layout: post
title: "Verifying An Alien Dictionary Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 953. In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

---

<br />

## Description

LeetCode Problem 953.

In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographically in this alien language.

Example 1:
```
Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
Output: true
Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.
```

Example 2:
```
Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
Output: false
Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.
```

Example 3:
```
Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
Output: false
Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '&empty;', where '&empty;' is defined as the blank character which is less than any other character (<a href="https://en.wikipedia.org/wiki/Lexicographical_order" target="_blank">More info</a>).
```

Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 20
* order.length == 26
* All characters in words[i] and order are English lowercase letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isAlienSorted(vector<string>& words, string order) {
        unordered_map<char,int> m;
        for (int i = 0; i < order.size(); i++) 
            m[order[i]] = i;
        for (int i = 0; i < words.size() - 1; i++) {
            string word1 = words[i];
            string word2 = words[i + 1];
            int i1 = 0, i2 = 0;
            while (i1 < word1.size() && i2 < word2.size() && word1[i1] == word2[i2]) {
                i1++, i2++;
            }
            if (i2 == word2.size() && i1 < word1.size()) 
                return false;
            if (i1 < word1.size() && i2 < word2.size()) {
                if (m[word1[i1]] > m[word2[i2]]) 
                    return false;
            }
        }
        return true;
    }
};
```


