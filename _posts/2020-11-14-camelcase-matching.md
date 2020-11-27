---
layout: post
title:  "Camelcase Matching Problem"
categories: [ Data Structure ]
tags: [ Trie, Leetcode ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: A query word matches a given **pattern** if we can insert lowercase letters to the pattern word so that it equals the **query**. 
---

<br />

## Description


A query word matches a given **pattern** if we can insert lowercase letters to the pattern word so that it equals the **query**. (We may insert each character at any position, and may insert 0 characters.)

Given a list of **queries**, and a **pattern**, return an **answer** list of booleans, where **answer[i]** is true if and only if **queries[i]** matches the **pattern**.





Example: 
```
Input:  queries = ["FooBar","FooBarTest","FootBall","FrameBuffer","ForceFeedBack"], 
        pattern = "FB"
Output: [true,false,true,true,false]
Explanation: 
        "FooBar" can be generated like this "F" + "oo" + "B" + "ar".
        "FootBall" can be generated like this "F" + "oot" + "B" + "all".
        "FrameBuffer" can be generated like this "F" + "rame" + "B" + "uffer".
```

<br />

## Solution


#### Trie Approach

We can use the `trie` data structure to store the *pattern*. Then for each word in the *queries*, we check the word against the trie to see if it matches the *pattern*.

To build the `trie`, please refer to the [`Implement Trie Problem`]({% post_url 2020-11-14-implement-trie %}) post. As there are both upper case and lower case letters, we need to use an array of size 52 to store next *TrieNodes*. For the first 26 elements, we store lower case letters; and for the last 26 elements, we store upper case letters.

For each word in the *queries*, we check whether it matches the *pattern*. We iterate through the letters in the word. If the letter is an upper case letter, we check whether the element in the array representing this letter is NULL or not. If so, we can return false, the word does not match the patter; otherwise, we update the current *TrieNode* with the next *TrieNode* representing this letter. If the letter is a lower case letter, it is ok that we do not find it in the *pattern*. So we check whether the element in the array representing this letter is NULL or not. If it is not NULL, we update the current *TrieNode* with the next *TrieNode*; otherwise, we do nothing.



<br />

## Sample C++ Code

This is a C++ implementation of the trie approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<string> ans;

struct TrieNode {
    TrieNode* arr[52];
    bool is_end;
    TrieNode() {
        for (int i = 0; i < 52; i ++) arr[i] = NULL;
        is_end = false;
    }
};

void insert(TrieNode* root, string key) {
    TrieNode* curr = root;
    int idx;
    for (int i = 0; i < key.size(); i ++) {
        if (key[i] >= 'A' && key[i] <= 'Z')
            idx = 26 + key[i] - 'A';
        else
            idx = key[i] - 'a';
        if (curr->arr[idx] == NULL)
            curr->arr[idx] = new TrieNode();
        curr = curr->arr[idx];
    }
    curr->is_end = true;
}

bool check(TrieNode* root, string key) {
    int idx;
    TrieNode* curr = root;
    for (int i = 0; i < key.size(); i ++) {
        if (key[i] >= 'A' && key[i] <= 'Z') {
            idx = 26 + key[i] - 'A';
            if (curr->arr[idx] == NULL)
                return false;
            else
                curr = curr->arr[idx];
        } else {
            idx = key[i] - 'a';
            if (curr->arr[idx] != NULL)
                curr = curr->arr[idx];
        }
    }
    return curr->is_end;
}

vector<bool> camelMatch(vector<string>& queries, string pattern) {
    TrieNode* root = new TrieNode();
    insert(root, pattern);
    
    vector<bool> ans;
    for (int i = 0; i < queries.size(); i ++) {
        ans.push_back(check(root, queries[i]));
    }
    return ans;
}

int main() {
    vector<string> queries = {"FooBar","FooBarTest","FootBall","FrameBuffer","ForceFeedBack"};
    string pattern = "FB";

    vector<bool> ans = camelMatch(queries, pattern);
    for (int i = 0; i < ans.size(); i ++) {
        cout << ans[i] << " ";
    }
}
```
