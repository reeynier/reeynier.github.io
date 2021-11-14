---
layout: post
title:  "Restore IP Addresses Problem"
categories: [ Algorithm ]
tags: [ String, Backtracking, Leetcode ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 93. Given a string s containing only digits, return all possible valid IP addresses that can be obtained from s.
---

<br />

## Description

LeetCode Problem 93. 

Given a string s containing only digits, return all possible valid IP addresses that can be obtained from s. You can return them in any order.

A valid IP address consists of exactly four integers, each integer is between 0 and 255, separated by single dots and cannot have leading zeros. For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses and "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses. 

 

Example 1:
```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```

Example 2:
```
Input: s = "0000"
Output: ["0.0.0.0"]
```

Example 3:
```
Input: s = "1111"
Output: ["1.1.1.1"]
```

Example 4:
```
Input: s = "010010"
Output: ["0.10.0.10","0.100.1.0"]
```

Example 5:
```
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

Constraints:

* 0 <= s.length <= 20
* s consists of digits only.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> ans;
    string origS;
    
    void backtrack(vector<int>& address, int idx) {
        if (address.size() == 4 && idx == origS.size()) {
            string S = to_string(address[0]) + "." + 
                to_string(address[1]) + "." + to_string(address[2]) +
                "." + to_string(address[3]);
            ans.push_back(S);
        }
        if (address.size() >= 4 || idx >= origS.size())
            return;
        
        int num = 0;
        for (int i = idx; i < origS.size(); i ++) {
            num = num * 10 + origS[i] - '0';
            if (origS[idx] == '0' && i > idx)
                break; 
            if (num <= 255) {
                address.push_back(num);
                backtrack(address, i+1);
                address.pop_back();
            } else {
                break;
            }
        }
    }
    
    vector<string> restoreIpAddresses(string s) {
        origS = s;
        vector<int> address;
        backtrack(address, 0);
        return ans;
    }
};
```
