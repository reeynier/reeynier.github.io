---
layout: post
title:  "Virtual Memory I: Overview"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Operating System ]
featured: false
hidden: false
excerpt: Virtual Memory is an abstraction that the Operating System provides for managing memory. Virtual Memory enables a program to execute with less physical memory than it needs.
---

<br />

## Virtual Memory Brief

`Virtual Memory` is an abstraction that the `Operating System` provides for managing memory. Virtual Memory enables a program to execute with less physical memory than it needs. This is based on the fact that many programs do not need all of their code and data at once (or ever). Virtual Memory requires hardware support and OS management algorithsm. The operating system will adjust memory allocation to a process based upon its behavior.

```
               Illegal Address:
 -----------   To Fault Handler                                      --------
|   kernel  | <------------------------                             |        |
 -----------                           |                            |        |
|           |                          |          Legal Address:    |        |
|application| Virtual Address    ---------------  Pysical Address   | memory |
|   load/   | <---------------> | MMU(Hardware) | <---------------> |        |
|   store   |                    ---------------                    |        |
|           | <---------------------------------------------------> |        |
 -----------                                                         --------
```

As shown in the above figure, programs load or store to `virtual addresses`. The actual memory uses `physical addresses`. The virtual memory hardware is the `Mameory Management Unit (MMU)`. MMU is usually part of CPU. It translates between virtual addresses and physical addresses. It gives per-process view of memory called `address space`. MMU can be configured through privileged instructions.

<br />


## Virtual Memory Goals

First, virtual memory gives each program its own virtual address space. At runtime, the Memory-Management Unit (MMU) relocates each load and store, and the applications do not see physical memory addresses.

Second, virtual memory can enforce protection and prevent one application from messing with another application's memory.

Third, virtual memory allows programs to see more memory than exists.














