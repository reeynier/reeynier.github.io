---
layout: post
title:  "How to Undo the Most Recent Local Commit in Git"
categories: [ Git ]
tags: [ Git Reset]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to undo the most recent local commit in Git.
---

<br />

##### Scenario A: Undo Latest Local Commit and Keep File Changes

```bash
$ git reset HEAD~1
```

The above command will:
* Undo the most recent local commit. 
* Your local changes of the files are still there.
* You need to add the changes and commit again.

Note: `HEAD~` is the same as `HEAD~1`.

##### Scenario B: Undo Latest Local Commit and Delete Local Changes 

```bash
$ git reset --hard HEAD~1
```

The above command will:
* Undo the most recent local commit.
* Your local changes of the files are **`Deleted`**. 


##### Scenario C: Undo Latest Local Commit but Keep File Changes and Git Index

```bash
$ git reset --soft HEAD~1
```

The above command will:
* Undo the most recent local commit.
* Your local changes of the files are still there.
* Your git index are still there -- you do not need to git add the changes again.





