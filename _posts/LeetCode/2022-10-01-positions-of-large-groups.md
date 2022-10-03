---
layout: post
title: "Positions Of Large Groups Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 830. In a string sof lowercase letters, these letters form consecutive groups of the same character.

---

<br />

## Description

LeetCode Problem 830.

In a string s of lowercase letters, these letters form consecutive groups of the same character.

For example, a string like s = "abbxxxxzyy" has the groups "a", "bb", "xxxx", "z", and"yy".

A group is identified by an interval[start, end], wherestartandenddenote the start and endindices (inclusive) of the group. In the above example,"xxxx"has the interval[3,6].

A group is consideredlargeif it has 3 or more characters.

Returnthe intervals of every large group sorted inincreasing order by start index.

Example 1:
```
Input: s = "abbxxxxzzy"
Output: [[3,6]]
Explanation: "xxxx" is the only large group with start index 3 and end index 6.
```

Example 2:
```
Input: s = "abc"
Output: []
Explanation: We have groups "a", "b", and "c", none of which are large groups.
```

Example 3:
```
Input: s = "abcdddeeeeaabbbcd"
Output: [[3,5],[6,9],[12,14]]
Explanation: The large groups are "ddd", "eeee", and "bbb".
```

Example 4:
```
Input: s = "aba"
Output: []
```

Constraints:
* 1 <= s.length <= 1000
* s contains lower-case English letters only.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string s) {
        vector<vector<int>> res;
        int left = 0, right = 0;
        while (left < s.size()) {
            while (s[left] == s[right]) 
                right++;
            if (right - left >= 3) 
                res.push_back({left, right-1});
            left = right;
        }
        return res;
    }
};
```


