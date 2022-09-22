---
layout: post
title: "Keyboard Row Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 500. Given an array of strings words, return the words that can be typed using letters of the alphabet on only one row of American keyboard like the image below.

---

<br />

## Description

LeetCode Problem 500.

Given an array of strings words, return the words that can be typed using letters of the alphabet on only one row of American keyboard like the image below.

In the American keyboard:
* the first row consists of the characters "qwertyuiop",
* the second row consists of the characters "asdfghjkl", and
* the third row consists of the characters "zxcvbnm".

Example 1:
```
Input: words = ["Hello","Alaska","Dad","Peace"]
Output: ["Alaska","Dad"]
```

Example 2:
```
Input: words = ["omk"]
Output: []
```

Example 3:
```
Input: words = ["adsdf","sfd"]
Output: ["adsdf","sfd"]
```

Constraints:
* 1 <= words.length <= 20
* 1 <= words[i].length <= 100
* words[i] consists of English letters (both lowercase and uppercase).

<br />

## Sample C++ Code


```c
class Solution {
  public:
    vector<string> findWords(vector<string> &words) {
        vector<unordered_set<char>> dict = {
            {'q', 'Q', 'w', 'W', 'e', 'E', 'r', 'R', 't', 'T', 'y', 'Y', 'u', 'U', 'i', 'I', 'o', 'O', 'p', 'P'},
            {'a', 'A', 's', 'S', 'd', 'D', 'f', 'F', 'g', 'G', 'h', 'H', 'j', 'J', 'k', 'K', 'l', 'L'},
            {'z', 'Z', 'x', 'X', 'c', 'C', 'v', 'V', 'b', 'B', 'n', 'N', 'm', 'M'}};

        vector<string> res;

        for (auto &word : words) {
            vector<bool> d(3, true);

            for (auto &ch : word)
                for (int i = 0; i < 3; ++i)
                    if (d[i] && dict[i].find(ch) == dict[i].end())
                        d[i] = false;

            if (d[0] || d[1] || d[2])
                res.push_back(word);
        }

        return res;
    }
};
```


