---
layout: post
title: "Set Intersection Size At Least Two Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Greedy, Sorting ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 757. You are given a 2D integer array intervals where intervals[i] = [start_i, end_i] represents all the integers from starti to endi inclusively.

---

<br />

## Description

LeetCode Problem 757.

You are given a 2D integer array intervals where intervals[i] = [start_i, end_i] represents all the integers from starti to endi inclusively.

A containing set is an array nums where each interval from intervals has at least two integers in nums.

For example, if intervals = [[1,3], [3,7], [8,9]], then [1,2,4,7,8,9] and [2,3,4,8,9] are containing sets.

Return the minimum possible size of a containing set.

Example 1:
```
Input: intervals = [[1,3],[3,7],[8,9]]
Output: 5
Explanation: let nums = [2, 3, 4, 8, 9].
It can be shown that there cannot be any containing array of size 4.
```

Example 2:
```
Input: intervals = [[1,3],[1,4],[2,5],[3,5]]
Output: 3
Explanation: let nums = [2, 3, 4].
It can be shown that there cannot be any containing array of size 2.
```

Example 3:
```
Input: intervals = [[1,2],[2,3],[2,4],[4,5]]
Output: 5
Explanation: let nums = [1, 2, 3, 4, 5].
It can be shown that there cannot be any containing array of size 4.
```

Constraints:
* 1 <= intervals.length <= 3000
* intervals[i].length == 2
* 0 <= start_i < end_i <= 10^8

<br />

## Sample C++ Code


```c
class Solution {
public:
    int intersectionSizeTwo(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [](vector<int>& a, vector<int>& b) {
            return a[1] < b[1] || (a[1] == b[1] && a[0] > b[0]); 
        });
        
        int n = intervals.size(), ans = 0, p1 = -1, p2 = -1;
        
        for (int i = 0; i < n; i++) {
            // current p1, p2 works for intervals[i]
            if (intervals[i][0] <= p1) 
                continue;
            
            // Neither of p1, p2 works for intervals[i]
            // replace p1, p2 by ending numbers
            if (intervals[i][0] > p2) {
                ans += 2;
                p2 = intervals[i][1];
                p1 = p2-1;
            }
            
            // only p2 works;  
            else {
                ans++;
                p1 = p2;
                p2 = intervals[i][1];
            }
        }
        
        return ans;
    }
};
```


