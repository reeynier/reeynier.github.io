---
layout: post
title: "Serialize And Deserialize Binary Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Tree, Breadth-First Search, Design ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 297. Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

---

<br />

## Description

LeetCode Problem 297.

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Example 1:
```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```

Example 2:
```
Input: root = []
Output: []
```

Example 3:
```
Input: root = [1]
Output: [1]
```

Example 4:
```
Input: root = [1,2]
Output: [1,2]
```

Constraints:
* The number of nodes in the tree is in the range [0, 10^4].
* -1000 <= Node.val <= 1000

<br />

## Sample C++ Code


```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string rootS, leftS, rightS;
        if (root == NULL)
            return "null";
        queue<TreeNode*> bfsQ;
        bfsQ.push(root);
        rootS = to_string(root->val);
        
        int len;
        TreeNode* curr;
        while (!bfsQ.empty()) {
            len = bfsQ.size();
            for (int i = 0; i < bfsQ.size(); i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                if (curr != NULL) {
                    if (curr->left == NULL)
                        rootS += ",null";
                    else
                        rootS += "," + to_string(curr->left->val);
                    if (curr->right == NULL)
                        rootS += ",null";
                    else
                        rootS += "," + to_string(curr->right->val);
                
                    bfsQ.push(curr->left);
                    bfsQ.push(curr->right);
                }
            }
        }
        int l = rootS.size();
        while ((l > 5) && (rootS.substr(l - 5, 5) == ",null")) {
            rootS = rootS.substr(0, l - 5);
            l = rootS.size();
        }
        
        return rootS;
    }
    
    string getNode(string& s) {
        int i = 0;
        string node;
        while ((s[i] != ',') && (i < s.size())) {
            node += s[i];
            i ++;
        }
        if (i < s.size())
            s = s.substr(i + 1, s.size() - i - 1);
        else
            s = "";
        return node;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if (data == "null")
            return NULL;

        string nodeS;
        TreeNode* root = new TreeNode;
        nodeS = getNode(data);
        root->val = stoi(nodeS);
        queue<TreeNode*> bfsQ;
        bfsQ.push(root);
        
        int len;
        TreeNode* curr;
        while (!bfsQ.empty()) {
            len = bfsQ.size();
            for (int i = 0;i < len; i ++) {
                curr = bfsQ.front();
                bfsQ.pop();
                
                if (curr != NULL) {
                    nodeS = getNode(data);
                    if (nodeS.empty())
                        return root;
                    TreeNode* leftNode = new TreeNode;
                    leftNode->left = NULL;
                    leftNode->right = NULL;
                    if (nodeS == "null")
                        leftNode = NULL;
                    else
                        leftNode->val = stoi(nodeS);
                    curr->left = leftNode;
                
                    
                    nodeS = getNode(data);
                    if (nodeS.empty())
                        return root;
                    TreeNode* rightNode = new TreeNode;
                    rightNode->left = NULL;
                    rightNode->right = NULL;
                    if (nodeS == "null")
                        rightNode = NULL;
                    else
                        rightNode->val = stoi(nodeS);
                    curr->right = rightNode;
                    
                    bfsQ.push(leftNode);
                    bfsQ.push(rightNode);
                }
            }
        }
        return root;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```


