---
layout: post
title: "Summary Ranges Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 228. You are given a sorted unique integer array nums.

---

<br />

## Description

LeetCode Problem 228.

You are given a sorted unique integer array nums.

Return the smallest sorted list of ranges that cover all the numbers in the array exactly. That is, each element of nums is covered by exactly one of the ranges, and there is no integer x such that x is in one of the ranges but not in nums.

Each range [a,b] in the list should be output as:
* "a->b" if a != b
* "a" if a == b

Example 1:
```
Input: nums = [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: The ranges are:
[0,2] --> "0->2"
[4,5] --> "4->5"
[7,7] --> "7"
```

Example 2:
```
Input: nums = [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: The ranges are:
[0,0] --> "0"
[2,4] --> "2->4"
[6,6] --> "6"
[8,9] --> "8->9"
```

Example 3:
```
Input: nums = []
Output: []
```

Example 4:
```
Input: nums = [-1]
Output: ["-1"]
```

Example 5:
```
Input: nums = [0]
Output: ["0"]
```

Constraints:
* 0 <= nums.length <= 20
* -2^31 <= nums[i] <= 2^31 - 1
* All the values of nums are unique.
* nums is sorted in ascending order.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        const int size_n = nums.size();
        vector<string> res;
        if ( 0 == size_n) return res;
        for (int i = 0; i < size_n;) {
            int start = i, end = i;
            while (end + 1 < size_n && nums[end+1] == nums[end] + 1) 
                end++;
            if (end > start) 
                res.push_back(to_string(nums[start]) + "->" + to_string(nums[end]));
            else 
                res.push_back(to_string(nums[start]));
            i = end + 1;
        }
        return res;
    }
};
```


