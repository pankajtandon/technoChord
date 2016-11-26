---
layout: post
title: "Some Cool Git Commands"
date: 2016-10-22 16:25:06 -0500
comments: true
---

#### To find out what a certain commiter worked on:

```
git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' | sort -k5n -k2M -k3n -k4n | grep -i pankaj

```

#### To find out how many lines were committed by whom in a git repo:

```
git ls-tree -r -z --name-only HEAD | xargs -0 -n1 git blame --line-porcelain HEAD |grep  "^author "|sort|uniq -c|sort -nr
```
