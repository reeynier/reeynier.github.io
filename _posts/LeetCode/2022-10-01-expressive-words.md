---
layout: post
title: "Expressive Words Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 809. Sometimes people repeat letters to represent extra feeling. 

---

<br />

## Description

LeetCode Problem 809.

Sometimes people repeat letters to represent extra feeling. For example:
* "hello" -> "heeellooo"
* "hi" -> "hiiii"

In these strings like "heeellooo", we have groups of adjacent letters that are all the same: "h", "eee", "ll", "ooo".

You are given a string s and an array of query strings words. A query word is stretchy if it can be made to be equal to s by any number of applications of the following extension operation: choose a group consisting of characters c, and add some number of characters c to the group so that the size of the group is three or more.

* For example, starting with "hello", we could do an extension on the group "o" to get "hellooo", but we cannot get "helloo" since the group "oo" has a size less than three. Also, we could do another extension like "ll" -> "lllll" to get "helllllooo". If s = "helllllooo", then the query word "hello" would be stretchy because of these two extension operations: query = "hello" -> "hellooo" -> "helllllooo" = s.

Return the number of query strings that are stretchy.

Example 1:
```
Input: s = "heeellooo", words = ["hello", "hi", "helo"]
Output: 1
Explanation: 
We can extend "e" and "o" in the word "hello" to get "heeellooo".
We can't extend "helo" to get "heeellooo" because the group "ll" is not size 3 or more.
```

Example 2:
```
Input: s = "zzzzzyyyyy", words = ["zzyy","zy","zyy"]
Output: 3
```

Constraints:
* 1 <= s.length, words.length <= 100
* 1 <= words[i].length <= 100
* s and words[i] consist of lowercase letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    
    void cntChars(string s, vector<int> &charVec, 
                 vector<int> &cntVec) {
        charVec.push_back(s[0]-'a');
        int cnt = 1;
        for (int i = 1;i < s.size(); i ++) {
            if ((s[i] - 'a') == charVec.back()) {
                cnt ++;
            } else {
                cntVec.push_back(cnt);
                charVec.push_back(s[i] - 'a');
                cnt = 1;
            }
        }
        cntVec.push_back(cnt);
    }
    
    int expressiveWords(string S, vector<string>& words) {
        int count = 0;
        vector<int> charSeq, cntSeq;
        vector<int> charW, cntW;
        
        if (S.size() == 0)
            return 0;
        
        cntChars(S, charSeq, cntSeq);

        for (int i = 0; i < words.size(); i ++) {
            string e = words[i];
            charW.clear();
            cntW.clear();
            
            if (e.size() == 0)
                continue;
            
            cntChars(e, charW, cntW);
            
            if (charW.size() != charSeq.size()) 
                continue;
            
            bool is_stretchy = true;
            for (int j = 0; j < charW.size(); j ++) {
                if (charW[j] != charSeq[j]) {
                    is_stretchy = false;
                    break;
                }
                if (cntW[j] != cntSeq[j]) {
                    if ((cntSeq[j] < 3) || (cntSeq[j] < cntW[j])) {
                        is_stretchy = false;
                        break;
                    }
                }
            }
                        
            if (is_stretchy)
                count ++;
        }
        
        return count;
    }
};
```


