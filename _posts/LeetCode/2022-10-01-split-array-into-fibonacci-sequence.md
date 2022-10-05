---
layout: post
title: "Split Array Into Fibonacci Sequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Backtracking ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 842. You are given a string of digits num, such as "123456579". We can split it into a Fibonacci-like sequence [123, 456, 579].

---

<br />

## Description

LeetCode Problem 842.

You are given a string of digits num, such as "123456579". We can split it into a Fibonacci-like sequence [123, 456, 579].

Formally, a Fibonacci-like sequence is a list f of non-negative integers such that:
* 0 <= f[i] < 2^31, (that is, each integer fits in a 32-bit signed integer type),
* f.length >= 3, and
* f[i] + f[i + 1] == f[i + 2] for all 0 <= i < f.length - 2.

Note that when splitting the string into pieces, each piece must not have extra leading zeroes, except if the piece is the number 0 itself.

Return any Fibonacci-like sequence split from num, or return [] if it cannot be done.

Example 1:
```
Input: num = "123456579"
Output: [123,456,579]
```

Example 2:
```
Input: num = "11235813"
Output: [1,1,2,3,5,8,13]
```

Example 3:
```
Input: num = "112358130"
Output: []
Explanation: The task is impossible.
```

Example 4:
```
Input: num = "0123"
Output: []
Explanation: Leading zeroes are not allowed, so "01", "2", "3" is not valid.
```

Example 5:
```
Input: num = "1101111"
Output: [11,0,11,11]
Explanation: The output [11, 0, 11, 11] would also be accepted.
```

Constraints:
* 1 <= num.length <= 200
* num contains only digits.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> ans;
    string origS;
    
    void backtrack(vector<int>& seq, int idx) {
        int len = seq.size();

        if (idx == origS.size() && len >= 3 && 
           seq[len-1] == seq[len-2]+seq[len-3]) {
            ans = seq;
        }
        if (idx >= origS.size())
            return;
        
        long long num = 0;
        for (int i = idx; i < origS.size(); i ++) {
            num = num * 10 + origS[i] - '0';
            if (num > INT_MAX) break;
            if (origS[idx] == '0' && i > idx) break;
            if (len >= 2) {
                if (num == (unsigned)(seq[len-1]) + (unsigned)(seq[len-2])) {
                    seq.push_back(num);
                    backtrack(seq, i+1);
                    seq.pop_back();
                } else if (num > (unsigned)(seq[len-1]) + (unsigned)(seq[len-2])) {
                    break;
                }
            } else {
                seq.push_back(num);
                backtrack(seq, i+1);
                seq.pop_back();
            }
        }
    }
    
    vector<int> splitIntoFibonacci(string S) {
        origS = S;
        vector<int> seq;
        backtrack(seq, 0);
        return ans;
    }
};
```


