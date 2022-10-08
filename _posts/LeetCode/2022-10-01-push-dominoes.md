---
layout: post
title: "Push Dominoes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String, Dynamic Programming ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 838. There are n dominoes in a line, and we place each domino vertically upright. In the beginning, we simultaneously push some of the dominoes either to the left or to the right.

---

<br />

## Description

LeetCode Problem 838.

There are n dominoes in a line, and we place each domino vertically upright. In the beginning, we simultaneously push some of the dominoes either to the left or to the right.

After each second, each domino that is falling to the left pushes the adjacent domino on the left. Similarly, the dominoes falling to the right push their adjacent dominoes standing on the right.

When a vertical domino has dominoes falling on it from both sides, it stays still due to the balance of the forces.

For the purposes of this question, we will consider that a falling domino expends no additional force to a falling or already fallen domino.

You are given a string dominoes representing the initial state where:
* dominoes[i] = 'L', if the i^th domino has been pushed to the left,
* dominoes[i] = 'R', if the i^th domino has been pushed to the right, and
* dominoes[i] = '.', if the i^th domino has not been pushed.

Return a string representing the final state.

Example 1:
```
Input: dominoes = "RR.L"
Output: "RR.L"
Explanation: The first domino expends no additional force on the second domino.
```

Example 2: 
```
Input: dominoes = ".L.R...LR..L.."
Output: "LL.RR.LLRRLL.."
```

Constraints:
* n == dominoes.length
* 1 <= n <= 10^5
* dominoes[i] is either 'L', 'R', or '.'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    // If we encounter . in string, we move forward to next index.
    // If we encounter L in string, we see if index of right is -1, 
    // we make all the left index L until we see any other L.
    // If we encounter L in string and there is some previous R index, 
    // then we simultaneously change string from left and right side till 
    // two pointers reach each other. After that right moves back to -1.
    // If we encounter R in string, we see if the index of R is not -1, 
    // we make all the indices upto that index R.
    string pushDominoes(string s) {
        int N = s.size(), right = -1;
        for (int i = 0; i < N; ++i) {
            if (s[i] == 'L') {
                if (right == -1) { 
                    for (int j = i - 1; j >= 0 && s[j] == '.'; --j) 
                      s[j] = 'L';  
                } else {
                    for (int j = right + 1, k = i - 1; j < k; ++j, --k) {
                        s[j] = 'R';
                        s[k] = 'L';
                    } 
                    right = -1;
                }
            } else if (s[i] == 'R') {
                if (right != -1) {
                    for (int j = right + 1; j < i; ++j) 
                        s[j] = 'R';
                }
                right = i;
            }
        }
        if (right != -1) {
            for (int j = right + 1; j < N; ++j) 
                s[j] = 'R';
        }
        return s;
    }
};
```


