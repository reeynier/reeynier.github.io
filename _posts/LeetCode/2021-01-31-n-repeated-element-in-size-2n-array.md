---
layout: post
title:  "N-Repeated Element In Size 2N Array Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 961. In a array A of size 2N, there are N+1 unique elements, and exactly one of these elements is repeated N times.
---

<br />

## Description

LeetCode Problem 961. 

In a array A of size 2N, there are N+1 unique elements, and exactly one of these elements is repeated N times.

Return the element repeated N times.

Example 1:

```
Input: [1,2,3,3]
Output: 3
```

Example 2:

```
Input: [2,1,2,5,3,2]
Output: 2
```

Example 3:

```
Input: [5,1,5,2,5,3,5,4]
Output: 5
```


<br />

## Sample C++ Code


This is a C++ solution using a `hash table`. The time complexity is O(n), and the space complexity is O(n).

```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

int repeatedNTimes(vector<int>& A) {
    int len = A.size();
    int n = len / 2;
    map<int, int> ht;
    for (int i = 0; i < len; i ++) {
        if (ht.find(A[i]) == ht.end())
            ht[A[i]] = 0;
        ht[A[i]] ++;
        if (ht[A[i]] > 1)
            return A[i];
    }
    return ht[A[len-1]];
}

int main() {
    vector<int> A = {1, 2, 3, 3};
    cout << repeatedNTimes(A) << endl;
}
```
