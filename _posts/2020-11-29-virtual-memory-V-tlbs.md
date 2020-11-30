---
layout: post
title:  "Virtual Memory V: TLBs"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Virtual Memory ]
featured: false
hidden: false
excerpt: How can we speed up address translation, and generally avoid the extra memory reference that paging seems to require?
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 19.

## Faster Translation

As discussed in [the previous post]({% post_url 2020-11-28-virtual-memory-IV-paging %}), using paging as the core mechanism to support virtual memory can lead to high performance overhead. This is because paging requires two memory lookups. So the problem is how can we speed up address translation, and generally avoid the extra memory reference that paging seems to require?

We can use the hardware for faster translation. Specifically, we add a cache to the hardware's memory management unit (MMU), also called the `translation-lookaside buffer (TLB)`. This cache stores some translation results (the PTEs). Upon each virtual memory reference, the hardware first checks the TLB to see if the desired translation is there already. If so, the translation is performed without having to consult the page table. Thus, we only need to have the second memory access (use the physical address to access memory), and we save the first memory access (consult the page table in memory).


#### TLB Basic Algorithm

Below shows the TLB control flow algorithm. It is a rough sketch of how hardware might handle a virtual address translation, assuming a simple linear page table and a hardware-managed TLB.
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
    else if (CanAccess(PTE.ProtectBits) == False)
        RaiseException(PROTECTION_FAULT)
    else 
        TLB_Insert(VPN, PTE.PFN, PTE.ProtectBits)
        RetryInstruction()
```

First, the hardware extracts the virtual page number (VPN) from the virtual address and checks if the TLB holds the translation for this VPN. If it holds, we have a TLB hit. We can do the checkings, calculate the physical address (as we discussed in the second part of the [paging]({% post_url 2020-11-28-virtual-memory-IV-paging %}) algorithm), and access memory.

If the TLB does not hold the translation for this VPN, we have a TLB miss. We can access the page table to find the translation, do the checkings, calculate the physical address, and access memory (as we discussed in [paging]({% post_url 2020-11-28-virtual-memory-IV-paging %})). And finally, we update the TLB with the translation.

#### Who Handles The TLB Miss

Both the hardware and the software (OS) can handle the TLB miss. For the architectures where hardware handles the TLB miss, the hardware knows where the page tables are located in memory (via a `page table base register`). When a TLB miss happens, the hardware will walk the page table, find the correct page table entry, extract the desired translation, update the TLB with the translation, and retry the instruction. For the architectures where the OS handles the TLB miss, the hardware simply raises an exception.  The exception will pause the current instruction stream, raises the privilege level to kernel mode, and jumps to a `trap handler`. The trap handler is code within the OS to handle TLB misses.  The code will lookup the translation in the page table, use special privileged instructions to update the TLB, and return from the trap. Then the hardware retries the instruction.

#### TLB Issue: Context Switch

With TLBs, some new issues arise when switching between processes. Specifically, the TLB contains virtual-to-physical translations that are only valid for the currently running process. THese translations are not meaningful for other processes. Thus, when switching from one process to another, the hardware and the OS must ensure that the running process will not use translations from previously running processes.

One approach for this problem is to simply `flush` the TLB on context switches. This can be accomplished with a privileged hardware instruction. However, the cost of this approach can be high as each time a process runs, it must incur TLB misses. To reduce this overhead, some systems add hardware support to enable sharing of the TLB across context switches. This is achieved by an `address space identifier (ASID)` field in the TLB. The ASID field is to differentiate between processes, so the TLB can hold translations from different processes at the same time without any confusion.