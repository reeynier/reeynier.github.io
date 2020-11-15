---
layout: post
title:  "Stream of Characters Problem"
categories: [ Algorithm, Leetcode ]
tags: [ Trie ]
similar: [ Trie, Queue ]
featured: false
hidden: false
---

<br />

## Description

Implement the **StreamChecker** class as follows.
* **StreamChecker(words)**: Constructor, initialize the data structure with the given words.
* **query(letter)**: returns true if and only if for some k >= 1, the last k characters queried (in order from oldest to newest, including this letter just queried) spell one of the words in the given list.

Words and queries will only consist of lowercase English letters.

Example: 
```
StreamChecker streamChecker = new StreamChecker(["cd","f","kl"]); // initialize the dictionary.
streamChecker.query('a');          // return false
streamChecker.query('b');          // return false
streamChecker.query('c');          // return false
streamChecker.query('d');          // return true, because 'cd' is in the wordlist
streamChecker.query('e');          // return false
streamChecker.query('f');          // return true, because 'f' is in the wordlist
streamChecker.query('g');          // return false
streamChecker.query('h');          // return false
streamChecker.query('i');          // return false
streamChecker.query('j');          // return false
streamChecker.query('k');          // return false
streamChecker.query('l');          // return true, because 'kl' is in the wordlist
```

<br />

## Solution

#### Trie and Queue Approach

We can use the `trie` data structure to solve this problem. How to build a `trie` structure and store the stream can be found in the [`Implement Trie Problem`]({% post_url 2020-11-14-implement-trie %}) post.


For all the queries, we use a *queue* to store the *TrieNodes* that are still valid for the current querying letter.

Every time we get a query, we push the root *TrieNode* to the queue. Then for every *TrieNode* in the queue, we check whether the querying letter exists in the array of next *TrieNodes*. If so, we point to the next *TrieNode* and push that *TrieNode* back to the queue; otherwise, we will remove the *TrieNode* from the queue. If the *is_end* tag of any of the *TrieNodes* in the queue is true, it means we find a word and we can return true.

Here is a walk-through of the approach. The trie is ["cd","f","kl"], and the queries are ('a', 'b', 'c', 'd').
```
Trie
c   f*  k
|       |
d*      l*

Queries:
| query | queue 
    a   |   -   <-- root->arr['a'-'a'] is NULL, queue is empty, return false
    b   |   -   <-- root->arr['b'-'a'] is NULL, queue is empty, return false
    c   |   c   <-- root->arr['c'-'a'] is not NULL, push root->arr['c'-'a'] to queue, return false
    d   |   d   <-- root->arr['c'-'a']->arr['d'-'a'] is not NULL, push root->arr['c'-'a']->arr['d'-'a'] to queue, is_end is true, return true
```

<br />

## Sample C++ Code

This is a C++ implementation of the trie and queue approach.

```c
#include <iostream>
#include <algorithm>
#include <queue>
#include <vector>

using namespace std;

class StreamChecker {
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
    queue<TrieNode*> q;
    
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
    
    StreamChecker(vector<string>& words) {
        root = new TrieNode();
        for (int i = 0; i < words.size(); i ++)
            insert(root, words[i]);
    }
    
    bool query(char letter) {
        q.push(root);
        int len = q.size();
        int idx = letter - 'a';
        TrieNode* curr;
        bool flag = false;
        for (int i = 0; i < len; i ++) {
            curr = q.front();
            q.pop();
            if (curr->arr[idx] != NULL) {
                if (curr->arr[idx]->is_end) {
                    flag = true;
                } 
                q.push(curr->arr[idx]);
            }    
        }
        return flag;
    }
};

int main() {
    vector<string> words = {"cd", "f", "kl"};
    StreamChecker* obj = new StreamChecker(words);
    cout << obj->query('a') << endl;
    cout << obj->query('b') << endl;
    cout << obj->query('c') << endl;
    cout << obj->query('d') << endl;
    cout << obj->query('e') << endl;
    cout << obj->query('f') << endl;
    cout << obj->query('g') << endl;
    cout << obj->query('h') << endl;
    cout << obj->query('i') << endl;
    cout << obj->query('j') << endl;
    cout << obj->query('k') << endl;
    cout << obj->query('l') << endl;
    return 0;
}
```
