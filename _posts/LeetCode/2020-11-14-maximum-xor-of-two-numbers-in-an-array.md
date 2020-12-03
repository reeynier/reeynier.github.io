---
layout: post
title:  "Maximum XOR of Two Numbers in an Array Problem"
categories: [ Data Structure ]
tags: [ Trie, Greedy, Leetcode ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 421. Given an integer array **nums**, return the maximum result of **nums[i] XOR nums[j]**
---

<br />

## Description


LeetCode Problem 421. Given an integer array **nums**, return the maximum result of **nums[i] XOR nums[j]**, where **0 ≤ i ≤ j < n**.


Example: 
```
Input: nums = [3,10,5,25,2,8]
Output: 28
Explanation: The maximum result is 5 XOR 25 = 28.
```

<br />

## Solution


#### Trie and Greedy Approach

We can use the `trie` data structure to store all the numbers in binary format. Then for each number in *nums*, we search for the number in the trie that will give us the maximum xor result. To obtain the maximum xor result, we need to find a number in the trie whose binary digits differ most from the number we are checking.



To build the `trie`, please refer to the [`Implement Trie Problem`]({% post_url LeetCode/2020-11-14-implement-trie %}) post. As we only storing the binary format of the numbers, we only need an array for two elements (0 and 1) in each *TrieNode*. To make the comparison between number easier, we store all the 32 binary bits for each number. 



Then for each number in *nums*, we search for the number in the trie that will give us the maximum xor result. We iterate through all the 32 bits. The strategy is to choose the oposite bit at each step whenever it is possible. So for any one bit in the number, if the opposite bit (1 to 0, or 0 to 1) exists in the trie, we update the *TrieNode* with the *TrieNode* stored in that opposite bit. If the opposite bit does not exist, we then use the *TrieNode* in the same bit. This is a greedy algorithm to find the number stored in the trie that has maximum digit differences from the number we are checking.



<br />

## Sample C++ Code

This is a C++ implementation of the trie and greedy approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct TrieNode {
    TrieNode* arr[2];
    bool is_end;
    TrieNode() {
        arr[0] = arr[1] = NULL;
        is_end = false;
    }
};

void insert(TrieNode* root, int num) {
    TrieNode* curr = root;
    for (int i = 31; i >= 0; i --) {
        int idx = ((num >> i) & 1);
        if (curr->arr[idx] == NULL)
            curr->arr[idx] = new TrieNode();
        curr = curr->arr[idx];
    }
    curr->is_end = true;
}

int maxXor = 0;

void search(TrieNode* root, int num) {
    TrieNode* curr = root;
    int val = 0;
    for (int i = 31; i >= 0; i --) {
        int idx = ((num >> i) & 1);
        if (idx == 0) {
            if (curr->arr[1] != NULL) {
                curr = curr->arr[1];
                val += (1 << i);
            } else {
                curr = curr->arr[0];
            }
        } else {
            if (curr->arr[0] != NULL) {
                curr = curr->arr[0];
                val += (1 << i);
            } else {
                curr = curr->arr[1];
            }
        }
    }
    if (val > maxXor)
        maxXor = val;
}

int findMaximumXOR(vector<int>& nums) {
    TrieNode* root = new TrieNode();
    for (int i = 0; i < nums.size(); i ++) {
        insert(root, nums[i]);
    }
    for (int i = 0; i < nums.size(); i ++) {
        search(root, nums[i]);
    }
    return maxXor;
}

int main() {
    vector<int> nums = {3,10,5,25,2,8};

    cout << findMaximumXOR(nums) << endl;
}
```
