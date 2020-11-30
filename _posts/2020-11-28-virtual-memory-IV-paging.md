---
layout: post
title:  "Virtual Memory IV: Paging"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Operating System ]
featured: false
hidden: false
excerpt: How can we virtualize memory with pages, so as to avoid the problems of segmentation
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 18.

## Paging

In the previous post about [segmentation]({% post_url 2020-11-27-virtual-memory-III-segmentation %}), we use segmentation (**variable-sized** pieces) for space management. However, this approach suffers from the `fragmentation` problem. Another approach is to chop up memory space into **fixed-size** pieces. We divide the physical memory into fixed-size units, also called as `pages`. So the question is how can we virtualize memory with pages, so as to avoid the problems of segmentation?


#### Overview

The figure below shows an example physical memory divided into fixed-size `pages`. In this case, there are 8 `page frames`. The pages of the virtual address space (AS) have been placed at different locations throughout physical memory. The OS itself is also using some of physical memory (page frame 0).
```
0      -----------------
      | reserved for OS |    page frame 0 of physical memory
16     -----------------     
      |    (unused)     |    page frame 1
32     -----------------  
      |   page 3 of AS  |    page frame 2
48     -----------------    
      |   page 0 of AS  |    page frame 3
64     -----------------  
      |    (unused)     |    page frame 4
80     -----------------   
      |   page 2 of AS  |    page frame 5
96     -----------------      
      |    (unused)     |    page frame 6
112    -----------------
      |   page 1 of AS  |    page frame 7
128    -----------------
```

Paging has a number of advantages over the segmentation approach. The first one is flexibility. With paging, the system can support address space abstraction effectively, without knowing how a process uses the address space. The second one is simplicity. Paging makes it simple for the OS to manage free space. The OS can keep a `free list` of all free pages, and assign and reclaim free spaces according to the list.

To record the mapping of virtual pages to the physical memory, the OS keeps a data structure called `page table` for **each process**. The `page tables` are used to store address translations for each of the virtual pages of the address space. For the example in the above figure, the page table stores four entries: virtual page 0 -> physical frame 3, virtual page 1 -> physical frame 7, virtual page 2 -> physical frame 5, virtual page 3 -> physical frame 2.

Now we have the page tables, let's consider the address translation. The figure below shows an example of how to translate the virtual address to the physical address. We split the virtual address into two components: the `virtual page number (VPN)` and the `offset` within the page. In the example below, the virtual address is 21 (010101 in binary). The VPN is 1 (01 in binary), and the offset is 5 (0101 in binary). 

```
                 |<-- VPN -->|<--     Offset      -->|
Virutal           -----------------------------------
Address          |  0  |  1  |  0  |  1  |  0  |  1  |
                  -----------------------------------
                    |     |     |     |     |     |
                   \|/   \|/    |     |     |     |
                  -----------   |     |     |     |   
                 |  Address  |  |     |     |     |
                 |Translation|  |     |     |     |
                  -----------   |     |     |     |
                    |     |     |     |     |     |
                   \|/   \|/   \|/   \|/   \|/   \|/
Physical    -----------------------------------------
Address    |  1  |  1  |  1  |  0  |  1  |  0  |  1  |
            -----------------------------------------
           |<--    PFN    -->|<--     Offset      -->|
```

The physical address also has two components: the `physical frame number (PFN)` (or `physical page number, PPN`) and the `offset`. From the page table, we know that the virtual page 1 is mapped to physical frame 7. So the PFN is 7 (111 in binary). The offset is kept as the same, because the offset just tells us which byte within the page we want. Thus, the translated physical address is 117 (1110101 in binary).

#### Page Table Details

In general, a page table stores **virtual-to-physical address translations** to let the OS know where each page of an address space actually resides in physical memory. The page tables are usually big, so the hardware MMU will not store the page table of the currently-running process. Instead, the page tables for each process are stored in memory.

One way to implement the page table is called the `linear page table`. In this case, the page table is implemented as an array. The OS indexes the array by the virtual page number (VPN), and looks up the page-table entry (PTE) at that index in order to find the desired physical frame number (PFN).

The figure below shows an example x86 `page table entry (PTE)`.
```
 31  30  29  28  27  26  25  24  23  22  21  20  19  18  17  16  15  14  13  12  11  10  09  08  07  06  05  04  03  02  01  00
 ------------------------------------------------------------------------------------------------------------------------------
|                                 PFN                                          | ///////// | G |PAT| D | A |PCD|PWT|U/S|R/W| P |  
 ------------------------------------------------------------------------------------------------------------------------------  
```

Now we describe the detail of address translation. To translate the virtual address to the correct physical address and fetch data from the physical address, the OS must first fetch the proper page table entry from the process's page table, perform the translation, and then load the data from physical memory. Below is the code of what happens during the translation.

```
// Extract the VPN from the virtual address
VPN = (VirtualAddress & VPN_MASK) >> SHIFT

// Form the address of the page table entry (PTE)
PTEAddr = PTBR + (VPN * sizeof(PTE))

// Fetch the PTE
PTE = AccessMemory(PTEAddr)

// Check if process can access the page
if (PTE.Valid == False)
    RaiseException(SEGMENTATION_FAULT)
else if (CanAccess(PTE.ProtectBits) == False)
    RaiseException(PROTECTION_FAULT)
else
    // Access is OK: form physical address and fetch it
    offset = VirtualAddress & OFFSET_MASK
    PhysAddr = (PTE.PFN << PFN_SHIFT) | Offset
    Register = AccessMemory(PhysAddr)
```
PTBR is the `page table base register`, which contains the physical address of the starting location of the page table.

We can see for each memory reference (whether an instruction fetch or an explicit load or store), paging requires us to perform **two** memory reference. One is to fetch the translation from the page table, the other is to fetch the data from the memory. This is costly and slows down the process.
