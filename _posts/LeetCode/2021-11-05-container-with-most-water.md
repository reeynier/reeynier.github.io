---
layout: post
title:  "Container With Most Water Problem"
categories: [ Algorithm ]
tags: [ Greedy, Two Pointers, Leetcode ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 11. Given n non-negative integers a_1, a_2, ..., a_n , where each represents a point at coordinate
---

<br />

## Description

LeetCode Problem 11. 

Given n non-negative integers a_1, a_2, ..., a_n , where each represents a point at coordinate (i, a_i). n vertical lines are drawn such that the two endpoints of the line i is at (i, a_i) and (i, 0). Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

Notice that you may not slant the container.

 

Example 1:
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
```

Example 2:
```
Input: height = [1,1]
Output: 1
```

Example 3:
```
Input: height = [4,3,2,1,4]
Output: 16
```

Example 4:
```
Input: height = [1,2,1]
Output: 2
```

Constraints:

* n == height.length
* 2 <= n <= 10^5
* 0 <= height[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int area = 0, max_area = 0;
        int l = 0, r = n-1;
        
        while (l < r) {
            area = (r - l) * min(height[l], height[r]);
            max_area = max(max_area, area);
            
            if (height[l] < height[r])
                l ++;
            else
                r --;
        }
        return max_area;
    }
};
```
