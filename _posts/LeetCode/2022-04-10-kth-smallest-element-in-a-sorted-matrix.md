---
layout: post
title: "Kth Smallest Element In A Sorted Matrix Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Sorting, Heap, Matrix ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 378. Given an n x n matrix where each of the rows and columns is sorted in ascending order, return the k^th smallest element in the matrix.

---

<br />

## Description

LeetCode Problem 378.

Given an n x n matrix where each of the rows and columns is sorted in ascending order, return the k^th smallest element in the matrix.

Note that it is the k^th smallest element in the sorted order, not the k^th distinct element.

You must find a solution with a memory complexity better than O(n^2).

Example 1:
```
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8^th smallest number is 13
```

Example 2:
```
Input: matrix = [[-5]], k = 1
Output: -5
```

Constraints:
* n == matrix.length == matrix[i].length
* 1 <= n <= 300
* -10^9 <= matrix[i][j] <= 10^9
* All the rows and columns of matrix are guaranteed to be sorted in non-decreasing order.
* 1 <= k <= n^2

<br />

## Sample C++ Code


```c
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int n = matrix.size();
        
        int left = matrix[0][0], right = matrix[n-1][n-1];
        int mid;
        
        while (left < right) {
            mid = (left + right) / 2;
            int lessthanmid = 0;
            int i = n-1, j = 0;
            while (i >= 0 && j < n) {
                if (matrix[i][j] <= mid) {
                    j ++;
                    lessthanmid += i+1;
                } else {
                    i --;
                }
            }
            if (lessthanmid < k) {
                left = mid + 1;
            } else {
                right = mid;
            }
            
        }
        return left;
        
    }
};
```


