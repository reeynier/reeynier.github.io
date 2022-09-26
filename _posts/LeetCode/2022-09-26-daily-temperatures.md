---
layout: post
title: "Daily Temperatures Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Stack, Monotonic Stack ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 739. Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the i^th day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

---

<br />

## Description

LeetCode Problem 739.

Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the i^th day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

Example 1:
```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

Example 2:
```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```

Example 3:
```
Input: temperatures = [30,60,90]
Output: [1,1,0]
```

Constraints:
* 1 <=temperatures.length <= 10^5
* 30 <=temperatures[i] <= 100

<br />

## Sample C++ Code using Stack


```c
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int len = T.size();
        vector<int> ans(len, 0);
        if (len <= 1)
            return ans;
        
        stack<int> st;
        st.push(0);
        int i = 0, curr;
        
        while (i < T.size() - 1) {
            i ++;
            while ((!st.empty()) && (T[i] > T[st.top()])) {
                curr = st.top();
                ans[curr] = i - curr;
                st.pop();
            }
            st.push(i);
        }
        
        return ans;
        
    }
};
```


