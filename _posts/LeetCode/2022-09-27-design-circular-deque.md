---
layout: post
title: "Design Circular Deque Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Linked List, Design, Queue ]
similar: [ Design ]
featured: false
hidden: false
excerpt: LeetCode 641. Design your implementation of the circular double-ended queue (deque).

---

<br />

## Description

LeetCode Problem 641.

Design your implementation of the circular double-ended queue (deque).

Implement the MyCircularDeque class:
* MyCircularDeque(int k) Initializes the deque with a maximum size of k.
* boolean insertFront() Adds an item at the front of Deque. Returns true if the operation is successful, or false otherwise.
* boolean insertLast() Adds an item at the rear of Deque. Returns true if the operation is successful, or false otherwise.
* boolean deleteFront() Deletes an item from the front of Deque. Returns true if the operation is successful, or false otherwise.
* boolean deleteLast() Deletes an item from the rear of Deque. Returns true if the operation is successful, or false otherwise.
* int getFront() Returns the front item from the Deque. Returns -1 if the deque is empty.
* int getRear() Returns the last item from Deque. Returns -1 if the deque is empty.
* boolean isEmpty() Returns true if the deque is empty, or false otherwise.
* boolean isFull() Returns true if the deque is full, or false otherwise.

Example 1:
```
Input
["MyCircularDeque", "insertLast", "insertLast", "insertFront", "insertFront", "getRear", "isFull", "deleteLast", "insertFront", "getFront"]
[[3], [1], [2], [3], [4], [], [], [], [4], []]
Output
[null, true, true, true, false, 2, true, true, true, 4]
Explanation
MyCircularDeque myCircularDeque = new MyCircularDeque(3);
myCircularDeque.insertLast(1);  // return True
myCircularDeque.insertLast(2);  // return True
myCircularDeque.insertFront(3); // return True
myCircularDeque.insertFront(4); // return False, the queue is full.
myCircularDeque.getRear();      // return 2
myCircularDeque.isFull();       // return True
myCircularDeque.deleteLast();   // return True
myCircularDeque.insertFront(4); // return True
myCircularDeque.getFront();     // return 4
```

Constraints:
* 1 <= k <= 1000
* 0 <= value <= 1000
* At most 2000 calls will be made to insertFront, insertLast, deleteFront, deleteLast, getFront, getRear, isEmpty, isFull.

<br />

## Sample C++ Code


```c
class MyCircularDeque {
private:
    vector<int> buffer;
    int cnt;
    int k;
    int front;
    int rear;
public:
    /** Initialize your data structure here. Set the size of the deque to be k. */
    MyCircularDeque(int k): buffer(k, 0), cnt(0), k(k), front(k - 1), rear(0) {
    }
    
    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    bool insertFront(int value) {
        if (cnt == k) {
            return false;
        }
        buffer[front] = value;
        front = (front - 1 + k) % k;
        ++cnt;

        return true;
    }
    
    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    bool insertLast(int value) {
        if (cnt == k) {
            return false;
        }
        buffer[rear] = value;
        rear = (rear + 1) % k;
        ++cnt;

        return true;
    }
    
    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    bool deleteFront() {
        if (cnt == 0) {
            return false;
        }
        front = (front + 1) % k;
        --cnt;

        return true;
    }
    
    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    bool deleteLast() {
        if (cnt == 0) {
            return false;
        }
        rear = (rear - 1 + k) % k;
        --cnt;

        return true;
    }
    
    /** Get the front item from the deque. */
    int getFront() {
        if (cnt == 0) {
            return -1;
        }
        return buffer[(front + 1) % k];
    }
    
    /** Get the last item from the deque. */
    int getRear() {
        if (cnt == 0) {
            return -1;
        }
        return buffer[(rear - 1 + k) % k];
    }
    
    /** Checks whether the circular deque is empty or not. */
    bool isEmpty() {
        return cnt == 0;
    }
    
    /** Checks whether the circular deque is full or not. */
    bool isFull() {
        return cnt == k;
    }
};
```


