---
layout: post
title:  "How to Undo a Git Add Before Commit (Short Answer)"
categories: [ Git ]
tags: [ Git Reset]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to undo a git add before commit.
---

<br />

##### Scenario A: You Have Commits Previously

```bash
$ git reset <file>
```
or equivalently

```bash
$ git reset HEAD <file>
```

The above command will:
* Remove the file from the current index (the "about to be committed" list) without changing anything else


```bash
$ git reset
```

The above command will:
* Remove all files from the current index. This is handy if there are too many files to be listed one by one.


##### Scenario B: You Do Not Have Any Commits Yet (A New Repository)

```bash
$ git rm --cached <file>
```

The above command will:
* Remove (unstage) the file from the current index.

```bash
$ git rm -r --cached .
```

The above command will:
* Remove all files from the current index.
