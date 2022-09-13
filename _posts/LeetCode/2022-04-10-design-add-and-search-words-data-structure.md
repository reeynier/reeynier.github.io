---
layout: post
title: "Design Add And Search Words Data Structure Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Depth-First Search, Design, Trie ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 211. Design a data structure that supports adding new words and finding if a string matches any previously added string.

---

<br />

## Description

LeetCode Problem 211.

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:
* WordDictionary()Initializes the object.
* void addWord(word) Adds word to the data structure, it can be matched later.
* bool search(word)Returns true if there is any string in the data structure that matches wordor false otherwise. word may contain dots '.' where dots can be matched with any letter.

Example:
```
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]
Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

Constraints:
* 1 <= word.length <= 500
* word in addWord consists lower-case English letters.
* word in search consist of '.' or lower-case English letters.
* At most 50000calls will be made to addWordand search.

<br />

## Sample C++ Code


```c
class WordDictionary {
public:
    struct TrieNode {
        TrieNode* arr[26];
        bool is_end;
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
        return;
    }
    
    TrieNode* head;
    
    /** Initialize your data structure here. */
    WordDictionary() {
        head = new TrieNode();
    }
    
    /** Adds a word into the data structure. */
    void addWord(string word) {
        insert(head, word);
    }
    
    void dfs(TrieNode* root, string& s, int idx, bool& found) {
        if (idx == s.size()) {
            if (root->is_end)
                found = true;
            return;
        }
        
        if (s[idx] == '.') {
            for (int i = 0; i < 26; i ++) {
                if (root->arr[i] != NULL)
                    dfs(root->arr[i], s, idx+1, found);
            }    
        } else {
            int i = s[idx] - 'a';
            if (root->arr[i] != NULL) {
                dfs(root->arr[i], s, idx+1, found);
            } 
        }
        
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    bool search(string word) {
        bool found = false;
        dfs(head, word, 0, found);
        return found;
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */
```


