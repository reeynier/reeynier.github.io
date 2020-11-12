---
layout: post
title:  "Four Sum II Problem"
categories: [ Algorithm, Solution ]
tags: [ Hash Table ]
featured: false
hidden: true
---

<br />

## Description

Given four lists **A**, **B**, **C**, **D** of integer values, compute how many quadruplets (**i, j, k, l**) there are such that **A[i] + B[j] + C[k] + D[l]** is zero. All **A**, **B**, **C**, **D** have same length of **N**.


Example: 
```
Input:  A = [ 1, 2]
        B = [-2,-1]
        C = [-1, 2]
        D = [ 0, 2]
Output: 2
Explanation: The two tuples are:
1. (0, 0, 0, 1) => A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) => A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

<br />

## Solution

This problem is similar to the [`four sum problem`]({% post_url 2020-11-10-four-sum %}).

#### Brute Force Approach

A simple solution is to use the `brute force` approach. 

We loop through each array to get four different elements (*a*, *b*, *c*, *d*). 
Then we check whether (*a* + *b* + *c* + *d* = 0) is true or not.

If it is true, we increase the total count; otherwise, we keep on searching.

The time complexity of this approach is O(n<sup>4</sup>), 
and the space complexity is O(1).

#### Hash Table Approach

We can use the `hash table` approach similar to the [`two sum problem`]({% post_url 2020-11-09-two-sum %}) to reduce the time complexity.

We first loop through two arrays *A* and *B*. During the iteration, we use a hash table to store the sum of the two elements (one from each array) as a key, and the occurrence of such sum as a value.   

We then loop through the rest two arrays *C* and *D*. We calculate the sum of the two elements (one from each array), and check whether *-sum* exists in the hash table. If so, we add the number of occurrence of *-sum* to the total count; otherwise, we continue the searching.

The time complexity can be reduced to O(n<sup>2</sup>), and the space complexity is O(n<sup>2</sup>).

<br />

## Sample C++ Code
This is a C++ implementation of the two pointer approach.
```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
    int count = 0;
    int len = A.size();
    map<int, int> ht;
    for (int i = 0; i < len; i ++) {
        for (int j = 0; j < len; j ++) {
            int x = A[i] + B[j];
            if (ht.find(x) == ht.end())
                ht[x] = 0;
            ht[x] ++;
        }
    }
    
    for (int i = 0; i < len; i ++) {
        for (int j = 0; j < len; j ++) {
            int x = -(C[i] + D[j]);
            if (ht.find(x) != ht.end())
                count += ht[x];
        }
    }
    return count;
}

int main() {
    vector<int> A = {1, 2};
    vector<int> B = {-2, -1};
    vector<int> C = {-1, 2};
    vector<int> D = {0, 2};
    
    cout << fourSumCount(A, B, C, D) << endl;
}
```
