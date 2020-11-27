---
layout: post
title:  "Longest Word In Dictionary Problem"
categories: [ Data Structure ]
tags: [ Trie, Depth First Search, Leetcode ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: Given a list of strings **words** representing an English dictionary, find the longest word in **words** that can be built one character at a time by other words in **words**.
---

<br />

## Description

Given a list of strings **words** representing an English dictionary, find the longest word in **words** that can be built one character at a time by other words in **words**. If there is more than one possible answer, return the longest word with the smallest lexicographical order. If there is no answer, return the empty string. 

All the strings in the input will only contain lowercase letters.


Example: 
```
Input:  words = ["w","wo","wor","worl", "world"]
Output: "world"
Explanation: The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
```

<br />

## Solution


#### Brute Force Approach

A simple solution is to use the `brute force` approach. 

We loop through every word in the dictionary. For each word, we loop through every prefix of the world and check whether that prefix of the word exists in the dictonary. Finally, we return the longest word that every prefix of the word exists in the dictionary.

The time complexity of this approach is O(n<sup>2</sup>m), where *n* is the length of the dictionary and *m* is the maximum length of the word in the dictionary. The space complexity is O(1).

#### Trie and Depth First Search Approach


We can use the data structure `trie` to store the dictionary and use `depth first search` to find the longest possible answer. Using the `trie` data structure can help us reduce the time complexity.

In every trie node, we use an array of length 26 to store possible next trie node, and a flag to indicate whether the trie node is the last letter of a word in the dictionary.

Suppose we have a dictionary of words like this, words = ["a", "banana", "app", "appl", "ap", "apply", "apple", "bar"]. The trie structure we build looks like the following. If the node is an end of a word, there is a * next to it.
```
a*   b
|    |
p*   a
|    | \
p*   n  r*
|    |
l*   a
|    |
e*   n
     |
     a*
```

After we build the trie, we can use depth first search to find the longest word that every letter in that word is an end of a word (marked by * in the above) in the dictionary.

The time complexity can be reduced to O(sum(m<sub>i</sub>)), where *m<sub>i</sub>* is the length of a word in the dictionary. The space complexity is O(sum(m<sub>i</sub>)).

<br />

## Sample C++ Code

This is a C++ implementation of the trie and depth first search approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct TrieNode {
    TrieNode* arr[26];
    bool is_end;
    TrieNode() {
        for (int i = 0; i < 26; i ++) arr[i] = NULL;
        is_end = false;
    }
};

void insert(TrieNode* root, string key) {
    TrieNode* curr = root;
    for (int i = 0; i < key.size(); i ++) {
        int idx = key[i] - 'a';
        if (curr->arr[idx] == NULL)
            curr->arr[idx] = new TrieNode();
        curr = curr->arr[idx];
    }
    curr->is_end = true;
}


void dfs(TrieNode* root, string key, string& ans) {
    if (root == NULL) return;
    for (int i = 0; i < 26; i ++) {
        if (root->arr[i] != NULL) {
            if (root->arr[i]->is_end == true) {
                key += (char)(i) + 'a';
                if (key.size() > ans.size())
                    ans = key;
                else if (key.size() == ans.size()) {
                    if (key < ans)
                        ans = key;
                }
                dfs(root->arr[i], key, ans);
                key.pop_back();
            }
        }
    }
}

string longestWord(vector<string>& words) {
    TrieNode* root = new TrieNode();
    for (int i = 0; i < words.size(); i ++)
        insert(root, words[i]);
    string ans;
    dfs(root, "", ans);
    return ans;
}

int main() {
    vector<string> words = {"w","wo","wor","worl", "world"};
    cout << longestWord(words) << endl;
}
```
