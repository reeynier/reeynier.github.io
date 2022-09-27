---
layout: post
title: "Maximum Swap Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Greedy ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 670. You are given an integer num. You can swap two digits at most once to get the maximum valued number.

---

<br />

## Description

LeetCode Problem 670.

You are given an integer num. You can swap two digits at most once to get the maximum valued number.

Return the maximum valued number you can get.

Example 1:
```
Input: num = 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
```

Example 2:
```
Input: num = 9973
Output: 9973
Explanation: No swap.
```

Constraints:
* 0 <= num <= 10^8

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maximumSwap(int num) {
        string n = to_string(num);
        
        // Keep in a map the last accurance of each digit:
        unordered_map<int, int> last;
        for (int i = 0; i < n.size(); i++)
            last[n[i] - '0'] = i;
        
        for (int i = 0; i < n.size(); i++) {
            for (int j = 9; j > n[i]-'0'; j--) {
                // If there's a larger digit later - swap:
                if (last[j] > i) {
                    swap(n[last[j]], n[i]);
                    return stoi(n);
                }
            }
        }
        return stoi(n);
    }
};
```


