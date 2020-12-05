---
layout: post
title:  "Virtual Memory II: Address Translation"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Virtual Memory ]
featured: false
hidden: false
excerpt: How can we `relocate` the process in memory in a way that is transparent to the process? 
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 15.

## Address Translation

To implement a simple virtual memory, we use the `hardware-based address translation` technique, or `address translation`. The address translation technique requires the combination of the OS and the hardware. For the hardware, it should support the translation of the virtual addresses provided by the instructions to physical addresses. This happens when there are memory accesses, such as instruction fetches, load instructions, and store instructions. For the OS, it should set up the hardware for correct translation, keep track of the memory usage of the processes, and control how memory is used.

The goal of address translation is to create an illusion to the process. The process has the illusion that it owns its private memory, and its `address space` starts at address zero and grows to a maximum of 16 KB. All memory accesses generated by the process should be within the bound (0 - 16 KB). In reality, the OS places the process somewhere in physical memory, not necessarily starting at address 0. The question is how can we `relocate` the process in memory in a way that is transparent to the process? 



#### Dynamic Relocation

The technique to support the address translation is referred to as `dynamic relocation`, or `base and bounds`. It requires two hardware registers within **each CPU**: the `base` register and the `bounds` register. With the base-and-bounds register pair, we can place the process' address space anywhere in physical memory.


The programs are written and compiled as if it is loaded at address zero. When a process starts running, the OS finds free space in physical memory and then sets the `base` register to the value of the beginning address of the memory chunk. 

When the process is running, the hardware translates all the memory accesses generated by the process in the following manner:

physical address = virtual address + base

The base here is the value stored in the base register, and the virtual address is the address provided by the program.

The address relocation happens at runtime. We can move address space even after the process has started running. Thus, this technique is often referred to as `dynamic relocation`.

The purpose of the `bound` register is for protection. Specifically, when doing address translation, the hardware will first check whether the memory access generated by the process is *within bounds*. The bound register would always be set to 16 KB. If a process generates a virtual address that is greater than the bounds, or is negative, the hardware will raise an exception, and the process will likely be terminated. 


The part of the hardware that supports the address translation is called `memory management unit (MMU)`. The base and bounds registers are also hardware structures. The hardware also provides special instructions to allow the OS to modify the base and bounds registers. These instructions are priviledged and can only be executed in kernel mode. 

#### Operating System Issues

As we stated above, the combination of hardware support and OS management leads to the implementation of a simple virtual memory. Here are the things the OS must get involved.

First, when a process is created, the OS must find space for its address space in memory and then mark the space as used. 

Second, when a process is terminated, the OS reclaims all of the process' memory and cleans up associated data structures. 

Thrid, when a context switch occurs, the OS must *save and restore* the base-and-bounds pair when it switches between processes. Specifically, when the OS decides to stop running a process, it must save the values of the base and bounds registers to memory (such as process control block). When the OS resumes a running process, it must set the values of the base and bounds to the correct values for this process.

Fourth, the OS must provide exception handlers. If a process tries to access memory outside its bounds, the CPU will raise an exception; the OS must be prepared to take action when such an exception arises (e.g. terminate the process).















