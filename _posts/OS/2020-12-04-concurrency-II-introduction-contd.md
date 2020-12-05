---
layout: post
title:  "Concurrency II: Introduction Cont'd"
categories: [ Operating System ]
tags: [ Concurrency, Thread ]
similar: [ Concurrency ]
featured: false
hidden: false
excerpt: Another important question is how threads interact when they access shared data.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 26.



#### Shared Data Example

In the [previous post]({% post_url OS/2020-12-04-concurrency-I-introduction %}), we showed the difference between processes and threads, when to use threads, how to create threads, and how threads can run in different orders. Another important question is how threads interact when they access shared data.

```c
#include <stdio.h>
#include <pthread.h>
#include "common.h"
#include "common_threads.h"

static volatile int counter = 0;

// simply adds 1 to counter repeatedly, in a loop
void* mythread(void* arg) {
	printf("%s: begin\n", (char*)arg);
	for (int i = 0; i < 1e7; i ++) {
		counter = counter + 1;
	}
	printf("%s: done\n", (char*)arg);
	return NULL;
}

// launches two threads (pthread_create)
// then waits for them (pthread_join)
int main(int argc, char* argv[]) {
	pthread_t p1, p2;
	printf("main: begin (counter = %d)\n", counter);
	Pthread_create(&p1, NULL, mythread, "A");
	Pthread_create(&p2, NULL, mythread, "B");

	// join waits for the threads to finish
	Pthread_join(p1, NULL);
	Pthread_join(p2, NULL);
	printf("main: done with both (counter = %d)\n", counter);
	return 0;
}
```

In this example, two threads will update a global shared variable. Instead of using two separate function bodies for the two threads, we use a single piece of code. Then, ideally, each thread adds a number to the shared variable counter for 10 million times in a loop. The desired final result is 20 million, and the desired output of the program is:
```
// Expected output
main: begin (counter = 0)
A: begin
B: begin
A: done
B: done
main: done with both (counter = 20000000)
```

However, when we run the code, we don't get the desired results and we even get different results for different runnings.
```
// One possible output
main: begin (counter = 0)
A: begin
B: begin
A: done
B: done
main: done with both (counter = 19345221)

// Another possible output
main: begin (counter = 0)
A: begin
B: begin
A: done
B: done
main: done with both (counter = 19221041)
```

#### Uncontrolled Scheduling

To understand why this happens, we first look at the code sequence of adding 1 to counter. We assume that the variable counter is located at address 0x8049a1c. The following three instructions load the value in counter to register eax, add 1, and store back the new value in eax to memory at the same address.

```
mov 0x8049a1c, %eax
add $0x1, %eax
mov %eax, 0x8049a1c
```


When there are two threads entering this region of code, something wrong can happen. Suppose thread 1 loads the value of counter, say 50, to its own private register, and then adds 1. Before thread 1 stores the value back to memory, a timer interrupt goes off; thus, the OS saves the state of thread 1 to its TCB and starts running thread 2. Thread 2 also loads the value of counter from memory, which is still 50 (but should be 51), to its own private register. Then thread 2 add 1 to the register and stores the value back to memory. The value in counter is now 51. Again, another context switch occurs. Thread 1 resumes and stores its value from register to memory, which is also 51. After the two executions, the counter is still 51, although it is expected to be 52. This is a `race condition`. The results of a race condition depend on the timing execution of the code, thus is `indeterministic`. 

Because multiple threads executing this code can result in a race condition, we call this code a `critical section`. A critical section is a piece of code that accesses a shared resource, and must not be concurrently executed by more than one thread.

One way to solve this problem would be to make sure the instructions in the critical section are executed `atomically`. It could not be interrupted. When an interrupt occurs, either the instruction has not run at all, or it has run to completion; there is no in-between state.


























































