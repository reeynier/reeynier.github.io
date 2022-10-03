---
layout: post
title: "Number Of Music Playlists Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 920. Your music player contains n different songs. You want to listen to goal songs (not necessarily different) during your trip. 

---

<br />

## Description

LeetCode Problem 920.

Your music player contains n different songs. You want to listen to goal songs (not necessarily different) during your trip. To avoid boredom, you will create a playlist so that:
* Every song is played at least once.
* A song can only be played again only if k other songs have been played.

Given n, goal, and k, return the number of possible playlists that you can create. Since the answer can be very large, return it modulo 10^9 + 7.

Example 1:
```
Input: n = 3, goal = 3, k = 1
Output: 6
Explanation: There are 6 possible playlists: [1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], and [3, 2, 1].
```

Example 2:
```
Input: n = 2, goal = 3, k = 0
Output: 6
Explanation: There are 6 possible playlists: [1, 1, 2], [1, 2, 1], [2, 1, 1], [2, 2, 1], [2, 1, 2], and [1, 2, 2].
```

Example 3:
```
Input: n = 2, goal = 3, k = 1
Output: 2
Explanation: There are 2 possible playlists: [1, 2, 1] and [2, 1, 2].
```

Constraints:
* 0 <= k < n <= goal <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    // F(N,L,K) = F(N - 1, L - 1, K) * N + F(N, L - 1, K) * (N - K)
    // For F(N - 1, L - 1, K), if only N - 1 in the L - 1 first songs.
    // We need to put the rest one at the end of music list.
    // Any song can be this last song, so there are N possible combinations.
    // For F(N, L - 1, K), if already N in the L - 1 first songs.
    // We can put any song at the end of music list, 
    // but it should be different from K last song. We have N - K choices.
    int numMusicPlaylists(int N, int L, int K) {
        long dp[N + 1][L + 1], mod = 1e9 + 7;
        for (int i = K + 1; i <= N; ++i)
            for (int j = i; j <= L; ++j)
                if ((i == j) || (i == K + 1))
                    dp[i][j] = factorial(i);
                else
                    dp[i][j] = (dp[i - 1][j - 1] * i + dp[i][j - 1] * (i - K)) % mod;
        return (int) dp[N][L];
    }

    long factorial(int n) {
        return n ? factorial(n - 1) * n % (long)(1e9 + 7) : 1;
    }
};
```


