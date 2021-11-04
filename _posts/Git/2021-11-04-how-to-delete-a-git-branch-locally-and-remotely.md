---
layout: post
title:  "How to Delete a Git Branch Locally and Remotely"
categories: [ Git ]
tags: [ Git Reset]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question how to delete a git branch locally and remotely.
---

<br />

##### Delete Local Branch

```bash
$ git branch -d <the_local_branch_name>
```

The above command will:
* Delete the local branch. You will receive an error if you try to delete the currently selected branch.
* Use `-D` (replace `-d` in the above command) to force delete the branch without checking merged status.


##### Delete Remote Branch

```bash
$ git push origin --delete <the_remote_branch_name>
```

The above command will:
* Remove a remote branch from the server.


