---
layout: post
title: "Buddy Strings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 859. Given two strings s and goal, return true if you can swap two letters in s so the result is equal to goal, otherwise, return false.

---

<br />

## Description

LeetCode Problem 859.

Given two strings s and goal, return true if you can swap two letters in s so the result is equal to goal, otherwise, return false.

Swapping letters is defined as taking two indices i and j (0-indexed) such that i != j and swapping the characters at s[i] and s[j].

* For example, swapping at indices 0 and 2 in "abcd" results in "cbad".

Example 1:
```
Input: s = "ab", goal = "ba"
Output: true
Explanation: You can swap s[0] = 'a' and s[1] = 'b' to get "ba", which is equal to goal.
```

Example 2:
```
Input: s = "ab", goal = "ab"
Output: false
Explanation: The only letters you can swap are s[0] = 'a' and s[1] = 'b', which results in "ba" != goal.
```

Example 3:
```
Input: s = "aa", goal = "aa"
Output: true
Explanation: You can swap s[0] = 'a' and s[1] = 'a' to get "aa", which is equal to goal.
```

Example 4:
```
Input: s = "aaaaaaabc", goal = "aaaaaaacb"
Output: true
```

Constraints:
* 1 <= s.length, goal.length <= 2 * 10^4
* s and goal consist of lowercase letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool buddyStrings(string A, string B) {
         if (A == B)
            return (set<char>(A.begin(), A.end()).size() < A.size());
        
        int n = A.length();
        int l = 0, r = n-1;
        
        while (l < n && A[l] == B[l])
            l++;
        while (r >= 0 && A[r] == B[r])
            r--;
        if (l < r)
            swap(A[l], A[r]);
        
        return A == B; 
    }
};
```


