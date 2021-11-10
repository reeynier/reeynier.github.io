---
layout: post
title:  "What is the Difference Between Git Pull and Git Fetch (Short Answer)"
categories: [ Git ]
tags: [ Git Pull]
similar: [ Git ]
featured: false
hidden: false
excerpt: Short answers to the question what is the difference between git pull and git fetch.
---

<br />

In its default mode, `git pull` is shorthand for `git fetch` followed by `git merge`.


##### Git Fetch

* Update your remote-tracking branches (get the latest version from remote to local)
* Does not change your local branches (does not automatically merge)


##### Git Pull

* Bring a local branch up-to-date with its remote version (get the latest version from remote to local, and merge into the local)
