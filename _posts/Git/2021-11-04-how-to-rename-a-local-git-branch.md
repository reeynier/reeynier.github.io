---
layout: post
title:  "How to Rename a Local Git Branch (Short Answer)"
categories: [ Git ]
tags: [ Git Branch]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to rename a local git branch.
---

<br />

##### Scenario A: Rename the Current Branch

```bash
$ git branch -m <newname>
```

The above command will:
* Rename the current branch
* The renamed branch will still refer to the old upstream branch associated with it, if any.

##### Scenario B: Rename a Different Branch (Not the Current Branch)

```bash
$ git branch -m <oldname> <newname>
```

The above command will:
* Rename your branch
* The renamed branch will still refer to the old upstream branch associated with it, if any.

##### Scenario C: Push the Local Branch and Reset the Upstream Branch

```bash
$ git push origin -u <newname>
```

The above command will:
* Reset the upstream branch for the new-name local branch