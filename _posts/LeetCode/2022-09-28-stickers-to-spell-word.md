---
layout: post
title: "Stickers To Spell Word Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String, Dynamic Programming, Backtracking, Bit Manipulation, Bitmask ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 691. We are given n different types of stickers. Each sticker has a lowercase English word on it.

---

<br />

## Description

LeetCode Problem 691.

We are given n different types of stickers. Each sticker has a lowercase English word on it.

You would like to spell out the given string target by cutting individual letters from your collection of stickers and rearranging them. You can use each sticker more than once if you want, and you have infinite quantities of each sticker.

Return the minimum number of stickers that you need to spell out target. If the task is impossible, return -1.

Note: In all test cases, all words were chosen randomly from the 1000 most common US English words, and target was chosen as a concatenation of two random words.

Example 1:
```
Input: stickers = ["with","example","science"], target = "thehat"
Output: 3
Explanation:
We can use 2 "with" stickers, and 1 "example" sticker.
After cutting and rearrange the letters of those stickers, we can form the target "thehat".
Also, this is the minimum number of stickers necessary to form the target string.
```

Example 2:
```
Input: stickers = ["notice","possible"], target = "basicbasic"
Output: -1
Explanation:
We cannot form the target "basicbasic" from cutting letters from the given stickers.
```

Constraints:
* n == stickers.length
* 1 <= n <= 50
* 1 <= stickers[i].length <= 10
* 1 <= target <= 15
* stickers[i] and target consist of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minStickers(vector<string>& stickers, string target) {
        int n = target.size(); 
        vector<uint> dp(1 << n, -1); 
        dp[0] = 0; 
        for (int mask = 0; mask < (1 << n); ++mask) 
            if (dp[mask] != -1) 
                for (auto& sticker : stickers) {
                    int mask0 = mask; 
                    for (auto& ch : sticker) 
                        for (int j = 0; j < n; ++j) 
                            if (ch == target[j] && (mask0 & (1<<j)) == 0) {
                                mask0 ^= 1 << j; 
                                break; 
                            }
                    dp[mask0] = min(dp[mask0], 1 + dp[mask]);
                }
        return dp.back(); 
    }
};
```


