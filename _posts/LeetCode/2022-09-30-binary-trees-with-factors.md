---
layout: post
title: "Binary Trees With Factors Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Dynamic Programming ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 823. Given an array of unique integers, arr, where each integer arr[i] is strictly greater than 1.

---

<br />

## Description

LeetCode Problem 823.

Given an array of unique integers, arr, where each integer arr[i] is strictly greater than 1.

We make a binary tree using these integers, and each number may be used for any number of times. Each non-leaf node's value should be equal to the product of the values of its children.

Return the number of binary trees we can make. The answer may be too large so return the answer modulo 10^9 + 7.

Example 1:
```
Input: arr = [2,4]
Output: 3
Explanation: We can make these trees: [2], [4], [4, 2, 2]
```

Example 2:
```
Input: arr = [2,4,5,10]
Output: 7
Explanation: We can make these trees: [2], [4], [5], [10], [4, 2, 2], [10, 2, 5], [10, 5, 2].
```

Constraints:
* 1 <= arr.length <= 1000
* 2 <= arr[i] <= 10^9
* All the values of arr are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int numFactoredBinaryTrees(vector<int>& arr) {
        int size_ = arr.size();
        unordered_map<int, unsigned long long> um;
        int total = 0;
        int mod = 1000000007;
        sort(arr.begin(), arr.end());
        for (int i = 0; i < size_; i++) {
            int curr = arr[i];
            um[curr] = 1;
            for (int j = 0; j < i; j++) {
                if (arr[i] % arr[j] == 0) {
                    int a = arr[j];
                    int b = arr[i] / arr[j];
                    if (a > b) {
                        break;
                    }
                    else if (a == b) {
                        um[curr] += um[a] * um[a];
                    }
                    else if (um.count(b)) {
                        um[curr] += 2 * um[a] * um[b];
                    }
                }
            }
            total = (total + um[curr]) % mod;
        }
        return total;
    }
};
```


