---
layout: post
title: "Minimum Time Difference Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, String, Sorting ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 539. Given a list of 24-hour clock time points in "HH:MM" format, return the minimum minutes difference between any two time-points in the list.

---

<br />

## Description

LeetCode Problem 539.

Given a list of 24-hour clock time points in "HH:MM" format, return the minimum minutes difference between any two time-points in the list.

Example 1:
```
Input: timePoints = ["23:59","00:00"]
Output: 1
```

Example 2:
```
Input: timePoints = ["00:00","23:59","00:00"]
Output: 0
```

Constraints:
* 2 <= timePoints <= 2 * 10^4
* timePoints[i] is in the format "HH:MM".

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findMinDifference(vector<string>& times) {
        int n = times.size();
        sort(times.begin(), times.end());
        int mindiff = INT_MAX;
        for (int i = 0; i < times.size(); i++) {
            int diff = abs(timeDiff(times[(i - 1 + n) % n], times[i]));
            diff = min(diff, 1440 - diff);
            mindiff = min(mindiff, diff);
        }
        return mindiff;
    }

private:
    int timeDiff(string t1, string t2) {
        int h1 = stoi(t1.substr(0, 2));
        int m1 = stoi(t1.substr(3, 2));
        int h2 = stoi(t2.substr(0, 2));
        int m2 = stoi(t2.substr(3, 2));
        return (h2 - h1) * 60 + (m2 - m1);
    }
};
```


