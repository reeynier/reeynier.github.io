---
layout: post
title: "Implement Queue Using Stacks Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Stack, Design, Queue ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 232. Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

---

<br />

## Description

LeetCode Problem 232.

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:
* void push(int x) Pushes element x to the back of the queue.
* int pop() Removes the element from the front of the queue and returns it.
* int peek() Returns the element at the front of the queue.
* boolean empty() Returns true if the queue is empty, false otherwise.

Notes:
* You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
* Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

Example 1:
```
Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]
Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

Constraints:
* 1 <= x <= 9
* At most 100calls will be made to push, pop, peek, and empty.
* All the calls to pop and peek are valid.


<br />

## Sample C++ Code


```c
class MyQueue {
public:
    stack<int> s1, s2;
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        s1.push(x);
        return;
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int ele = 0;
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        if (!s2.empty()) {
            ele = s2.top();
            s2.pop();
        }
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        return ele;
    }
    
    /** Get the front element. */
    int peek() {
        int ele = 0;
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        if (!s2.empty()) {
            ele = s2.top();
        }
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        return ele;
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return s1.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```


