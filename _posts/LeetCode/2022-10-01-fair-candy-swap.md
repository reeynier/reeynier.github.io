---
layout: post
title: "Fair Candy Swap Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Binary Search, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 888. Alice and Bob have a different total number of candies. You are given two integer arrays aliceSizes and bobSizes where aliceSizes[i] is the number of candies of the i^th box of candy that Alice has and bobSizes[j] is the number of candies of the j^th box of candy that Bob has.

---

<br />

## Description

LeetCode Problem 888.

Alice and Bob have a different total number of candies. You are given two integer arrays aliceSizes and bobSizes where aliceSizes[i] is the number of candies of the i^th box of candy that Alice has and bobSizes[j] is the number of candies of the j^th box of candy that Bob has.

Since they are friends, they would like to exchange one candy box each so that after the exchange, they both have the same total amount of candy. The total amount of candy a person has is the sum of the number of candies in each box they have.

Return an integer array answer where answer[0] is the number of candies in the box that Alice must exchange, and answer[1] is the number of candies in the box that Bob must exchange. If there are multiple answers, you may return any one of them. It is guaranteed that at least one answer exists.

Example 1:
```
Input: aliceSizes = [1,1], bobSizes = [2,2]
Output: [1,2]
```

Example 2:
```
Input: aliceSizes = [1,2], bobSizes = [2,3]
Output: [1,2]
```

Example 3:
```
Input: aliceSizes = [2], bobSizes = [1,3]
Output: [2,3]
```

Example 4:
```
Input: aliceSizes = [1,2,5], bobSizes = [2,4]
Output: [5,4]
```

Constraints:
* 1 <= aliceSizes.length, bobSizes.length <= 10^4
* 1 <= aliceSizes[i], bobSizes[j] <= 10^5
* Alice and Bob have a different total number of candies.
* There will be at least one valid answer for the given input.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) {
        int a = 0, b = 0;
        for (int i = 0; i < A.size(); i++)
            a += A[i];
        for (int i = 0; i < B.size(); i++)
            b += B[i];
        a = (b - a) / 2;
        set<int> s;
        for (auto x : A)
            s.insert(x + a);
        for (auto x : B) {
            if (s.find(x) != s.end())
                return {x - a, x};
        }
        return {};
    }
};
```


