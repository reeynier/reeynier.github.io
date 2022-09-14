---
layout: post
title: "Largest Divisible Subset Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Dynamic Programming, Sorting ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 368. Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies

---

<br />

## Description

LeetCode Problem 368.

Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:
* answer[i] % answer[j] == 0, or
* answer[j] % answer[i] == 0

If there are multiple solutions, return any of them.

Example 1:
```
Input: nums = [1,2,3]
Output: [1,2]
Explanation: [1,3] is also accepted.
```

Example 2:
```
Input: nums = [1,2,4,8]
Output: [1,2,4,8]
```

Constraints:
* 1 <= nums.length <= 1000
* 1 <= nums[i] <= 2 * 10^9
* All the integers in nums are unique.

<br />

## Sample C++ Code

Dynamic programming approach:
1. We first sort the array so that we only have to check A[i] % A[j] when j < i.
2. The vector dp[i] is the longest subset that satisfies the required conditions and ending at index i. The initial length of any subset is 1.
3. The vector previous_index[i] stores the indices of previously included elements in this subset.
4. For j < i < n, if A[i] % A[j] == 0 and dp[i] < dp[j] + 1, we add A[i] to the subsets that have last element as A[j].

```c
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& A) {
		int n = A.size();

		if(n == 0) return {};

		sort(A.begin(), A.end());

		vector<int> dp(n, 1);
		vector<int> previous_index(n, -1);

		int max_ind = 0; 

		for(int i=1; i<n; i++) {
		   for(int j=0; j<i; j++) {
		       if(A[i]%A[j]==0 and dp[i] < dp[j] + 1) {
		           dp[i] = dp[j]+1;
		           previous_index[i] = j;
		       }
		   }
		   if(dp[i] > dp[max_ind]) {
		       max_ind = i;
		   }
		}
		        
		vector<int> answer;
		int t = max_ind;  
		while(t >= 0) {
		  answer.push_back(A[t]);
		  t = previous_index[t];
		}

		return answer;  
    }
};
```


