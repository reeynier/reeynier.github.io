---
layout: post
title: "Maximum Length Of Pair Chain Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Greedy, Sorting ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 646. You are given an array of n pairs pairs where pairs[i] = [left_i, right_i] and left_i < right_i.

---

<br />

## Description

LeetCode Problem 646.

You are given an array of n pairs pairs where pairs[i] = [left_i, right_i] and left_i < right_i.
A pair p2 = [c, d] follows a pair p1 = [a, b] if b < c. A chain of pairs can be formed in this fashion.

Return the length longest chain which can be formed.

You do not need to use up all the given intervals. You can select pairs in any order.

Example 1:
```
Input: pairs = [[1,2],[2,3],[3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4].
```

Example 2:
```
Input: pairs = [[1,2],[7,8],[4,5]]
Output: 3
Explanation: The longest chain is [1,2] -> [4,5] -> [7,8].
```

Constraints:
* n == pairs.length
* 1 <= n <= 1000
* -1000 <= left_i < right_i <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findLongestChain(vector<vector<int>>& pairs) {
        sort(pairs.begin(), pairs.end(), cmp);
        int cnt = 0;
        vector<int>& pair = pairs[0];
        for (int i = 0; i < pairs.size(); i++) {
            if (i == 0 || pairs[i][0] > pair[1]) {
                pair = pairs[i];
                cnt++;
            }
        }
        return cnt;
    }

private:
    static bool cmp(vector<int>& a, vector<int>&b) {
        return a[1] < b[1] || a[1] == b[1] && a[0] < b[0];
    }
};
```


