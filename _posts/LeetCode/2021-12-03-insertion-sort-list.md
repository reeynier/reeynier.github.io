---
layout: post
title: "Insertion Sort List Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Linked List, Sorting ]
similar: [ Linked List ]
featured: false
hidden: false
excerpt: LeetCode 147. Given the head of a singly linked list, sort the list using insertion sort, and return the sorted list's head.

---

<br />

## Description

LeetCode Problem 147.

Given the head of a singly linked list, sort the list using insertion sort, and return the sorted list's head.

The steps of the insertion sort algorithm:
* Insertion sort iterates, consuming one input element each repetition and growing a sorted output list.
* At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list and inserts it there.
* It repeats until no input elements remain.

The following is a graphical example of the insertion sort algorithm. The partially sorted list (black) initially contains only the first element in the list. One element (red) is removed from the input data and inserted in-place into the sorted list with each iteration.

Example 1: 
```
Input: head = [4,2,1,3]
Output: [1,2,3,4]
```

Example 2: 
```
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```

Constraints:
* The number of nodes in the list is in the range [1, 5000].
* -5000 <= Node.val <= 5000

<br />

## Sample C++ Code


```c
ListNode *insertionSortList(ListNode *head) {
	if (head == NULL || head->next == NULL)
		return head;

	ListNode *p = head->next;
	head->next = NULL;

	while (p != NULL) {
		// store the next node to be insert
		ListNode *pNext = p->next;    
		ListNode *q = head;

		if (p->val < q->val) {
			// node p should be the new head
			p->next = q;
			head = p;
		}
		else {
			while (q != NULL && q->next != NULL && q->next->val <= p->val)
				q = q->next;
			p->next = q->next;
			q->next = p;
		}

		p = pNext;
	}
	return head;
}
```


