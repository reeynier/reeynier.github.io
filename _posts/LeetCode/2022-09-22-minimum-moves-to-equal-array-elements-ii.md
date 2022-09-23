---
layout: post
title: "Minimum Moves To Equal Array Elements II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Sorting ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 462. Given an integer array nums of size n, return the minimum number of moves required to make all array elements equal.

---

<br />

## Description

LeetCode Problem 462.

Given an integer array nums of size n, return the minimum number of moves required to make all array elements equal.

In one move, you can increment or decrement an element of the array by 1.

Test cases are designed so that the answer will fit in a 32-bit integer.

Example 1:
```
Input: nums = [1,2,3]
Output: 2
Explanation:
Only two moves are needed (remember each move increments or decrements one element):
[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```

Example 2:
```
Input: nums = [1,10,2,9]
Output: 16
```

Constraints:
* n == nums.length
* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

<br />

## Sample C++ Code

To get minimum number of moves to make all elements equal, we should move all elements to the median value. 

Suppose we have three numbers [1, 4, 10]. If we move all elements to min, which is 1, the number of moves are (1 - 1) + (4 - 1) + (10 - 1) = 12. If we move all elements to max, which is 10, the number of moves are (10 - 1) + (10 - 4) + (10 - 10) = 15. If we move all elements to the middle number, which is 4, the number of moves are (4 - 1) + (4 - 4) + (10 - 4) = 9. We can observe that moving the min and max elements to any value between [min, max] will cost (max - min) moves. The total number of moves is the (max - min) + (median_value - target_number). If the target_number is the median value, the number of moves is the minimum. If the target number is outside of [min, max], the number of moves is even larger.

Now we could add two more numbers in between 1 and 10, say the array is [1, 2, 4, 6, 10]. We can easily get that moving all elements to 4 is the best answer. The number of moves is (10 - 1) + (6 - 2) + (4 - 4) = 13, which is the (old_max - old_min) + (new_max - new_min).

If the number of elements is even, moving to either median value gives us the same results.


```c
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        int n = nums.size ();
        sort (nums.begin(), nums.end());
        int mid = n/2, i = 0, count = 0;
        for (i = 0; i < n; i++)
            count += abs (nums [i] - nums [mid]);
        return count;
    }
};
```


