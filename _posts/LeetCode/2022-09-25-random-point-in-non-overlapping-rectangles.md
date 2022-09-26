---
layout: post
title: "Random Point In Non-Overlapping Rectangles Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Binary Search, Prefix Sum, Ordered Set, Randomized ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 497. You are given an array of non-overlapping axis-aligned rectangles rects where rects[i] = [a_i, b_i, x_i, y_i] indicates that (a_i, b_i) is the bottom-left corner point of the i^th rectangle and (x_i, y_i) is the top-right corner point of the i^th rectangle. Design an algorithm to pick a random integer point inside the space covered by one of the given rectangles. A point on the perimeter of a rectangle is included in the space covered by the rectangle.

---

<br />

## Description

LeetCode Problem 497.

You are given an array of non-overlapping axis-aligned rectangles rects where rects[i] = [a_i, b_i, x_i, y_i] indicates that (a_i, b_i) is the bottom-left corner point of the i^th rectangle and (x_i, y_i) is the top-right corner point of the i^th rectangle. Design an algorithm to pick a random integer point inside the space covered by one of the given rectangles. A point on the perimeter of a rectangle is included in the space covered by the rectangle.

Any integer point inside the space covered by one of the given rectangles should be equally likely to be returned.

Note that an integer point is a point that has integer coordinates.

Implement the Solution class:
* Solution(int[][] rects) Initializes the object with the given rectangles rects.
* int[] pick() Returns a random integer point [u, v] inside the space covered by one of the given rectangles.

Example 1: 
```
Input
["Solution", "pick", "pick", "pick", "pick", "pick"]
[[[[-2, -2, 1, 1], [2, 2, 4, 6]]], [], [], [], [], []]
Output
[null, [1, -2], [1, -1], [-1, -2], [-2, -2], [0, 0]]
Explanation
Solution solution = new Solution([[-2, -2, 1, 1], [2, 2, 4, 6]]);
solution.pick(); // return [1, -2]
solution.pick(); // return [1, -1]
solution.pick(); // return [-1, -2]
solution.pick(); // return [-2, -2]
solution.pick(); // return [0, 0]
```

Constraints:
* 1 <= rects.length <= 100
* rects[i].length == 4
* -10^9 <= a_i < x_i <= 10^9
* -10^9 <= b_i < y_i <= 10^9
* x_i - a_i <= 2000
* y_i - b_i <= 2000
* All the rectangles do not overlap.
* At most 10^4 calls will be made to pick.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> v;
    vector<vector<int>> rects;
    
    int area(vector<int>& r) {
        return (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
    }
    
    Solution(vector<vector<int>> _) {
        rects = _;
        for (auto& r : rects) {
            v.push_back(area(r) + (v.empty() ? 0 : v.back()));
        }
    }
    
    vector<int> pick() {
        // First pick a random rectangle with a weight of their areas.
        int rnd = rand() % v.back();
        auto it = upper_bound(v.begin(), v.end(), rnd);
        int idx = it - v.begin();
        
        // pick a random point in rect[idx]
        auto r = rects[idx];
        return {
            rand() % (r[2] - r[0] + 1) + r[0],
            rand() % (r[3] - r[1] + 1) + r[1]
        };
    }
};
/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(rects);
 * vector<int> param_1 = obj->pick();
 */
```


