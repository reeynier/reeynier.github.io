---
layout: post
title:  "Merge Intervals Problem"
categories: [ Algorithm ]
tags: [ Sort, Leetcode ]
similar: [ Sort ]
featured: false
hidden: false
excerpt: LeetCode 56. Given an array of intervals, merge all overlapping intervals.
---

<br />

## Description

LeetCode Problem 56. Given an array of **intervals** where **intervals[i] = [start_i, end_i]**, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example: 
```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

<br />

## Solution

To merge the intervals, we first need to sort them so that the beginnings of the intervals are in the ascending order. Then it is easier for us to merge the intervals.

Suppose we have two intervals, [beg1, end1] and [beg2, end2]. 

If (end1 >= beg2), the two intervals can be merged. The merged interval will be in the range: (min(beg1, beg2), max(end1, end2)).

If (end1 < beg2), these two intervals will not be merged. As the array of intervals has already been sorted, we will be safe to say that the first interval will not be merged with latter intervals. Thus, we can push the first interval into the resulting array.

We iterate through the array of intervals. For each interval, we iterate through the rest of the array. We merge the intervals until no more merges can be done. Then we push the final merged interval to the resulting array.

<br />

## Sample C++ Code


This is a C++ implementation of the above approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<vector<int>> merge(vector<vector<int>>& intervals) {
    int n = intervals.size();
    if (n == 0) return intervals;
  
    sort(intervals.begin(), intervals.end());
  
    vector<vector<int>> ans;
    int idx = 0;
    int beg = intervals[idx][0], end = intervals[idx][1];
    int nextb, nexte;
  
    while (idx < n-1) {
        idx ++;
        nextb = intervals[idx][0], nexte = intervals[idx][1];
        if (end >= nextb) {
            beg = min(beg, nextb);
            end = max(end, nexte);
        }
        else {
            ans.push_back({beg, end});
            beg = nextb, end = nexte;
        }
    }

    ans.push_back({beg, end});
    return ans;
}

int main() {
    vector<vector<int>> intervals = {
        {1,3}, {2,6}, {8,10}, {15,18}
    };
    vector<vector<int>> ans;
    ans = merge(intervals);
    for (int i = 0; i < ans.size(); i ++) {
        cout << ans[i][0] << " " << ans[i][1] << endl;
    }
}
```
