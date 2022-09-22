---
layout: post
title: "Detect Capital Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 520. We define the usage of capitals in a word to be right when one of the following cases holds

---

<br />

## Description

LeetCode Problem 520.

We define the usage of capitals in a word to be right when one of the following cases holds:
* All letters in this word are capitals, like "USA".
* All letters in this word are not capitals, like "leetcode".
* Only the first letter in this word is capital, like "Google".

Given a string word, return true if the usage of capitals in it is right.

Example 1:
```
Input: word = "USA"
Output: true
```

Example 2:
```
Input: word = "FlaG"
Output: false
```

Constraints:
* 1 <= word.length <= 100
* word consists of lowercase and uppercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool detectCapitalUse(string word) {
        for(int i = 1; i < word.size(); i++) {
            if(isupper(word[1]) != isupper(word[i]) || 
               islower(word[0]) && isupper(word[i])) 
                return false;
        }        
        return true;
    }
};
```


