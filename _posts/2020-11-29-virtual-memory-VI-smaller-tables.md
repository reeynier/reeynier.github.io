---
layout: post
title:  "Virtual Memory VI: Smaller Tables"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Operating System ]
featured: false
hidden: false
excerpt: Paging also introduces the problem that page tables are too big and thus consume too much memory.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 20.

## Faster Translation


Besides performance, [paging]({% post_url 2020-11-28-virtual-memory-IV-paging %}) also introduces another problem: page tables are too big and thus consume too much memory. And we usually have one page table for every process in the system. So the question is how can we make page tables smaller?

To reduce the size of page tables, a simple solution is to use bigger pages. However, the major problem with this approach is that big pages lead to waste within each page. This problem is also known as `internal fragmentation`.

#### Multi-Level Page Tables

Assume we have an address space in which the used portions of the heap and stack are small, how to get rid of all those invalid regions in the page table instead of keeping them all in memory? We can have a `multiple-level page table`. 

The basic idea of multiple-level page table is that: we first divide the page table into page-sized units; if an entire page of page table entries (PTEs) is invalid, we do not allocate that page of the page table at all. To track whether a page of the page table is valid, we use a data structure called `page directory`. The page directory tells us where a page of the page table is, or that the entire page of the page table is not allocated.

The two figures below show examples of the linear page table, and the multi-level page table. For the linear page table, even though most of the middle regions of the address space are not valid, we still allocate page-table space for these regions. For the multi-level page table, the page directory marks just two pages of the page table as valid; thus, only those two pages of the page table resides in memory.

```
     Linear Page Table
      ---------------------
PTBR |         201         | ----
      ---------------------      |
                                 |
 valid  prot      PFN            |
 -------------------------   <---
|  1  | rx  |      12     |
|  1  | rx  |      13     | PFN 201
|  0  |  -  |       -     |
|  1  | rw  |     100     |
 -------------------------
|  0  |  -  |       -     |
|  0  |  -  |       -     | PFN 202
|  0  |  -  |       -     |
|  0  |  -  |       -     |
 -------------------------
|  0  |  -  |       -     |
|  0  |  -  |       -     | PFN 203
|  0  |  -  |       -     |
|  0  |  -  |       -     |
 -------------------------
|  0  |  -  |       -     |
|  0  |  -  |       -     | PFN 204
|  1  | rw  |      86     |
|  1  | rw  |      15     |
 -------------------------
```

```
    Multi-Level Page Table
      ---------------------
PDBR |         200         | ----
      ---------------------      |
                                 |
 valid      PFN                  |       valid  prot      PFN 
 -------------------  <----------        ------------------------- 
|  1  |      12     | --------------->  |  1  | rx  |      12     |
|  1  |      13     | PFN 200           |  1  | rx  |      13     | PFN 201
|  0  |       -     |                   |  0  |  -  |       -     |
|  1  |     100     | -------           |  1  | rw  |     100     |
 -------------------         |           -------------------------
 The Page Directory          |
                             |          [ Page 1 of PT: Not Allocated]
                             |
                             |          [ Page 2 of PT: Not Allocated]
                             |
                             |           -------------------------
                              --------> |  0  |  -  |       -     |
                                        |  0  |  -  |       -     | PFN 204
                                        |  1  | rw  |      86     |
                                        |  1  | rw  |      15     |
                                         -------------------------
```

For each page in the page table, the page directory contains one entry (`page directory entry, PDE`). A PDE minimally has a `valid bit` and a `page frame number (PFN)`. The valid bit means at least one of the pages of the page table that the entry points to (via PFN) is valid.

The advantages of the multi-level page table approach are: First, it only allocates page-table spaces in proportion to the amount of address space you are using; Second, each portion of the page table fits neatly within a page, making it easier to manage memory. The downside of using multi-level page table approach are: First, there is a cost to multi-level tables -- on a TLB miss, two loads from memory are required instead of one (for the linear page table approach); Second, it adds complexity to the hardware and the OS to handle the page-table lookup.


#### The Translation Process

The algorithm below shows the control flow of the multi-level page table approach. Before any page table access occurs, the hardware first checks the TLB. If there is a TLB hit, the physical address is formed directly without accessing the page table. If there is a TLB miss, the hardware needs to perform the multi-level lookup.

```
VPN = (VirtualAddress & VPN_MASK) >> SHIFT
(Success, TlbEntry) = TLB_Lookup(VPN)
if (Success == True)  // TLB Hit
    if (CanAccess(TlbEntry.ProtectBits) == True)
        Offset = VirtualAddress & OFFSET_MASK
        PhysAddr = (TlbEntry.PFN << SHIFT) | Offset
        Register = AccessMemory(PhysAddr)
    else
        RaiseException(PROTECTION_FAULT)
else  // TLB Miss
    // First, get page directory entry
    PDIndex = (VPN & PD_MASK) >> PD_SHIFT
    PDEAddr = PDBR + (PDIndex * sizeof(PDE))
    PDE = AccessMemory(PDEAddr)
    if (PDE.Valid == False)
        RaiseException(SEGMENTATION_FAULT)
    else
        // PDE is valid, now fetch PTE from page table
        PTIndex = (VPN & PT_MASK) >> PT_SHIFT
        PTEAddr = (PDE.PFN << SHIFT) + (PTIndex * sizeof(PTE))
        PTE = AccessMemory(PTEAddr)
        if (PTE.Valid == False)
            RaiseException(SEGMENTATION_FAULT)
        else if (CanAccess(PTE.ProtectBits) == False)
            RaiseException(PROTECTION_FAULT)
        else
            TLB_Insert(VPN, PTE.PFN, PTE.ProtectBits)
            RetryInstruction()
```






































