---
layout: post
title: "Falling Squares Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Segment Tree, Ordered Set ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 699. There are several squares being dropped onto the X-axis of a 2D plane.

---

<br />

## Description

LeetCode Problem 699.

There are several squares being dropped onto the X-axis of a 2D plane.

You are given a 2D integer array positions where positions[i] = [left_i, sideLength_i] represents the i^th square with a side length of sideLength_i that is dropped with its left edge aligned with X-coordinate left_i.

Each square is dropped one at a time from a height above any landed squares. It then falls downward (negative Y direction) until it either lands on the top side of another square or on the X-axis. A square brushing the left/right side of another square does not count as landing on it. Once it lands, it freezes in place and cannot be moved.

After each square is dropped, you must record the height of the current tallest stack of squares.
Return an integer array ans where ans[i] represents the height described above after dropping the i^th square.

Example 1: 
```
Input: positions = [[1,2],[2,3],[6,1]]
Output: [2,5,5]
Explanation:
After the first drop, the tallest stack is square 1 with a height of 2.
After the second drop, the tallest stack is squares 1 and 2 with a height of 5.
After the third drop, the tallest stack is still squares 1 and 2 with a height of 5.
Thus, we return an answer of [2, 5, 5].
```

Example 2:
```
Input: positions = [[100,100],[200,100]]
Output: [100,100]
Explanation:
After the first drop, the tallest stack is square 1 with a height of 100.
After the second drop, the tallest stack is either square 1 or square 2, both with heights of 100.
Thus, we return an answer of [100, 100].
Note that square 2 only brushes the right side of square 1, which does not count as landing on it.
```

Constraints:
* 1 <= positions.length <= 1000
* 1 <= left_i <= 10^8
* 1 <= sideLength_i <= 10^6

<br />

## Sample C++ Code

Brute Force Approach 

```c
class Solution {
public:
    vector<int> fallingSquares(vector<vector<int>>& a) {
        int n = a.size();
        vector<int> ans(n, 0);
        for (int i = 0; i < n; i++) {
            ans[i] = a[i][1];
            int curL = a[i][0];
            int curR = a[i][1] + curL;
            for (int j = 0; j < i; j++) {
                int L = a[j][0];
                int R = L + a[j][1];
                if (curL < R && curR > L) 
                    ans[i] = max(ans[i], a[i][1] + ans[j]);;
            }
        }
        for (int i = 1; i < n; i++) 
            ans[i] = max(ans[i], ans[i-1]);
        return ans;
    }
};
```

TreeMap Approach

```c
class Solution {
public:
    vector<int> fallingSquares(vector<vector<int>>& positions) {
        map<int, vector<int>> invals;
        int n = positions.size();
        vector<int> ht(n, 0);
        int l = positions[0][0], h = positions[0][1];
        ht[0] = h;
        invals[l] = {l+h, h};
        for (int i = 1; i < n; i++) {
            int h = drop(invals, positions[i]);
            ht[i] = max(h, ht[i-1]);
        }
        return ht;
    }
private:
    // return the height of current square
    int drop(map<int, vector<int>>& invals, vector<int>& square) {
        int l = square[0], h = square[1], r = l+h, pre_ht = 0;
        auto low = invals.lower_bound(l), up = invals.lower_bound(r);
        // consider intervals in range [low-1, up) 
        if (low != invals.begin()) low--;
        for (auto it = low; it != up; it++) 
            if (it->second[0] > l) pre_ht = max(pre_ht, it->second[1]);
        // erase overlapping intervals, add current interval and update the interval at low and up-1
        int l1 = low->first, r1 = low->second[0], h1 = low->second[1], r2 = 0, h2 = 0;
        if (up != invals.begin()) {
            up--;
            r2 = up->second[0];
            h2 = up->second[1];
            up++;
        }
        invals.erase(low, up);
        invals[l] = {r, pre_ht+h};
        if (l1 < l) invals[l1] = {min(l, r1), h1};
        if (r2 > r) invals[r] = {r2, h2};
        return pre_ht+h;
    }
};
```

