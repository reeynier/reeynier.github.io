---
layout: post
title:  "Word Search II Problem"
categories: [ Algorithm, Leetcode ]
tags: [ Trie, Backtracking ]
similar: [ Trie ]
featured: false
hidden: false
---

<br />

## Description

Given an **m x n** **board** of characters and a list of strings **words**, return all **words** on the **board**.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.



Example: 
```
-----------------
| o | a | a | n |        o---a   a   n          o   a   a   n  
-----------------            |
| e | t | a | e |        e   t   a   e          e   t---a---e 
-----------------            |
| i | h | k | r |        i   h   k   r          i   h   k   r 
-----------------
| i | f | l | v |        i   f   l   v          i   f   l   v 
-----------------
```
```
Input:  board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]]
        words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```

<br />

## Solution


#### Trie and Backtracking Approach

We can use the data structure `trie` to store the words. Then for each character in the board, we can use `backtracking` to search whether we can construct a word starting from this character.

We first build a trie structure that stores the list of words. In every trie node, we use an array of length 26 to store possible next trie node, and a flag to indicate whether the trie node is the last letter of a word in the dictionary. We also use a string to store the string formed by the trie nodes starting from the root node.

Suppose we have a list of words like this, words = ["oath","pea","eat","rain"]. The trie structure we build looks like the following. If the node is an end of a word, there is a * next to it.
```
e   o   p   r
|   |   |   |
a   a   e   a
|   |   |   |
t*  t   a*  i
    |       |
    h*      n*
```  

Next, for each character in the board, we use `backtracking` to search whether we can construct a word starting from this character. 

In each cell of the board, we mark this cell as visited, then we search the four neighboring cells. During the search, if the current cell has been visited, or does not exist in the trie, we backtrack. If we reach the end of a word in the trie, we find a solution.


<br />

## Sample C++ Code

This is a C++ implementation of the trie and backtracking approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<string> ans;

struct TrieNode {
    TrieNode* arr[26];
    bool is_end;
    string word;
    TrieNode() {
        for (int i = 0; i < 26; i ++) {
            arr[i] = NULL;
        }
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
    curr->word = key;
}

void backtrack(vector<vector<char>>& board, TrieNode* root, int x, int y) {
    if (x < 0 || x >= board.size() || y < 0 || y >= board[0].size())
        return;
    
    char c = board[x][y];
    if (c == '.') return;
    if (root->arr[c-'a'] == NULL) return;
    
    board[x][y] = '.';
    if (root->arr[c-'a']->is_end == true) {
        ans.push_back(root->arr[c-'a']->word); 
        root->arr[c-'a']->is_end = false;
    }
    
    backtrack(board, root->arr[c-'a'], x-1, y);
    backtrack(board, root->arr[c-'a'], x+1, y);
    backtrack(board, root->arr[c-'a'], x, y-1);
    backtrack(board, root->arr[c-'a'], x, y+1);
    
    board[x][y] = c;
    
}

vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
    int r = board.size(), c = board[0].size();
    
    TrieNode* root = new TrieNode();
    for (int i = 0; i < words.size(); i ++) {
        insert(root, words[i]);
    }
    
    for (int i = 0; i < r; i ++) {
        for (int j = 0; j < c; j ++) {
            backtrack(board, root, i, j);
        }
    }
    return ans;
}

int main() {
    vector<vector<char>> board;
    board.push_back({'o','a','a','n'});
    board.push_back({'e','t','a','e'});
    board.push_back({'i','h','k','r'});
    board.push_back({'i','f','l','v'});
    vector<string> words = {"oath","pea","eat","rain"};
    vector<string> ans = findWords(board, words);
    for (int i = 0; i < ans.size(); i ++)
        cout << ans[i] << endl;
}
```
