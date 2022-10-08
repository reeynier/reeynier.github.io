---
layout: post
title: "Largest Component Size By Common Factor Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Union Find ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 952. You are given an integer array of unique positive integers nums. Consider the following graph

---

<br />

## Description

LeetCode Problem 952.

You are given an integer array of unique positive integers nums. Consider the following graph:
* There are nums.length nodes, labeled nums[0] to nums[nums.length - 1],
* There is an undirected edge between nums[i] and nums[j] if nums[i] and nums[j] share a common factor greater than 1.

Return the size of the largest connected component in the graph.

Example 1: 
```
Input: nums = [4,6,15,35]
Output: 4
```

Example 2: 
```
Input: nums = [20,50,9,63]
Output: 2
```

Example 3: 
```
Input: nums = [2,3,6,7,4,12,21,39]
Output: 8
```

Constraints:
* 1 <= nums.length <= 2 * 10^4
* 1 <= nums[i] <= 10^5
* All the values of nums are unique.

<br />

## Sample C++ Code using Union Find 


```c
class UnionFindSet {
public:
    UnionFindSet(int n) : _parent(n) {
        for (int i=0; i<n; i++) {
            _parent[i] = i;
        }
    }
    
    void Union(int x, int y) {
        _parent[Find(x)] = _parent[Find(y)];
    }
    
    int Find(int x) {
        if (_parent[x] != x) {
            _parent[x] = Find(_parent[x]);
        }
        return _parent[x];
    }
    
private:
    vector<int> _parent;
};

class Solution {
public:
    int largestComponentSize(vector<int>& A) {
        int n = *max_element(A.begin(), A.end());
        UnionFindSet ufs(n+1);
        for (int &a : A) {
            for (int k = 2; k <= sqrt(a); k++) {
                if (a % k == 0) {
                    ufs.Union(a, k);
                    ufs.Union(a, a / k);
                }
            }
        }
        
        unordered_map<int, int> m;
        int ans = 1;
        for (int &a : A) {
            ans = max(ans, ++m[ufs.Find(a)]);
        }
        return ans;
    }
};
```


