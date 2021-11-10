---
layout: post
title:  "How to Revert a Git Repository to a Previous Commit (Short Answer)"
categories: [ Git ]
tags: [ Git Revert ]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to revert a git repository to a previous commit.
---

<br />



##### Scenario A: Temporarily Switch to a Different Commit

```bash
$ git checkout 0d1d7fc32
```

The above command will:
* checkout the desired commit
* detach your HEAD (leave you with no branch checked out)

##### Scenario B: Hard Delete Unpublished Commits

```bash
$ git reset --hard 0d1d7fc32
```

The above command will:
* destroy any local modifications
* if you want to keep uncommitted work, use `git stash`

##### Scenario C: Undo Published Commits With New Commits

```bash
$ git revert 0d1d7fc32 25eee4ca
```

or

```bash
$ git revert --no-commit 0d1d7fc32..HEAD
```

or

```bash
$ git revert -m 1 <merge_commit_sha>
```

The first command will:
* create two separate revert commits
* revert the two commits

The second command will:
* revert everything from the HEAD back to the commit hash
* `--no-commit` flag lets git revert all the commits at once

The third command will:
* revert a merge commit