---
layout: post
title:  "How to Modify Existing Unpushed Commit Messages (Short Answer)"
categories: [ Git ]
tags: [ Git Commit]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to modify existing unpushed commit messages.
---

<br />

##### Scenario A: Long New Commit Message

```bash
$ git commit --amend
```

The above command will:
* open your editor
* allow you to change the commit message of the most recent commit

##### Scenario B: Short New Commit Message

```bash
$ git commit --amend -m "New commit message"
```

The above command will:
* update the commit message of the most recent commit