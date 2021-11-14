---
layout: post
title:  "Largest Rectangle in Histogram Problem"
categories: [ Algorithm ]
tags: [ Array, Stack, Leetcode ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 84. Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.
---

<br />

## Description

LeetCode Problem 84. 

Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

 

Example 1:
```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

Example 2:
```
Input: heights = [2,4]
Output: 4
```

Constraints:

* 1 <= heights.length <= 10^5
* 0 <= heights[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int largestRectangleArea(vector<int>& hist) {
        int n = hist.size();
        int max_area = 0, area;
        int i = 0, tp;
        stack<int> s;
        
        while (i < n) {
            if (s.empty() || hist[s.top()] <= hist[i]) {
                s.push(i);
                i ++;
            } else {
                tp = s.top();
                s.pop();
                area = hist[tp] * (s.empty() ? i : i - s.top() - 1);
                if (area > max_area)
                    max_area = area;
            }
        }
        
        while (!s.empty()) {
            tp = s.top();
            s.pop();
            area = hist[tp] * (s.empty() ? i : i - s.top() - 1);
            if (area > max_area)
                max_area = area;
        }
        return max_area;
    }
};
```
