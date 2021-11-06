---
layout: post
title:  "How to Checkout a Remote Git Branch (Short Answer)"
categories: [ Git ]
tags: [ Git Branch]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to checkout a remote git branch.
---

<br />

##### You Have One Remote

```bash
$ git fetch
$ git checkout <remote-branch-name>
```

The above commands will:
* Fetch all remote branches
* Checkout to a branch

##### You Have More Than One Remote

```bash
$ git fetch <remote-name>
$ git checkout -b <remote-branch-name> <remote-name>/<remote-branch-name>
```

The above commands will:
* Fetch all remote branches
* Create your own copy of that branch and checkout to the branch