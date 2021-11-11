---
layout: post
title:  "Edit Distance Problem"
categories: [ Data Structure ]
tags: [ String, Dynamic Programming, Leetcode ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 72. Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.
---

<br />

## Description

LeetCode Problem 72. 

Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character
 

Example 1:
```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

Example 2:
```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

Constraints:

* 0 <= word1.length, word2.length <= 500
* word1 and word2 consist of lowercase English letters.


<br />

## Sample C++ Code


```c
int minDistance(string word1, string word2) {
    /* Use f[i][j] to represent the shortest edit distance between word1[0,i) and word2[0, j). 
    Then compare the last character of word1[0,i) and word2[0,j), 
    which are c and d respectively (c == word1[i-1], d == word2[j-1]):

    if c == d, then : f[i][j] = f[i-1][j-1]
    otherwise we can use three operations to convert word1 to word2:
        (a) if we replaced c with d: f[i][j] = f[i-1][j-1] + 1;
        (b) if we added d after c: f[i][j] = f[i][j-1] + 1;
        (c) if we deleted c: f[i][j] = f[i-1][j] + 1;

    Note that f[i][j] only depends on f[i-1][j-1], f[i-1][j] and f[i][j-1], 
    therefore we can reduce the space to O(n) by using only the (i-1)th array and previous 
    updated element(f[i][j-1]). */

    int l1 = word1.size();
    int l2 = word2.size();

    vector<int> f(l2+1, 0);
    for (int j = 1; j <= l2; ++j)
        f[j] = j;

    for (int i = 1; i <= l1; ++i)
    {
        int prev = i;
        for (int j = 1; j <= l2; ++j)
        {
            int cur;
            if (word1[i-1] == word2[j-1]) {
                cur = f[j-1];
            } else {
                cur = min(min(f[j-1], prev), f[j]) + 1;
            }

            f[j-1] = prev;
            prev = cur;
        }
        f[l2] = prev;
    }
    return f[l2];

}  
```
