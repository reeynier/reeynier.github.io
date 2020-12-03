---
layout: post
title:  "Virtual Memory VIII: Page Replacement Policies"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Virtual Memory ]
featured: false
hidden: false
excerpt: How can the OS decide which page(s) to evict from memory.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 22.

## Policies

In the previous post, we show the [page replacement mechanisms]({% post_url OS/2020-11-29-virtual-memory-VII-page-replacement-mechanisms %}). When a page fault occurs, the OS need to find a free page on the free-page list and assign it to the faulting page. When little memory is free, the OS starts `paging out` pages to make room for actively-used pages. The `replacement policy` is to decide which page(s) to `evict`. So the question is how can the OS decide which page(s) to evict from memory?

#### The Optimal Replacement Policy

Ideally, the replacement policy that leads to the fewest number of misses is to replace the page that will be accessed *furthest in the future*. It means you will refer to other pages before you refer to the one furthest out. This is equivalent to say that all other pages are more important than the one furthest out. Although this policy is simple, it is difficult to implement. This optimal replacement policy is often used for comparison, to understand how a particular replacement policy works.

#### A Simple Policy: FIFO

A simple policy is the `First-In, First-Out (FIFO)` replacement policy. The pages are simply placed in a queue when they enter the system. When a replacement occurs, the page on the tail of the queue (the first-in pages) is evicted. FIFO is simple to implement, but the hit rate can be low.

#### Another Simple Policy: Random

Another simple policy is `Random`, which simply picks a random page to replace. The Random replacement policy is also simple to implement. The performance of Random can be as good as optimal or much worse. How Random does depends on the luck it gets in its choices.


#### Using History: LRU

The FIFO policy and the Random policy have a common problem: it might kick out an important page which is about to be referenced again. We need something smarter. To improve our guess at the future, we can lean on the past and use history as our guide. For example, if a program has accessed a page in the near past, it is likely to access it again in the near future. The `Least-Recently-Used (LRU)` policy replaces the least recently used page when an eviction must take place. Similarly, the `Least-Frequently-Used (LFU)` policy replaces the least frequently used page.


#### Approximating LRU

Implementing the LRU plicy perfectly can be complicated. Specifically, upon each *page access*, we must update some data structure to move this page to the front of the list. To keep track of which pages have been least and most recently used, the system has to do some accounting work on every memory reference which could greatly reduce performance.

Implementing an approximating LRU is more feasible from a computational-overhead standpoint. The idea requires support from hardware. For each page, the hardware stores a `use bit` (or `reference bit`). When a page is referenced (i.e. read or written), the use bit is set by hardware to 1. Then the OS employs the `clock algorithm`. 

Imagine all the pages of the system arranged in a circular list. A `clock hand` points to some particular page to begin with (it doesn't really matter which). When a replacement must occur, the OS checks if the currently-pointed -to page has a use bit of 1 or 0. If the use bit is 1, this implies that this page was recently used and thus is *not* a good candidate for replacement. Thus, the use bit of this page will be set to 0 (cleared), and the clock hand is incremented to the next page. The algorithm continues until it finds a use bit that is set to 0, implying this page has not been recently used. In the worst case, all pages have been used and we have to search through the entire set of pages, clearing all the use bits. This approach has the nice property of not repeatedly scanning through all of memory looking for an unused page, but it is not the only way to employ a use bit to approximate LRU.








































