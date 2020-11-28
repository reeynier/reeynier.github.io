---
layout: post
title:  "Virtual Memory IV: Paging"
categories: [ Operating System ]
tags: [ Virtual Memory ]
similar: [ Operating System ]
featured: false
hidden: false
excerpt: In the previous post about segmentation, we use variable-sized pieces for space management.
---

<br />

This post is adapted from Professor Remzi H. Arpaci-Dusseau and  Professor Andrea C. Arpaci-Dusseau's [OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/){:target="_blank"} book, Chapter 18.

## Paging

In the previous post about [segmentation]({% post_url 2020-11-27-virtual-memory-segmentation %}), we use segmentation (**variable-sized** pieces) for space management. However, this approach suffers from the `fragmentation` problem. Another approach is to chop up memory space into **fixed-size** pieces. We divide the physical memory into fixed-size units, also called as `pages`. So the question is how can we virtualize memory with pages, so as to avoid the problems of segmentation?





