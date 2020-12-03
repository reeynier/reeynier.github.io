---
layout: post
title:  "Replace Words Problem"
categories: [ Data Structure ]
tags: [ Trie, Leetcode ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 648. Given a **dictionary** consisting of many *roots*, and a **sentence** consisting of words separated by spaces,
---

<br />

## Description

LeetCode Problem 648. Given a **dictionary** consisting of many *roots* (a concept in English that can be followed by some other letters to form another longer word which is called a *successor*), and a **sentence** consisting of words separated by spaces, replace all *successors* in the **sentence** with the *root* forming it. If a *successor* can be replaced by more than one *root*, replace it with the *root* that has the shortest length. Return the **sentence** after replacement.


Example: 
```
Input: dictionary = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

<br />

## Solution


#### Trie Approach


We can use the data structure `trie` to store the dictionary. Then for each word in the sentence, we search the shortest root in the trie.

In every trie node, we use an array of length 26 to store possible next trie node, and a flag to indicate whether the trie node is the last letter of a word in the dictionary.

Suppose we have a dictionary of roots like this, dictionary = ["cat","bat","rat"]. The trie structure we build looks like the following. If the node is an end of a word, there is a * next to it.
```
b    c    r
|    |    |
a    a    a
|    |    |
t*   t*   t*
```

Next, for each word in the sentence, we search whether a root of the word exists in the trie. We start from the first letter of the word. If the letter is not null in the current trie node, we go to the next trie node of that letter. We keep searching until the trie node is an end of a root. 

Let's take the word "cattle" as an example. We start from the letter "c". The letter "c" is not null in the current trie node, then we go to the next trie node of "c", which is "a". Then we go to the next trie node of "a", which is "t". The letter "t" is an end node of a root, so the shortest root of the word "cattle" is "cat". We then replace "cattle" with "cat" in the sentence.

The time complexity can be reduced to O(n), where *n* is the length of the sentence. The space complexity is O(n).

<br />

## Sample C++ Code

This is a C++ implementation of the trie approach.

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

string search(TrieNode* root, string key) {
    TrieNode* curr = root;
    string rootStr = "";
    for (int i = 0; i < key.size(); i ++) {
        int idx = key[i] - 'a';
        rootStr += key[i];
        if (curr->arr[idx] == NULL) {
            return key;
        }
        if (curr->arr[idx]->is_end) {
            return rootStr;
        }        
        curr = curr->arr[idx];
    }
    return key;
}

string replaceWords(vector<string>& dictionary, string sentence) {
    TrieNode* root = new TrieNode();
    for (int i = 0; i < dictionary.size(); i ++) {
        insert(root, dictionary[i]);
    }
    
    string ans, word;
    while (!sentence.empty()) {
        size_t p = sentence.find(' ');
        word = sentence.substr(0, p);
        sentence = sentence.substr(p+1, sentence.size()-p-1);
        ans += search(root, word);
        if (p == string::npos)
            break;
        else
            ans += ' ';
    }
    return ans;
}

int main() {
    vector<string> words = {"cat","bat","rat"};
    string sentence = "the cattle was rattled by the battery";
    cout << replaceWords(words, sentence) << endl;
}
```
