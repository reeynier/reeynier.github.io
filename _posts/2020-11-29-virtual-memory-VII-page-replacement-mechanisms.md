---
layout: post
title:  "Virtual Memory VII: Page Replacement Mechanisms"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Operating System ]
featured: false
hidden: false
excerpt: How can the OS make use of a larger, slower device to transparently provide the illusion of a large virtual address space.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 21.

## Mechanisms


So far, we have assumed that every process's address space is small and fits into physical memory. To support large address spaces and create the illusion that there is enough memory for each process's address space, we need to go beyond the physical memory. We need a `hard disk drive` to support large address spaces for multiple concurrently-running processes. The goal is to support using more memory than is physically available. So the question is how can the OS make use of a larger, slower device to transparently provide the illusion of a large virtual address space?



The first thing we need to do is to reserve some space on the disk for moving pages back and forth. Such space is referred to as `swap space`. The OS can read from and write to the swap space in page-sized units. The OS need to remember the disk address of a given page.

To support swapping pages to and from the disk, we need some hardware support. Specifically, when the hardware looks in the page table entries (PTEs), it should be able to figure out whether the page is present or not in physical memory. So we have a `present bit` in the PTE. If the present bit is set to one, it means the page is present in physical memory; otherwise, the page is not in memory but somewhere on disk. The act of accessing a page that is not in physical memory is referred to as a `page fault`.


#### The Page Fault

If a page is not present in physical memory, the OS will handle the page fault. The OS need to swap the page back into memory. The OS first looks in the PTE to find the address of the page in the disk, and issues a request to disk to fetch the page into memory. When the disk I/O completes, the OS will update the page frame number (PFN) field of the PTE to record the in-memory location of the newly-fetched page, and retry the instruction. This attempt to retry the instruction will generate a TLB miss. The TLB will then be updated with the address translation. Finally, a last retry of the instruction will find the translation in the TLB and thus proceed to fetch the desired data or instruction from memory. Note that when the I/O is in flight, the process will be in the `blocked` state and thus the OS will run other processes.

The algorithm below shows the hardware page fault control flow.

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
    PTEAddr = PTBR + (VPN * sizeof(PTE))
    PTE = AccessMemory(PTEAddr)
    if (PTE.Valid == False)
        RaiseException(SEGMENTATION_FAULT)
    else 
        if (CanAccess(PTE.ProtectBits) == False)
            RaiseException(PROTECTION_FAULT)
        else if (PTE.Present == True)
            // Assuming hardware-managed TLB
            TLB_Insert(VPN, PTE.PFN, PTE.ProtectBits)
            RetryInstruction()
        else if (PTE.Present == False)
            RaiseException(PAGE_FAULT)
``` 


The algorithm below shows how the OS handle the page fault.

```
PFN = FindFreePhysicalPage()
if (PFN == -1)               // No free page found
    PFN = EvictPage()        // Run replacement algorithm
DiskRead(PTE.DiskAddr, PFN)  // Sleep (waiting for I/O)
PTE.present = True           // Update page table with present bit and translation (PFN)
PTE.PFN = PFN
RetryInstruction()           // Retry instruction
```

























