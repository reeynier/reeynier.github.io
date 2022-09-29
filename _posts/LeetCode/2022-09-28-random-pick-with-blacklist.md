---
layout: post
title: "Random Pick With Blacklist Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, Binary Search, Sorting, Randomized ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 710. You are given an integer n and an array of unique integers blacklist. Design an algorithm to pick a random integer in the range [0, n - 1] that is not in blacklist. Any integer that is in the mentioned range and not in blacklist should be equally likely to be returned.

---

<br />

## Description

LeetCode Problem 710.

You are given an integer n and an array of unique integers blacklist. Design an algorithm to pick a random integer in the range [0, n - 1] that is not in blacklist. Any integer that is in the mentioned range and not in blacklist should be equally likely to be returned.

Optimize your algorithm such that it minimizes the number of calls to the built-in random function of your language.

Implement the Solution class:
* Solution(int n, int[] blacklist) Initializes the object with the integer n and the blacklisted integers blacklist.
* int pick() Returns a random integer in the range [0, n - 1] and not in blacklist.

Example 1:
```
Input
["Solution", "pick", "pick", "pick", "pick", "pick", "pick", "pick"]
[[7, [2, 3, 5]], [], [], [], [], [], [], []]
Output
[null, 0, 4, 1, 6, 1, 0, 4]
Explanation
Solution solution = new Solution(7, [2, 3, 5]);
solution.pick(); // return 0, any integer from [0,1,4,6] should be ok. Note that for every call of pick,
// 0, 1, 4, and 6 must be equally likely to be returned (i.e., with probability 1/4).
solution.pick(); // return 4
solution.pick(); // return 1
solution.pick(); // return 6
solution.pick(); // return 1
solution.pick(); // return 0
solution.pick(); // return 4
```

Constraints:
* 1 <= n <= 10^9
* 0 <= blacklist.length <- min(10^5, n - 1)
* 0 <= blacklist[i] < n
* All the values of blacklist are unique.
* At most 2 * 10^4 calls will be made to pick.

<br />

## Sample C++ Code using Binary Search 


```c
class Solution {
private:
    int N;
    int b;
    vector<int> blackList;
public:
    Solution(int N, vector<int>& blacklist) : b(blacklist.size()), N(N), blackList(blacklist) {
        sort(blackList.begin(), blackList.end());
    }
    
    int pick() {
        int k = rand() % (N - b);
        if (b == 0)
            return k;
        if (blackList[0] > k)
            return k;
        int start = 0, end = b - 1;
        while (start <= end) {
            int mid = (start + end) / 2;
            int wc = blackList[mid] - mid;
            if (wc <= k && (mid == b - 1 || mid != b - 1 && blackList[mid+1] - mid - 1 > k)) {
                return k + 1 - wc + blackList[mid];
            } else if (wc > k) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return -1;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(N, blacklist);
 * int param_1 = obj->pick();
 */
```


