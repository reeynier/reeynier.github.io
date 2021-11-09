---
layout: post
title:  "Permutation Sequence Problem"
categories: [ Algorithm ]
tags: [ Math, Recursion, Leetcode ]
similar: [ Recursion ]
featured: false
hidden: false
excerpt: LeetCode 60. Given n and k, return the kth permutation sequence.
---

<br />

## Description

LeetCode Problem 60. 

The set [1, 2, 3, ..., n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:
```
"123"
"132"
"213"
"231"
"312"
"321"
```

Given n and k, return the kth permutation sequence.

 

Example 1:
```
Input: n = 3, k = 3
Output: "213"
```

Example 2:
```
Input: n = 4, k = 9
Output: "2314"
```

Example 3:
```
Input: n = 3, k = 1
Output: "123"
```
 

Constraints:

* 1 <= n <= 9
* 1 <= k <= n!


<br />

## Sample C++ Code


```c
string getPermutation(int n, int k) {
    // pTable refers to permutation table and numSet refers to a set of numbers from 1 to 9.
    int pTable[10] = {1};
    for (int i = 1; i <= 9; i++){
        pTable[i] = i * pTable[i - 1];
    }
    string result;
    vector<char> numSet{'1', '2', '3', '4', '5', '6', '7', '8', '9'};
    while (n > 0){
        // 1 calculate which number we will use.
        // 2 remove that number from numSet.
        // 3 recalculate k.
        // 4 n--.
        int temp = (k - 1) / pTable[n - 1];
        result += numSet[temp];
        numSet.erase(numSet.begin() + temp);
        k = k - temp * pTable[n - 1];
        n--;
    }
    return result;
}
```
