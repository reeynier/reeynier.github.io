---
layout: post
title:  "Virtual Memory III: Segmentation"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Virtual Memory ]
featured: false
hidden: false
excerpt: How to support a large address space with (potentially) a lot of free space?
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 16.

## Segmentation

In the previous post about [address translation]({% post_url OS/2020-11-27-virtual-memory-II-address-translation %}), we use the base-and-bound approach to implement a simple virtual memory. The entire address space has been put in memory. This is usually wasteful as much of the space is usually not used by the process by still taking up the memory space. It is also hard to run a program when the entire address space does not fit into memory. So the question is how to support a large address space with (potentially) a lot of free space?

#### Generalized Base and Bounds

To solve this problem, we can use the `segmentation` technique. The idea is: instead of having only one base-and-bounds pair in MMU, we can have a base-and-bounds pair for each logical segment of the address space. We have three logical segments: code, stack, and heap. The OS can place each segment in different parts of physical memory, and thus avoid filling physical memory with unused virtual address space.

Below is an illustration of unused virtual address space:
```
 0 KB    ----------------
         | Program Code |
 2 KB    ----------------
         | //////////// |
 4 KB    ----------------
         |              |
         |     Heap     |
         |              |
 7 KB    ----------------
         |      |       |
         |     \|/      |
         |              |
         |  Free Space  |  <---- Unused Virtual Address Space
         |              |
         |     /|\      |            
         |      |       |     
14 KB    ----------------
         |              |
         |    Stack     |
         |              |
16 KB    ----------------
```


The hardware structure in MMU required to support segmentation is three base-and-bounds register pairs. Below is an example of register values in three pairs of base and bounds registers.

```
Segment    Base    Size    Grows Positive
-----------------------------------------
Code       32 K    2 K     1
Heap       34 K    3 K     1
Stack      28 K    2 K     0
```

Translation Example 1: virtual address 100.

This address is in the code segment. The physical address is: 32 K + 100 = 32868.

Translation Example 2: virtual address 4200.

This address is in the heap segment. The physical address is: 34 K + (4200 - 4K) = 34 K + (4200 - 4096) = 34920.

Translation Example 3: virtual address 15 K.

This address is in the stack segment. The stack segment grows backwards. In physical memory, it starts at 28 KB, and grows back to 26 KB, corresponding to virtual addresses 16 KB to 14 KB. Thus, the virtual address 15 K corresponds to the physical address 27 K.

If we are trying to access an illegal address, a `segmentation fault` will be raised.

#### OS Support

Segmentation raises a number of new issues for the operating system.

First, what should the OS do on a context switch? The segment registers must be saved and restored.

Second, when the segments grow, the OS need to provide more space and update the segment size register to the new (bigger) size.

Third, as each segment might be a different size, the physical memory will quickly become full of little holes of free space, making it difficult to allocate new segments, or to grow existing ones. This problem is called `external fragmentation`. One solution to this problem would be to compact physical memory by rearranging the existing segments. 



