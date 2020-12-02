---
layout: post
title:  "Concatenate Words Problem"
categories: [ Data Structure ]
tags: [ Trie, Depth First Search, Leetcode ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 472. Given a list of **words** (without duplicates), return all **concatenated words** in the given list of **words**.
---

<br />

## Description


LeetCode Problem 472. Given a list of **words** (without duplicates), return all **concatenated words** in the given list of **words**.
A **concatenated word** is defined as a string that is comprised entirely of at least two shorter words in the given array.


Example: 
```
Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
Explanation: 
1. "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
2. "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
3. "ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
```

<br />

## Solution


#### Trie and Depth First Search Approach


We can use the data structure `trie` to store the words. Then for each word in the list of words, we use depth first search to see whether it is a concatenation of two or more words from the list.

We first build a trie structure that stores the list of words. In every trie node, we use an array of length 26 to store possible next trie node, and a flag to indicate whether the trie node is the last letter of a word in the dictionary.

Suppose we have a list of words like this, words = ["cat", "cats", "catsdogcats", "dog", "dogcatsdog", "hippopotamuses", "rat", "ratcatdogcat"]. The trie structure we build looks like the following. If the node is an end of a word, there is a * next to it.
```
c    d    h    r
|    |    |    |
a    o    i    a
|    |    |    |
t*   g*   p    t*
|    |    |    |
s*   c    p    c
|    |    |    |
d    a    o    a
|    |    |    |
o    t    p    t
|    |    |    |
g    s    o    d
|    |    |    |
c    d    t    o
|    |    |    |
a    o    a    g
|    |    |    |
t    g*   m    c
|         |    |
s*        u    a
          |    |
          s    t*
          |
          e
          |
          s*
```  

Next, for each word in the sentence, we search whether the word is a concatenation of two or more other words from the list. We can use `depth first search` here.

For each word, we start from the root node of the trie and the first letter of the word. If the letter is not null in the current trie node, we go to the next trie node of that letter. We keep searching until the trie node is an end of a word (with a * in the above graph). We increase the count of words the comprise the current word. Then we start from the root node of the trie again, and keep on searching until we reach the end of the current word. If we cannot find the letter in the trie, we go backtrack to the last run of trie nodes and continue the search.

If we can find a concatenation of words that reaches the end of the current word, we check how many words are concatenated. If it is greater than 2, we put the current word to the final answer.


Let's take the word "catsdogcats" as an example. 
```
 c    <-- we start from the root node, and the first letter is "c"
 |
cat   <-- "cat" exists, we reach an end of a word, we start from the root again (count = 1)
 |
 s    <-- no "s" exists in the root node, we backtrack (count = 2)
 |
cats  <-- "cats" exists, we reach an end of a word, we start from the root again (count = 1)
 |
dog   <-- "dog" exists, we reach an end of a word, we start from the root again (count = 2)
 |
cat   <-- "cat" exists, we reach an end of a word, we start from the root again (count = 3)
 |
 s    <-- no "s" exists in the root node, we backtrack (count = 4)
 |
cats  <-- "cats" exists, we reach an end of the word "catsdogcats", count = 3, we ar done.
```

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

bool dfs(TrieNode* root, string key, int index, int count) {
    if (index >= key.size())
        return count > 1;
    TrieNode* curr = root;
    for (int i = index; i < key.size(); i ++) {
        int p = key[i] - 'a';
        if (curr->arr[p] == NULL) {
            return false;
        }
        curr = curr->arr[p];
        if (curr->is_end) {
            if (dfs(root, key, i+1, count+1))
                return true;
        }
    }
    return false;
}

vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
    TrieNode* root = new TrieNode();
    for (int i = 0; i < words.size(); i ++) {
        insert(root, words[i]);
    }
    vector<string> ans;
    for (int i = 0; i < words.size(); i ++) {
        if (dfs(root, words[i], 0, 0))
            ans.push_back(words[i]);
    }
    return ans;   
}

int main() {
    vector<string> words = {"cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"};
    vector<string> ans = findAllConcatenatedWordsInADict(words);
    for (int i = 0; i < ans.size(); i ++)
        cout << ans[i] << endl;
}
```
