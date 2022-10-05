---
layout: post
title: "Largest Time For Given Digits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 949. Given an arrayarr of 4 digits, find the latest 24-hour time that can be made using each digit exactly once.

---

<br />

## Description

LeetCode Problem 949.

Given an arrayarr of 4 digits, find the latest 24-hour time that can be made using each digit exactly once.

24-hour times are formatted as "HH:MM", where HHis between00and23, andMMis between00and59. The earliest 24-hour time is 00:00, and the latest is 23:59.

Return the latest 24-hour timein"HH:MM" format. If no valid time can be made, return an empty string.

Example 1:
```
Input: arr = [1,2,3,4]
Output: "23:41"
Explanation:The valid 24-hour times are "12:34", "12:43", "13:24", "13:42", "14:23", "14:32", "21:34", "21:43", "23:14", and "23:41". Of these times, "23:41" is the latest.
```

Example 2:
```
Input: arr = [5,5,5,5]
Output: ""
Explanation:There are no valid 24-hour times as "55:55" is not valid.
```

Example 3:
```
Input: arr = [0,0,0,0]
Output: "00:00"
```

Example 4:
```
Input: arr = [0,0,1,0]
Output: "10:00"
```

Constraints:
* arr.length == 4
* 0 <= arr[i] <= 9

<br />

## Sample C++ Code


```c
class Solution {
public:
    string largestTimeFromDigits(vector<int>& a) {
        string ans = ""; 
        int mx = -1, h1 = -1, h2 = -1, m1 = -1, m2 = -1;
        for (int i = 0; i < 4; ++i) {
            if (a[i] > 2) continue;
            for (int j = 0; j < 4; ++j) {
                if (j == i) continue;
                if (a[i] == 2 && a[j] > 3) continue;
                for (int k = 0; k < 4; ++k) {
                    if (k == j || k == i) continue;
                    if (a[k] > 5) continue;
                    int l = 6 - i - j - k;
                    if (l == k || l == j || l == i) continue;
                    // value of time in minutes.
                    int val = (a[l] + (a[k] * 10)) + (a[j] + (a[i] * 10)) * 60;
                    if (mx < val) {
                        mx = val;
                        h1 = a[i], h2 = a[j], m1 = a[k], m2 = a[l];
                    }
                }
            }
        }
        if (h1 == -1 || h2 == -1 || m1 == -1 || m2 == -1) 
            return "";
        ans = to_string(h1) + to_string(h2) + ":" + to_string(m1) + to_string(m2);
        return ans;
    }
};
```


