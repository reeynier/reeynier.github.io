---
layout: post
title:  "Concurrency I: Introduction"
categories: [ Operating System ]
tags: [ Concurrency, Thread ]
similar: [ Concurrency ]
featured: false
hidden: false
excerpt: A `thread` is an abstraction for a single running process. Each thread is like a separate process.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 26.

#### Processes And Threads

A `thread` is an abstraction for a single running process. Instead of the classic view of a single point of execution within a program, a multi-threaded program has more than one point of execution. Each thread is like a separate process. The difference between a thread and a separate process is that the threads share the same address space and thus can access the same data. 

The state of a single thread is also very similar to that of a process. For each single thread, it has a `program counter (PC)` to store where the program is fetching instructions from, and a set of registers for use of computation. A `multi-threaded` program has multiple program counters to store execution points. During a `context switch` between threads, we need `thread control blocks (TCBs)` to store the state of each thread of a process. For the context switch between processes, we save the process state to a `process control block (PCB)`. In the context switch between threads as compared to processes, the address space remains the same and there is no need to switch which page table we are using.

Another major difference between threads and processes concerns the stack. For a process (or a `single-threaded process`), there is a single stack, which usually resides at the bottom of the address space. In multi-threaded process, each thread runs independently and owns a single stack in the address space.


#### Why Use Threads

There are two major reasons to use threads. The first one is `parallelism`. If you are executing the program on a system with multiple processors, you can potentially speed up this process by using the processors to each perform a portion of the work. Transforming the single-threaded program into a program running on multiple processors is called `parallelization`.

The second reason is to avoid blocking program progress due to slow I/O -- either disk I/O or a page fault. While one thread is waiting, the CPU schedular can switch to other threads to utilize the CPU to perform computation. Threading enables **overlap** of I/O with other activities within a single program.

In both cases, we can use multiple processes instead of threads. However, threads share an address space and thus easy to share data. Processes are a more sound choice for logically separate tasks where little sharing of data structures in memory is needed.

#### Thread Creation Example

```c
#include <stdio.h>
#include <assert.h>
#include <pthread.h>
#include "common.h"
#include "common_threads.h"

void *mythread(void *arg) {
	printf("%s\n", (char*)arg);
	return NULL;
}

int main(int argc, char* argv[]) {
	pthread_t p1, p2;
	printf("main: begin\n");
	Pthread_create(&p1, NULL, mythread, "A");
	Pthread_create(&p2, NULL, mythread, "B");
	// join waits for the threads to finish
	Pthread_join(p1, NULL);
	Pthread_join(p2, NULL);
	printf("main: end\n");
	return 0;
}
```

In the above example, the main program creates two threads. Each thread will run the function mythread() with different arguments (the string A or B). Once a thread is created, it may start running or may be put in a ready state. After creating the two threads, the main thread calls pthread_join(). It waits for a particular thread to complete. This ensures the two threads will run and complete before finally allowing the main thread to run again. The execution order of the two threads depends on the OS `scheduler`. A thread that is created first does not mean it will run first.









































