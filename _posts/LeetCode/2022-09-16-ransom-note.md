---
layout: post
title: "Ransom Note Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Counting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 383. Given two stings ransomNote and magazine, return true if ransomNote can be constructed from magazine and false otherwise.

---

<br />

## Description

LeetCode Problem 383.

Given two stings ransomNote and magazine, return true if ransomNote can be constructed from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

Example 1:
```
Input: ransomNote = "a", magazine = "b"
Output: false
```

Example 2:
```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

Example 3:
```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

Constraints:
* 1 <= ransomNote.length, magazine.length <= 10^5
* ransomNote and magazine consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        int count[26] = {0};
        for(char ch : magazine)
            count[ch - 'a']++;
        
        for(char ch : ransomNote)
            if(count[ch - 'a']-- <= 0)
                return false;
        
        return true;
    }
};
```


