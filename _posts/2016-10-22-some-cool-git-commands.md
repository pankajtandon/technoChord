---
layout: post
title: "Some Cool Git Commands"
date: 2016-10-22 16:25:06 -0500
comments: true
---

#### To show all branches and their committers in reverse chronological order:

```
git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' | sort -k5nr -k2Mr -k3nr -k4nr
```

#### To find out what a certain committer worked on:

```
git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' | sort -k5n -k2M -k3n -k4n | grep -i pankaj

```

#### To list all files committed by author:

```
git ls-tree -r --name-only HEAD  | xargs -n1 git blame --line-porcelain HEAD | grep  "^filename \|^author " | awk '(NR%2){print$0p }{p="-"$0}' | sort | uniq -c
```

###### ...and exclude hidden files:
```
git ls-tree -r --name-only HEAD  | grep -v "^\." | xargs -n1 git blame --line-porcelain HEAD | grep  "^filename \|^author " | awk '(NR%2){print$0p }{p="-"$0}' | sort | uniq -c
```

#### To find out how many lines were committed by whom in a git repo:

```
git ls-tree -r -z --name-only HEAD | xargs -0 -n1 git blame --line-porcelain HEAD |grep  "^author "|sort|uniq -c|sort -nr
```
