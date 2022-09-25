---
layout: post
title: "Reconstruct Original Digits From English Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 423. Given a string s containing an out-of-order English representation of digits 0-9, return the digits in ascending order.

---

<br />

## Description

LeetCode Problem 423.

Given a string s containing an out-of-order English representation of digits 0-9, return the digits in ascending order.

Example 1:
```
Input: s = "owoztneoer"
Output: "012"
```

Example 2:
```
Input: s = "fviefuro"
Output: "45"
```

Constraints:
* 1 <= s.length <= 10^5
* s[i] is one of the characters ["e","g","f","i","h","o","n","s","r","u","t","w","v","x","z"].
* s is guaranteed to be valid.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string originalDigits(string s) {
        vector<string> words = {"zero", "two", "four", "six", "eight", "one", "three", "five", "seven", "nine"};
        vector<int> nums = {0, 2, 4, 6, 8, 1, 3, 5, 7, 9};
        vector<int> distinct_char = {'z', 'w', 'u', 'x', 'g', 'o', 'r', 'f', 'v', 'i'};
        vector<int> counts(26, 0);
        string result;
        for(auto ch : s){ counts[ch-'a']++;}
        for(int i = 0; i < 10; i++){
            int count = counts[distinct_char[i]-'a'];
            for(int j = 0; j < words[i].size(); j++)
                counts[words[i][j]-'a'] -= count;
            while(count--)
                result += to_string(nums[i]);
        }
        sort(result.begin(), result.end());
        return result;
    }
};
```


