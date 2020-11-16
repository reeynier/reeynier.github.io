---
layout: post
title:  "Implement Trie (Prefix Tree) Problem"
categories: [ Algorithm ]
tags: [ Trie, Leetcode ]
similar: [ Trie ]
featured: false
hidden: false
---

<br />

## Description

Implement a **Trie** with **insert**, **search**, and **startsWith** methods. You may assume that all inputs are consist of lowercase letters **a-z**.


Example: 
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

<br />

## Solution

This problem is to implement the `trie` data structure. 

To implement the `trie` data structure, we need to implement a structure *TrieNode*. 

In the *TrieNode*, we can use an array to store possible subsequent letters. The array is indexed with 0 .. 25, representing the letters from 'a' to 'z'.

Originally, all elements in the array are *NULL*, meaning that this *TrieNode* is not pointing to any other *TrieNodes*. If there are subsequent letters to the current *TrieNode*, we can **new** a new *TrieNode* and add the node to the appropirate slot in the array of the current *TrieNode*. In this way, the two *TrieNodes* are connected. There is also an *is_end* flag in the *TrieNode*, indicating whether the current *TrieNode* is an end of a string.

To **insert** a string into the `trie` structure, we iterate through every letter in the string. For each letter, we **new** a *TrieNode* and add them to the array of the previous *TrieNode*. When we reach the end of the string, we mark the *is_end* flag to be true.

The time and space complexity of **insert** operation is O(m), where *m* is the string length.

To **search** a string in the `trie` structure, we start from the root node of the `trie`. In each *TrieNode*, we check whether the element in the array storing the *TrieNode* of the next letter is *NULL* or not. If it is NULL, then the string is not in the trie, we return false. If there is a *TrieNode* in that slot of the array, we use that *TrieNode* to keep on searching until the end of the string. When we reach the end of the string, we need to check the *is_end* tag. If the tag is true, that means this string is stored in the trie, we return true; otherwise, we return false.

The **startWith** method is similar to the **search** method. The only difference is that when we reach the string end, we do not need to check the *is_end* flag, we can return true directly.

The time complexity of **search** and **startWith** methods are O(m), where *m* is then length of the string. The space complexity are O(1).


<br />

## Sample C++ Code

This is a C++ implementation.

```c
#include <iostream>
#include <algorithm>

using namespace std;

class Trie {
public:
    struct TrieNode {
        TrieNode* arr[26];
        bool is_end;
        TrieNode() {
            for (int i = 0; i < 26; i ++) arr[i] = NULL;
            is_end = false;
        }
    };
    
    TrieNode* root;
    
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* curr = root;
        for (int i = 0; i < word.size(); i ++) {
            int idx = word[i] - 'a';
            if (curr->arr[idx] == NULL)
                curr->arr[idx] = new TrieNode();
            curr = curr->arr[idx];
        }
        curr->is_end = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* curr = root;
        for (int i = 0; i < word.size(); i ++) {
            int idx = word[i] - 'a';
            if (curr->arr[idx] == NULL)
                return false;
            curr = curr->arr[idx];
        }
        return curr->is_end;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        TrieNode* curr = root;
        for (int i = 0; i < prefix.size(); i ++) {
            int idx = prefix[i] - 'a';
            if (curr->arr[idx] == NULL)
                return false;
            curr = curr->arr[idx];
        }
        return true;
    }
};

int main() {
    Trie* obj = new Trie();
    string word = "apple";
    string prefix = "app";
    obj->insert(word);
    bool param_2 = obj->search(word);
    bool param_3 = obj->startsWith(prefix);

    cout << param_2 << " " << param_3 << endl;
}
```
