---
layout: post
title: "Binary Watch Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Backtracking, Bit Manipulation ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 401. A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.

---

<br />

## Description

LeetCode Problem 401.

A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.
* For example, the below binary watch reads "4:51".

Given an integer turnedOn which represents the number of LEDs that are currently on, return all possible times the watch could represent. You may return the answer in any order.

The hour must not contain a leading zero.
* For example, "01:00" is not valid. It should be "1:00".
The minute must be consist of two digits and may contain a leading zero.
* For example, "10:2" is not valid. It should be "10:02".

Example 1:
```
Input: turnedOn = 1
Output: ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]
```

Example 2:
```
Input: turnedOn = 9
Output: []
```

Constraints:
* 0 <= turnedOn <= 10

<br />

## Sample C++ Code using Backtracking


```c
class Solution {
    vector<int> hour = {1, 2, 4, 8}, minute = {1, 2, 4, 8, 16, 32};
public:
    vector<string> readBinaryWatch(int num) {
        vector<string> res;
        helper(res, make_pair(0, 0), num, 0);
        return res;
    }
    
    void helper(vector<string>& res, pair<int, int> time, int num, int start_point) {
        if (num == 0) {
            res.push_back(to_string(time.first) +  (time.second < 10 ?  ":0" : ":") + to_string(time.second));
            return;
        }
        for (int i = start_point; i < hour.size() + minute.size(); i ++)
            if (i < hour.size()) {    
                time.first += hour[i];
                if (time.first < 12)     
                    helper(res, time, num - 1, i + 1);     
                time.first -= hour[i];
            } else {     
                time.second += minute[i - hour.size()];
                if (time.second < 60)    
                    helper(res, time, num - 1, i + 1);     
                time.second -= minute[i - hour.size()];
            }
    }
};
```


