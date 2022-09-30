---
layout: post
title: "Array Of Doubled Pairs Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Greedy, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 954. Given an integer array of even length arr, return true if it is possible to reorder arr such that arr[2 * i + 1] = 2 * arr[2 * i] for every 0 <= i < len(arr) / 2, or false otherwise.

---

<br />

## Description

LeetCode Problem 954.

Given an integer array of even length arr, return true if it is possible to reorder arr such that arr[2 * i + 1] = 2 * arr[2 * i] for every 0 <= i < len(arr) / 2, or false otherwise.

Example 1:
```
Input: arr = [3,1,3,6]
Output: false
```

Example 2:
```
Input: arr = [2,1,2,6]
Output: false
```

Example 3:
```
Input: arr = [4,-2,2,-4]
Output: true
Explanation: We can take two groups, [-2,-4] and [2,4] to form [-2,-4,2,4] or [2,4,-2,-4].
```

Example 4:
```
Input: arr = [1,2,4,16,8,4]
Output: false
```

Constraints:
* 2 <= arr.length <= 3 * 10^4
* arr.length is even.
* -10^5 <= arr[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool canReorderDoubled(vector<int>& arr) {
        unordered_map<int, int> freq;
        for (auto num : arr) freq[num]++;
        
        sort(arr.begin(), arr.end());
        
        for (auto num : arr) {
            if (freq[num] && freq[num*2]) {
                freq[num]--;
                freq[num*2]--;
            }
        }
        
        for (auto [a, b] : freq)
            if (b) return false;
        
        return true;
    }
};
```


