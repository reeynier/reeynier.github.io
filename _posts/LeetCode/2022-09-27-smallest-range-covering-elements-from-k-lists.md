---
layout: post
title: "Smallest Range Covering Elements From K Lists Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Greedy, Sliding Window, Sorting, Heap ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 632. You have k lists of sorted integers in non-decreasingorder. Find the smallest range that includes at least one number from each of the k lists.

---

<br />

## Description

LeetCode Problem 632.

You have k lists of sorted integers in non-decreasingorder. Find the smallest range that includes at least one number from each of the k lists.

We define the range [a, b] is smaller than range [c, d] if b - a < d - c or a < c if b - a == d - c.

Example 1:
```
Input: nums = [[4,10,15,24,26],[0,9,12,20],[5,18,22,30]]
Output: [20,24]
Explanation: 
List 1: [4, 10, 15, 24,26], 24 is in range [20,24].
List 2: [0, 9, 12, 20], 20 is in range [20,24].
List 3: [5, 18, 22, 30], 22 is in range [20,24].
```

Example 2:
```
Input: nums = [[1,2,3],[1,2,3],[1,2,3]]
Output: [1,1]
```

Example 3:
```
Input: nums = [[10,10],[11,11]]
Output: [10,11]
```

Example 4:
```
Input: nums = [[10],[11]]
Output: [10,11]
```

Example 5:
```
Input: nums = [[1],[2],[3],[4],[5],[6],[7]]
Output: [1,7]
```

Constraints:
* nums.length == k
* 1 <= k <= 3500
* 1 <= nums[i].length <= 50
* -10^5 <= nums[i][j] <= 10^5
* nums[i]is sorted in non-decreasing order.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> smallestRange(vector<vector<int>>& nums) {
        typedef vector<int>::iterator vi;
        
        struct comp {
            bool operator()(pair<vi, vi> p1, pair<vi, vi> p2) {
                return *p1.first > *p2.first;
            }
        };
        
        int lo = INT_MAX, hi = INT_MIN;
        priority_queue<pair<vi, vi>, vector<pair<vi, vi>>, comp> pq;
        for (auto &row : nums) {
            lo = min(lo, row[0]);
            hi = max(hi, row[0]);
            pq.push({row.begin(), row.end()});
        }
        
        vector<int> ans = {lo, hi};
        while (true) {
            auto p = pq.top();
            pq.pop();
            ++p.first;
            if (p.first == p.second)
                break;
            pq.push(p);
            
            lo = *pq.top().first;
            hi = max(hi, *p.first);
            if (hi - lo < ans[1] - ans[0])
                ans = {lo, hi};
        }
        return ans;
    }
};
```


