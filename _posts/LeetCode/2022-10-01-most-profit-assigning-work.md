---
layout: post
title: "Most Profit Assigning Work Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, Binary Search, Greedy, Sorting ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 826. You have n jobs and m workers. You are given three arrays, difficulty, profit, and worker where

---

<br />

## Description

LeetCode Problem 826.

You have n jobs and m workers. You are given three arrays: difficulty, profit, and worker where:
* difficulty[i] and profit[i] are the difficulty and the profit of the i^th job, and
* worker[j] is the ability of j^th worker (i.e., the j^th worker can only complete a job with difficulty at most worker[j]).

Every worker can be assigned at most one job, but one job can be completed multiple times.
* For example, if three workers attempt the same job that pays $1, then the total profit will be $3. If a worker cannot complete any job, their profit is $0.

Return the maximum profit we can achieve after assigning the workers to the jobs.

Example 1:
```
Input: difficulty = [2,4,6,8,10], profit = [10,20,30,40,50], worker = [4,5,6,7]
Output: 100
Explanation: Workers are assigned jobs of difficulty [4,4,6,6] and they get a profit of [20,20,30,30] separately.
```

Example 2:
```
Input: difficulty = [85,47,57], profit = [24,66,99], worker = [40,25,25]
Output: 0
```

Constraints:
* n == difficulty.length
* n == profit.length
* m == worker.length
* 1 <= n, m <= 10^4
* 1 <= difficulty[i], profit[i], worker[i] <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxProfitAssignment(vector<int>& difficulty, vector<int>& profit, vector<int>& worker) {
        vector<pair<int,int>> vc;
        for (int i = 0; i < difficulty.size(); i++) 
            vc.push_back(make_pair(difficulty[i], profit[i]));   
        sort(vc.begin(), vc.end());
        for (int i = 1; i < vc.size(); i++) 
            vc[i].second = max(vc[i].second, vc[i - 1].second);
         
        sort(worker.begin(), worker.end());
        int  x = 0, ans = 0;
        for (int i = 0; i < worker.size(); i++) {
            while (vc[x].first <= worker[i] && vc.size() > x) {
                x++;
            }
            ans += x == 0 ? 0 : vc[x - 1].second;
        }
        return ans;
    }
};
```


