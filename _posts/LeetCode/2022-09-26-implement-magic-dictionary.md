---
layout: post
title: "Implement Magic Dictionary Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Design, Trie ]
similar: [ Design ]
featured: false
hidden: false
excerpt: LeetCode 676. Design a data structure that is initialized with a list of different words. Provided a string, you should determine if you can change exactly one character in this string to match any word in the data structure.

---

<br />

## Description

LeetCode Problem 676.

Design a data structure that is initialized with a list of different words. Provided a string, you should determine if you can change exactly one character in this string to match any word in the data structure.

Implement theMagicDictionaryclass:
* MagicDictionary()Initializes the object.
* void buildDict(String[]dictionary)Sets the data structurewith an array of distinct strings dictionary.
* bool search(String searchWord) Returns true if you can change exactly one character in searchWord to match any string in the data structure, otherwise returns false.

Example 1:
```
Input
["MagicDictionary", "buildDict", "search", "search", "search", "search"]
[[], [["hello", "leetcode"]], ["hello"], ["hhllo"], ["hell"], ["leetcoded"]]
Output
[null, null, false, true, false, false]
Explanation
MagicDictionary magicDictionary = new MagicDictionary();
magicDictionary.buildDict(["hello", "leetcode"]);
magicDictionary.search("hello"); // return False
magicDictionary.search("hhllo"); // We can change the second 'h' to 'e' to match "hello" so we return True
magicDictionary.search("hell"); // return False
magicDictionary.search("leetcoded"); // return False
```

Constraints:
* 1 <=dictionary.length <= 100
* 1 <=dictionary[i].length <= 100
* dictionary[i] consists of only lower-case English letters.
* All the strings indictionaryare distinct.
* 1 <=searchWord.length <= 100
* searchWordconsists of only lower-case English letters.
* buildDictwill be called only once before search.
* At most 100 calls will be made to search.

<br />

## Sample C++ Code


```c
class MagicDictionary {
public:
    vector<string> dict;
    
    /** Initialize your data structure here. */
    MagicDictionary() {
    
    }
    
    void buildDict(vector<string> dictionary) {
        for (int i = 0; i < dictionary.size(); i ++) {
            dict.push_back(dictionary[i]);
        }
        return;
    }
    
    bool checkDiff(string a, string b) {
        if (a.size() != b.size())
            return false;
        int cnt_diff = 0;
        for (int i = 0; i < a.size(); i ++) {
            if (a[i] != b[i])
                cnt_diff ++;
        }
        return (cnt_diff == 1);
    }
    
    bool search(string searchWord) {
        bool exist = false;
        for (int i = 0; i < dict.size(); i ++) {
            if (checkDiff(searchWord, dict[i])) {
                exist = true;
                break;
            }
        }
        return exist;
    }
};

/**
 * Your MagicDictionary object will be instantiated and called as such:
 * MagicDictionary* obj = new MagicDictionary();
 * obj->buildDict(dictionary);
 * bool param_2 = obj->search(searchWord);
 */
```


