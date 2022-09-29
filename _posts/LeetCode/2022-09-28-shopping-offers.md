---
layout: post
title: "Shopping Offers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Backtracking, Bit Manipulation, Memoization, Bitmask ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 638. In LeetCode Store, there are n items to sell. Each item has a price. However, there are some special offers, and a special offer consists of one or more different kinds of items with a sale price.

---

<br />

## Description

LeetCode Problem 638.

In LeetCode Store, there are n items to sell. Each item has a price. However, there are some special offers, and a special offer consists of one or more different kinds of items with a sale price.

You are given an integer array price where price[i] is the price of the i^th item, and an integer array needs where needs[i] is the number of pieces of the i^th item you want to buy.

You are also given an array special where special[i] is of size n + 1 where special[i][j] is the number of pieces of the j^th item in the i^th offer and special[i][n] (i.e., the last integer in the array) is the price of the i^th offer.

Return the lowest price you have to pay for exactly certain items as given, where you could make optimal use of the special offers. You are not allowed to buy more items than you want, even if that would lower the overall price. You could use any of the special offers as many times as you want.

Example 1:
```
Input: price = [2,5], special = [[3,0,5],[1,2,10]], needs = [3,2]
Output: 14
Explanation: There are two kinds of items, A and B. Their prices are $2 and $5 respectively. 
In special offer 1, you can pay $5 for 3A and 0B
In special offer 2, you can pay $10 for 1A and 2B. 
You need to buy 3A and 2B, so you may pay $10 for 1A and 2B (special offer #2), and $4 for 2A.
```

Example 2:
```
Input: price = [2,3,4], special = [[1,1,0,4],[2,2,1,9]], needs = [1,2,1]
Output: 11
Explanation: The price of A is $2, and $3 for B, $4 for C. 
You may pay $4 for 1A and 1B, and $9 for 2A ,2B and 1C. 
You need to buy 1A ,2B and 1C, so you may pay $4 for 1A and 1B (special offer #1), and $3 for 1B, $4 for 1C. 
You cannot add more items, though only $9 for 2A ,2B and 1C.
```

Constraints:
* n == price.length
* n == needs.length
* 1 <= n <= 6
* 0 <= price[i] <= 10
* 0 <= needs[i] <= 10
* 1 <= special.length <= 100
* special[i].length == n + 1
* 0 <= special[i][j] <= 50

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool canconsider(vector<int>& x,vector<int>& needs){
        for (int i = 0; i < needs.size(); i++) {
            if (needs[i] < x[i])
                return false;
        }
        return true;
    }
    
    int shoppingOffersutil(vector<int>& price, vector<vector<int>>& special, vector<int>& needs,map<vector<int>,int>& dp) {
        if (dp.find(needs) != dp.end())
            return dp[needs];
        int restsum = 0;
            for (int j = 0; j < needs.size(); j++)
                restsum += needs[j] * price[j];
        int ans = restsum;
        for (int i = 0; i < special.size(); i++) {
            if (canconsider(special[i], needs) && ans >= special[i][needs.size()]) {
                auto tempneed = needs;
                for (int j = 0; j < needs.size(); j++) {
                    tempneed[j] -= special[i][j];
                }
                ans = min(ans, special[i][needs.size()] + shoppingOffersutil(price, special, tempneed, dp));
            }
        }
        return dp[needs] = ans;
    }
    
    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        map<vector<int>,int> dp;
        return shoppingOffersutil(price, special, needs, dp);
    }
};
```


