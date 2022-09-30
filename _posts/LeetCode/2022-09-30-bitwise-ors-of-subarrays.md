---
layout: post
title: "Bitwise ORs Of Subarrays Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 898. We have an array arr of non-negative integers.

---

<br />

## Description

LeetCode Problem 898.

We have an array arr of non-negative integers.

For every (contiguous) subarray sub = [arr[i], arr[i + 1], ..., arr[j]] (with i <= j), we take the bitwise OR of all the elements in sub, obtaining a result arr[i] \| arr[i + 1] \| ... \| arr[j].

Return the number of possible results. Results that occur more than once are only counted once in the final answer.

Example 1:
```
Input: arr = [0]
Output: 1
Explanation: There is only one possible result: 0.
```

Example 2:
```
Input: arr = [1,1,2]
Output: 3
Explanation: The possible subarrays are [1], [1], [2], [1, 1], [1, 2], [1, 1, 2].
These yield the results 1, 1, 2, 1, 3, 3.
There are 3 unique values, so the answer is 3.
```

Example 3:
```
Input: arr = [1,2,4]
Output: 6
Explanation: The possible results are 1, 2, 3, 4, 6, and 7.
```

Constraints:
* 1 <= nums.length <= 5 * 10^4
* 0 <= nums[i]<= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int subarrayBitwiseORs(vector<int>& arr) {
        int sz = arr.size();
        unordered_set<int> st;
        for (int i = 0; i < sz; i++) {
            st.insert(arr[i]);
            for (int j = i - 1; j >= 0; j--) {
                if ((arr[i] | arr[j]) == arr[j])
                    break;
                arr[j] |= arr[i];
                st.insert(arr[j]);
            }
        }
        return st.size();
    }
};
```


