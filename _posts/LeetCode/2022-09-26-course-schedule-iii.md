---
layout: post
title: "Course Schedule III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Greedy, Heap ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 630. There are n different online courses numbered from 1 to n. You are given an array courses where courses[i] = [duration_i, lastDay_i] indicate that the i^th course should be taken continuously for duration_i days and must be finished before or on lastDay_i.

---

<br />

## Description

LeetCode Problem 630.

There are n different online courses numbered from 1 to n. You are given an array courses where courses[i] = [duration_i, lastDay_i] indicate that the i^th course should be taken continuously for duration_i days and must be finished before or on lastDay_i.

You will start on the 1^st day and you cannot take two or more courses simultaneously.

Return the maximum number of courses that you can take.

Example 1:
```
Input: courses = [[100,200],[200,1300],[1000,1250],[2000,3200]]
Output: 3
Explanation: 
There are totally 4 courses, but you can take 3 courses at most:
First, take the 1^st course, it costs 100 days so you will finish it on the 100^th day, and ready to take the next course on the 101^st day.
Second, take the 3^rd course, it costs 1000 days so you will finish it on the 1100^th day, and ready to take the next course on the 1101^st day. 
Third, take the 2^nd course, it costs 200 days so you will finish it on the 1300^th day. 
The 4^th course cannot be taken now, since you will finish it on the 3300^th day, which exceeds the closed date.
```

Example 2:
```
Input: courses = [[1,2]]
Output: 1
```

Example 3:
```
Input: courses = [[3,2],[4,3]]
Output: 0
```

Constraints:
* 1 <= courses.length <= 10^4
* 1 <= duration_i, lastDay_i <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int scheduleCourse(vector<vector<int>>& courses) {
        if (courses.size() <= 0) 
            return 0;
        sort(courses.begin(), courses.end(), [](const vector<int>& a, vector<int>& b) {
            return a[1] < b[1];
        });
        priority_queue<int> q;
        int sum = 0;
        for (auto i : courses) {
            sum += i[0];
            q.push(i[0]);
            if (sum > i[1]) {
                sum -= q.top();
                q.pop();
            }
        }
        return q.size();
    }
};
```


