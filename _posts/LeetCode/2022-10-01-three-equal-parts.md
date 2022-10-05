---
layout: post
title: "Three Equal Parts Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 927. You are given an array arr which consists of only zeros and ones, divide the array into three non-empty parts such that all of these parts represent the same binary value.

---

<br />

## Description

LeetCode Problem 927.

You are given an array arr which consists of only zeros and ones, divide the array into three non-empty parts such that all of these parts represent the same binary value.

If it is possible, return any [i, j] with i + 1 < j, such that:
* arr[0], arr[1], ..., arr[i] is the first part,
* arr[i + 1], arr[i + 2], ..., arr[j - 1] is the second part, and
* arr[j], arr[j + 1], ..., arr[arr.length - 1] is the third part.
* All three parts have equal binary values.

If it is not possible, return [-1, -1].

Note that the entire part is used when considering what binary value it represents. For example, [1,1,0] represents 6 in decimal, not 3. Also, leading zeros are allowed, so [0,1,1] and [1,1] represent the same value.

Example 1:
```
Input: arr = [1,0,1,0,1]
Output: [0,3]
```

Example 2:
```
Input: arr = [1,1,0,1,1]
Output: [-1,-1]
```

Example 3:
```
Input: arr = [1,1,0,0,1]
Output: [0,2]
```

Constraints:
* 3 <= arr.length <= 3 * 10^4
* arr[i] is 0 or 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> threeEqualParts(vector<int>& A) {
        vector<int> dp;
        for (int i = 0 ; i < A.size(); i++) 
            // this loop is used to store the index of all 1s
            if (A[i]) 
                dp.push_back(i);
            
        if (dp.size() % 3) 
            // if the number of 1s cannot be devided perfectly by 3, the input is invalid
            return {-1, -1}; 
        
	    if (dp.empty()) 
            // if the number of 1 is zero, then it is natually valid, return {0, 2}
            return {0,2}; 
        
        //if we want to devide into 3 parts, the distribution pattern of 1s in three parts should be the same
        int l1 = 0, l2 = dp.size() / 3, l3 = l2 * 2; 
        for (int i = 1; i < l2; i++ ) {
            int diff = dp[i] - dp[i-1];
            if (dp[l2+i] - dp[l2+i-1] != diff || dp[l3+i] - dp[l3+i-1] != diff) 
                //unmatched pattern
                return {-1, -1};
	    }
        
        // calculate how many 0s tail
        int tail0 = A.size() - dp.back(); 
        if (dp[l3] - dp[l3-1] < tail0 ||   dp[l2] - dp[l2-1] < tail0) 
            // all three parts should tail with the same number of 0s with that in the last part
            return {-1,-1};
        
        return {dp[l2-1] + tail0 - 1, dp[l3-1] + tail0};
    }
};
```


