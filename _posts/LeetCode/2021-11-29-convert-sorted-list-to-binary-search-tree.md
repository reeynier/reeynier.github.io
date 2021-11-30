---
layout: post
title: "Convert Sorted List To Binary Search Tree Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Linked List, Divide and Conquer, Tree, Binary Search Tree, Binary Tree ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 109. Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

---

<br />

## Description

LeetCode Problem 109.

Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example 1:
```
Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.
```

Example 2:
```
Input: head = []
Output: []
```

Example 3:
```
Input: head = [0]
Output: [0]
```

Example 4:
```
Input: head = [1,3]
Output: [3,1]
```

Constraints:
* The number of nodes in head is in the range [0, 2 * 10^4].
* -10^5 <= Node.val <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    TreeNode *sortedListToBST(ListNode *head) {
    	return sortedListToBST( head, NULL );
    }
    
private:
    TreeNode *sortedListToBST(ListNode *head, ListNode *tail) {
    	if( head == tail )
    		return NULL;
    	if( head->next == tail ) {	
    		TreeNode *root = new TreeNode( head->val );
    		return root;
    	}
    	ListNode *mid = head, *temp = head;
    	while( temp != tail && temp->next != tail ) {
    		mid = mid->next;
    		temp = temp->next->next;
    	}
    	TreeNode *root = new TreeNode( mid->val );
    	root->left = sortedListToBST( head, mid );
    	root->right = sortedListToBST( mid->next, tail );
    	return root;
    }
};
```


