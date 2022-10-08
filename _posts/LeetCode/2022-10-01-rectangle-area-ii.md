---
layout: post
title: "Rectangle Area II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Line Sweep, Segment Tree ]
similar: [ Line Sweep ]
featured: false
hidden: false
excerpt: LeetCode 850. You are given a 2D array of axis-aligned rectangles. Each rectangle[i] = [x_i1, y_i1, x_i2, y_i2] denotes the i^th rectangle where (x_i1, y_i1) are the coordinates of the bottom-left corner, and (x_i2, y_i2) are the coordinates of the top-right corner.

---

<br />

## Description

LeetCode Problem 850.

You are given a 2D array of axis-aligned rectangles. Each rectangle[i] = [x_i1, y_i1, x_i2, y_i2] denotes the i^th rectangle where (x_i1, y_i1) are the coordinates of the bottom-left corner, and (x_i2, y_i2) are the coordinates of the top-right corner.

Calculate the total area covered by all rectangles in the plane. Any area covered by two or more rectangles should only be counted once.

Return the total area. Since the answer may be too large, return it modulo 10^9 + 7.

Example 1: 
```
Input: rectangles = [[0,0,2,2],[1,0,2,3],[1,0,3,1]]
Output: 6
Explanation: A total area of 6 is covered by all three rectangales, as illustrated in the picture.
From (1,1) to (2,2), the green and red rectangles overlap.
From (1,0) to (2,3), all three rectangles overlap.
```

Example 2:
```
Input: rectangles = [[0,0,1000000000,1000000000]]
Output: 49
Explanation: The answer is 10^18 modulo (10^9 + 7), which is 49.
```

Constraints:
* 1 <= rectangles.length <= 200
* rectanges[i].length == 4
* 0 <= x_i1, y_i1, x_i2, y_i2 <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int rectangleArea(vector<vector<int>>& rectangles) {
        // find unique y's so the adjacent y_diff are heights
        // sweep all rectangles along x for each height
        set<int> ys;
        for (auto const & r: rectangles) {
            ys.insert(r[1]);
            ys.insert(r[3]);
        }
        // sort rectangle with x_start
        sort(rectangles.begin(), rectangles.end(), [](auto const & r1, auto const & r2) {
            return r1[0] < r2[0];
        });
        // sweep from bottom to top
        int prev_y= *ys.begin();
        long long res = 0;
        int mod = pow(10, 9) + 7;
        for (auto y: ys) {
            long long height = y - prev_y;
            long long x_start = rectangles.front()[0];
            long long x_end = x_start;
            for (auto const & r: rectangles) {
                // check if r fully occupy in between y and prev_y
                if (r[1] <= prev_y && r[3] >=y) {
                    if (r[0] > x_end) {
                        res += height * (x_end-x_start) % mod;
                        x_start = r[0];
                    }
                    if (r[2] > x_end) {
                        x_end = r[2];
                    }
                }
            }
            res += height * (x_end-x_start) % mod;
            prev_y = y;
        }
        return res % mod;
    }
};
```


